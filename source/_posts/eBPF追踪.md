---
title: eBPF追踪
date: 2025-05-14 09:41:05
categories: 
  - "编程实战"
tags:
  - "eBPF" 
  - "系统调用追踪"
description: |
    使用eBPF追踪调用系统调用。
---


### **一、eBPF 追踪系统调用的基本原理**

#### 1. **什么是 eBPF？**

- **eBPF**（Extended Berkeley Packet Filter）是 Linux 内核中的一种虚拟机，允许用户在不修改内核代码的情况下，**动态注入小程序**到内核中运行。
- **类比**：就像给 Linux 内核安装了一个“插件系统”，可以实时监控或修改内核的行为。

#### 2. **为什么用 eBPF 追踪系统调用？**

- 传统工具（如 `strace`）通过 **劫持进程的系统调用表** 来监控，性能开销极大（可能慢 100 倍以上）。
- eBPF 直接在 **内核态** 收集数据，几乎无性能损耗。

#### 3. **追踪系统调用的两种方式**

| 方式           | 原理                                                    | 优缺点                     |
| -------------- | ------------------------------------------------------- | -------------------------- |
| **kprobe**     | 挂钩内核函数（如 `__x64_sys_open`）                     | 灵活但依赖内核版本，不稳定 |
| **tracepoint** | 挂钩内核预定义的静态探针（如 `raw_syscalls:sys_enter`） | 稳定但仅能访问预定义的参数 |

**本脚本使用的是 `tracepoint`**（更稳定）。

------

### **二、详细追踪流程分解**

#### 1. **内核提供的 tracepoint：`sys_enter`**

- Linux 内核在每次系统调用开始时，会触发一个预定义的 tracepoint，名为：

  ```
  raw_syscalls:sys_enter
  ```

- 这个 tracepoint 会暴露系统调用的 参数，包括：

  - `args->id`：系统调用号（如 `read` 是 `0`，`write` 是 `1`）。
  - `args->args[0..5]`：系统调用的 6 个参数。

#### 2. **eBPF 程序的挂载过程**

```
bpf_text = """
TRACEPOINT_PROBE(raw_syscalls, sys_enter) {
    u32 key = args->id;              // 获取系统调用号
    syscall_count.increment(key);    // 统计次数
    return 0;
}
"""
b = BPF(text=bpf_text)  # 加载并自动挂载
```

- **`TRACEPOINT_PROBE`**：告诉 eBPF 将这个程序挂载到 `sys_enter` 事件。
- **`args->id`**：从 tracepoint 的参数中提取系统调用号。
- **`syscall_count.increment(key)`**：在 eBPF 的哈希表中对对应的调用号 +1。

**挂载后的内核行为**：

```
+---------------------+
| 用户程序调用 read()   |
+----------+----------+
           |
           v
+----------+----------+
| 内核触发 sys_enter   |
| (args->id = 0)       |
+----------+----------+
           |
           v
+----------+----------+
| eBPF 程序累加计数器   |
| syscall_count[0]++  |
+---------------------+
```

#### 3. **用户态读取统计数据**

```
for k, v in b["syscall_count"].items():
    syscall_id = k.value
    count = v.value
    name = syscall_names.get(syscall_id, f"unknown({syscall_id})")
```

- **`b["syscall_count"]`**：从内核中的 eBPF 哈希表读取数据。
- **`syscall_names`**：将数字转换为可读名称（如 `0 -> "read"`）。

------

### **三、关键代码段逐行解析**

#### 1. **BPF 程序定义**

```
#include <uapi/linux/ptrace.h>
BPF_HASH(syscall_count, u32);  // 定义哈希表，键是 u32，值自动累加
```

- `#include`：引入内核头文件，访问 tracepoint 的参数。
- `BPF_HASH`：定义一个哈希表，键是系统调用号（`u32`），值是调用次数。

```
TRACEPOINT_PROBE(raw_syscalls, sys_enter) {
    u32 key = args->id;         // 提取系统调用号
    syscall_count.increment(key); // 计数 +1
    return 0;                   // 必须返回 0
}
```

- `TRACEPOINT_PROBE`：宏，用于挂载到 `sys_enter`。
- `args->id`：系统调用号（如 `read` 是 `0`）。

#### 2. **Python 端的处理**

```
b = BPF(text=bpf_text)  # 编译并加载 BPF 程序
```

- 这一行会将 BPF 代码编译成字节码，加载到内核，并自动挂载到 `sys_enter`。

```
while True:
    time.sleep(args.interval)
    for k, v in b["syscall_count"].items():  # 读取内核中的哈希表
        syscall_id = k.value
        count = v.value
    b["syscall_count"].clear()  # 清空计数器
```

- `b["syscall_count"]`：访问 eBPF 哈希表。
- `clear()`：重置统计，准备下一轮。

------

### **四、完整数据流图示**

```
+-------------------+     +---------------------+     +------------------+
| 用户程序调用 read() | --> | 内核触发 sys_enter    | --> | eBPF 程序计数      |
+-------------------+     | (args->id = 0)       |     | syscall_count[0]++|
                          +---------------------+     +------------------+
                                                             |
                                                             v
+------------------+     +---------------------+     +------------------+
| Python 读取哈希表  | <-- | 每 N 秒读取并清空     | <-- | 写入日志文件       |
| syscall_count[0] |     | b["syscall_count"]   |     | "read: 42"       |
+------------------+     +---------------------+     +------------------+
```

