---
title: 使用 eBPF 实时追踪软件构建过程
date: 2025-05-28 10:00:00
categories:
  - "编程实战"
  - "系统监控"
tags:
  - "eBPF"
  - "系统调用追踪"
  - "构建分析"
  - "性能监控"
description: |
    利用 eBPF 技术，实时追踪软件构建过程中关键的系统调用（如进程创建和文件访问），以理解构建依赖和流程。
---




### **一、引言：为什么要追踪软件构建过程？**

软件构建（如使用 `make`, `cmake`, `gcc`, `cargo` 等）通常涉及一系列复杂的步骤：
*   **进程创建**：调用编译器、链接器、代码生成器等。
*   **文件访问**：读取源代码、头文件、库文件；写入目标文件、日志、中间产物。

理解这些底层的操作对于：
*   **依赖分析**：找出哪些文件真正影响了构建结果。
*   **性能瓶颈定位**：发现构建过程中耗时较长的步骤或不必要的文件操作。
*   **构建系统调试**：深入了解构建工具的实际行为。

传统工具如 `strace` 虽然可以追踪系统调用，但其通过 `ptrace` 实现，性能开销巨大，不适合实时监控复杂的构建过程。**eBPF** 提供了一种在内核态进行高效、低开销监控的强大机制。

### **二、eBPF 追踪构建过程的基本原理**

#### 1. **什么是 eBPF？**

- **eBPF**（Extended Berkeley Packet Filter）是 Linux 内核中的一种虚拟机，允许用户在不修改内核代码、不重新编译内核的情况下，将自定义的小程序（eBPF 程序）动态加载到内核中运行。
- 这些 eBPF 程序可以挂钩到内核的特定事件点（如系统调用、函数入口/出口、网络事件等），安全地收集信息或进行有限的操作。

#### 2. **为什么用 eBPF 追踪构建？**

- **低开销**：eBPF 程序在内核中运行，事件过滤和初步处理也在内核完成，避免了大量数据在内核态和用户态之间的频繁拷贝，性能远超 `strace`。
- **安全性**：eBPF 程序在加载到内核前会经过严格的验证器检查，确保其不会导致内核崩溃或产生安全问题。
- **灵活性**：可以精确地选择要追踪的事件和收集的数据。

#### 3. **本工具追踪的关键事件 (通过 Tracepoints)**

**Tracepoints** 是内核源码中预设的静态探测点，提供稳定的 ABI，是进行事件追踪的推荐方式。本工具主要关注以下 tracepoints：

*   `syscalls:sys_enter_execve`: 当任何进程即将执行一个新的程序时触发。用于捕获构建命令（如 `gcc`, `cmake`）及其调用的其他工具的执行。
*   `syscalls:sys_enter_openat`: 当任何进程即将打开一个文件时触发 (现代Linux上 `open` 通常是 `openat` 的封装)。用于捕获源文件、依赖库的读取，以及目标文件、日志的写入。
*   `sched:sched_process_fork`: 当一个新进程被创建时（通过 `fork` 或 `clone`）触发。用于将追踪范围从父构建进程扩展到其所有子进程。
*   `sched:sched_process_exit`: 当一个进程退出时触发。用于清理追踪状态。

### **三、详细追踪流程与代码解析**

#### 1. **eBPF C 程序核心逻辑 (`bpf_text`)**

我们的 eBPF 程序是用 C 语言编写的，它将在内核中运行。

##### a. 数据结构与BPF Map

```c
// Data structure for events sent to userspace
struct event_t {
    u64 ts_ns;          // Nanosecond timestamp (monotonic from boot)
    u32 pid;            // Process ID
    u32 ppid;           // Parent Process ID
    char comm[TASK_COMM_LEN]; // Command name
    char event_type;    // 'E' for exec, 'O' for open
    char filename[MAX_FILENAME_LEN]; // Filename for exec/open
    int flags_or_ret;   // Flags for open, placeholder for exec
};
BPF_PERF_OUTPUT(events); // Perf buffer to send events to userspace

// BPF map to store PIDs of processes we want to trace
BPF_HASH(pids_to_trace, u32, u8); // Key: PID, Value: 1 (means trace)
```
*   `struct event_t`: 定义了从内核发送到用户空间的数据包格式。
*   `BPF_PERF_OUTPUT(events)`: 声明一个性能事件缓冲区，用于高效地将 `event_t` 数据发送给用户态的 Python 程序。
*   `BPF_HASH(pids_to_trace, u32, u8)`: 声明一个哈希表（BPF map），用于在内核中存储需要追踪的进程ID。这是实现选择性追踪的关键。

##### b. 追踪 `execve` 系统调用

```c
TRACEPOINT_PROBE(syscalls, sys_enter_execve) {
    struct event_t event = {};
    struct task_struct *task = (struct task_struct *)bpf_get_current_task();

    event.ts_ns = bpf_ktime_get_ns(); // Get monotonic timestamp
    event.pid = bpf_get_current_pid_tgid() >> 32; // Get current PID

    // Get Parent PID (PPID) using bpf_probe_read_kernel (CO-RE is preferred if available)
    event.ppid = 0;
    if (task) {
        struct task_struct *real_parent_ptr;
        if (bpf_probe_read_kernel(&real_parent_ptr, sizeof(real_parent_ptr), &task->real_parent) == 0 && real_parent_ptr) {
            bpf_probe_read_kernel(&event.ppid, sizeof(event.ppid), &real_parent_ptr->tgid);
        }
    }

    bpf_get_current_comm(&event.comm, sizeof(event.comm)); // Get current command name
    bpf_probe_read_user_str(&event.filename, sizeof(event.filename), (void *)args->filename); // Get filename being exec'd
    
    event.event_type = 'E';
    events.perf_submit(args, &event, sizeof(event)); // Send event to userspace
    return 0;
}
```
*   当任何进程调用 `execve` 时，此探针被触发。
*   它收集进程ID、父进程ID、当前命令名、执行的文件名和时间戳。
*   **所有 `execve` 事件都会被发送到用户空间**。用户空间逻辑将决定这个 `execve` 是否是触发器（如 `make`, `gcc`），如果是，则将此PID添加到内核的 `pids_to_trace` map 中。

##### c. 追踪 `openat` 系统调用

```c
TRACEPOINT_PROBE(syscalls, sys_enter_openat) {
    u32 pid = bpf_get_current_pid_tgid() >> 32;
    // !!! Crucial Filter: Only trace if PID is in our map !!!
    u8 *should_trace = pids_to_trace.lookup(&pid);
    if (should_trace == NULL) {
        return 0; // Not a traced process, ignore this openat
    }

    struct event_t event = {};
    // ... (collect pid, comm, filename, flags, timestamp) ...
    bpf_probe_read_user_str(&event.filename, sizeof(event.filename), (void *)args->filename);
    event.flags_or_ret = args->flags;
    event.event_type = 'O';
    events.perf_submit(args, &event, sizeof(event));
    return 0;
}
```
*   当任何进程调用 `openat` 时触发。
*   **关键过滤**：首先检查当前进程的PID是否存在于 `pids_to_trace` map中。如果不存在，则说明这个 `openat` 调用与我们关心的构建过程无关，直接返回，不进行任何处理。
*   如果需要追踪，则收集相关信息并发送到用户空间。

##### d. 追踪进程创建与退出 (维护 `pids_to_trace` map)

```c
TRACEPOINT_PROBE(sched, sched_process_fork) {
    u32 parent_pid = args->parent_pid;
    u32 child_pid = args->child_pid;
    u8 *is_parent_traced = pids_to_trace.lookup(&parent_pid);

    if (is_parent_traced) { // If parent is traced...
        u8 one = 1;
        pids_to_trace.update(&child_pid, &one); // ...trace the child too.
    }
    return 0;
}

TRACEPOINT_PROBE(sched, sched_process_exit) {
    u32 pid = bpf_get_current_pid_tgid() >> 32;
    pids_to_trace.delete(&pid); // Clean up map when process exits
    return 0;
}
```
*   `sched_process_fork`: 当一个被追踪的进程创建子进程时，将子进程的PID也加入到 `pids_to_trace` map中，确保追踪链的延续。
*   `sched_process_exit`: 当进程退出时，将其从 `pids_to_trace` map中移除，保持map的清洁。

#### 2. **Python 用户空间控制程序**

Python 脚本（使用 BCC 框架）负责：
*   加载和管理 eBPF C 程序。
*   处理用户输入（如日志文件名、触发命令列表）。
*   从内核的 perf buffer 中读取事件。
*   实现时间戳校准。
*   根据 `execve` 事件的程序名，判断是否为触发命令，并更新内核的 `pids_to_trace` BPF map。
*   格式化事件数据并写入日志文件。

##### a. 初始化与BPF加载

```python
from bcc import BPF
# ... (argparse for --output, --triggers) ...

# eBPF C code as a string
bpf_text = """... (as shown above) ..."""

# Load BPF program
b = BPF(text=bpf_text)
pids_to_trace_map = b.get_table("pids_to_trace") # Get a reference to the BPF map
```

##### b. 时间戳校准 (重要)

内核 `bpf_ktime_get_ns()` 返回的是自系统启动以来的 monotonic 时间戳。我们需要将其转换为标准的 wall clock 时间（自 Epoch）。

```python
import time
from datetime import datetime, timezone

INITIAL_BOOT_TIME_NS = 0
try:
    # Preferred: Read boot time (seconds since epoch) from /proc/stat
    with open("/proc/stat", "r") as f:
        for line in f:
            if line.startswith("btime "):
                INITIAL_BOOT_TIME_NS = int(line.split()[1]) * 1_000_000_000 # s to ns
                break
    if INITIAL_BOOT_TIME_NS == 0: raise FileNotFoundError("btime not found")
except Exception as e:
    # Fallback: Estimate using current wall time and monotonic time
    WALL_TIME_AT_SCRIPT_START_NS = int(datetime.now(timezone.utc).timestamp() * 1_000_000_000)
    MONOTONIC_TIME_AT_SCRIPT_START_NS = time.monotonic_ns()
    INITIAL_BOOT_TIME_NS = WALL_TIME_AT_SCRIPT_START_NS - MONOTONIC_TIME_AT_SCRIPT_START_NS
```
这个 `INITIAL_BOOT_TIME_NS` 将用于校准每个事件的时间戳。

##### c. 事件处理回调

```python
def print_event(cpu, data, size):
    event = b["events"].event(data) # Cast raw data to event_t

    # Apply timestamp correction
    corrected_event_ts_ns = INITIAL_BOOT_TIME_NS + event.ts_ns
    timestamp_str = datetime.fromtimestamp(corrected_event_ts_ns / 1e9, timezone.utc).isoformat()

    if event.event_type == b'E': # Exec event
        filename_decoded = event.filename.decode('utf-8', 'replace')
        executable_name = os.path.basename(filename_decoded)

        # If it's a trigger command, add its PID to the kernel map
        if executable_name in trigger_commands and event.pid not in userspace_activated_pids:
            key = ct.c_uint(event.pid)
            leaf = ct.c_ubyte(1)
            pids_to_trace_map[key] = leaf # Update BPF map
            userspace_activated_pids.add(event.pid)
            # Log trigger message
            log_file.write(f"# {timestamp_str} INFO: Triggered by '{executable_name}' ...\n")
        
        # Log the exec event if its PID (or its ancestor) was a trigger
        key_check = ct.c_uint(event.pid)
        if key_check in pids_to_trace_map:
            # ... (format and write EXEC log line) ...
            log_file.write(f"{timestamp_str} {event.pid} ... EXEC {filename_decoded}\n")

    elif event.event_type == b'O': # Open event (already filtered by BPF for traced PIDs)
        # ... (format and write OPEN log line) ...
        filename_decoded = event.filename.decode('utf-8', 'replace')
        # Further userspace filtering for common non-source files can be added here
        if not filename_decoded.startswith(("/dev/", "/proc/", "/sys/")):
             log_file.write(f"{timestamp_str} {event.pid} ... OPEN {filename_decoded} (flags: {event.flags_or_ret:#x})\n")

# Open perf buffer and attach callback
b["events"].open_perf_buffer(print_event, page_cnt=128)

# Poll for events
while True:
    try:
        b.perf_buffer_poll(timeout=100)
    except KeyboardInterrupt:
        break
```
*   `print_event` 函数是核心。当eBPF程序通过perf buffer发送事件时，此函数被调用。
*   它首先校正时间戳。
*   对于 `EXEC` 事件 (`event_type == b'E'`)：
    *   检查执行的程序名是否在用户提供的 `trigger_commands` 列表中。
    *   如果是，则通过 `pids_to_trace_map[key] = leaf` 将该进程的PID更新到内核的BPF map中，以便内核开始追踪该进程的 `openat` 调用及其子进程。
    *   记录 `EXEC` 事件。
*   对于 `OPEN` 事件 (`event_type == b'O'`)：
    *   这些事件已经被内核中的eBPF程序根据 `pids_to_trace` map过滤过了，所以我们直接记录它们。
    *   可以添加额外的用户空间过滤（例如，忽略对 `/dev`, `/proc` 等虚拟文件系统的访问）。

#### 3. **数据流图示**

```
+---------------------------+     +----------------------------+     +---------------------------------+
| 1. User runs `make` (PID X) | --> | 2. sys_enter_execve hook   | --> | 3. Python: 'make' is trigger.   |
| (Initial Trigger Command) |     |    eBPF sends exec event.  |     |    Update BPF_HASH(pids_to_trace)|
+---------------------------+     +----------------------------+     |    with X. Log EXEC event.      |
                                                                     +---------------------------------+
                                                                                       | (PID X now in map)
                                                                                       v
+---------------------------+     +----------------------------+     +---------------------------------+
| 4. `make` (PID X) calls   | --> | 5. sys_enter_openat hook.  | --> | 6. Python: Log OPEN event for   |
|    `open("Makefile")`     |     |    eBPF: X in map? Yes.    |     |    Makefile.                    |
+---------------------------+     |    Send open event.        |     +---------------------------------+
                                  +----------------------------+

+---------------------------+     +----------------------------+     +---------------------------------+
| 7. `make` (PID X) forks   | --> | 8. sched_process_fork hook.| --> | 9. eBPF: X in map? Yes.         |
|    child `gcc` (PID Y)    |     |    Parent=X, Child=Y.      |     |    Add Y to BPF_HASH.           |
+---------------------------+     +----------------------------+     +---------------------------------+
                                                                                       | (PID Y now in map)
                                                                                       v
+---------------------------+     +----------------------------+     +---------------------------------+
| 10. `gcc` (PID Y) execs   | --> | 11. sys_enter_execve hook. | --> | 12. Python: 'gcc' is trigger.   |
|     itself.               |     |     eBPF sends exec event. |     |     (Optional) Update BPF_HASH. |
+---------------------------+     +----------------------------+     |     Log EXEC event for gcc.     |
                                                                     +---------------------------------+
```
