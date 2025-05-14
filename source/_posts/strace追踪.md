---
title: strace追踪
date: 2025-05-14 09:41:13
categories: 
  - "编程理论"
tags:
  - "strace" 
description: |
    使用strace形成构建过程日志。
---


# **解析构建过程**

详细分析 `cmake` 和 `make` 构建过程中发生了什么，包括：

1. **构建脚本的执行流程**
2. **`strace` 如何跟踪系统调用**
3. **构建过程中的关键阶段**
4. **如何分析 `strace` 日志定位问题**

------

## **1. 构建脚本的执行流程**

该脚本的主要逻辑如下：

### **1.1 参数检查**

```bash
if [ $# -ne 1 ]; then
    echo "Usage: $0 <project_dir>"
    exit 1
fi
```

- 检查是否传入正确的参数（项目目录）。
- 如果参数错误，打印用法并退出。

### **1.2 初始化变量**

```bash
PROJECT_DIR=$1
PROJECT_NAME=$(basename "$PROJECT_DIR")
TIMESTAMP=$(date +%s)
LOG_PREFIX="${PROJECT_NAME}_${TIMESTAMP}"
LOG_DIR="repos/build_logs"
```

- 提取项目名称、时间戳，并设置日志路径。

### **1.3 创建日志目录**

```bash
mkdir -p "$LOG_DIR"
```

- 确保日志目录存在，否则创建它。

### **1.4 构建日志记录**

```bash
{
    echo "开始构建项目: $PROJECT_NAME"
    echo "构建时间: $(date)"
    echo "----------------------------------------"
    ...
} 2>&1 | tee -a "$BUILD_LOG"
```

- 使用 `tee` 记录所有输出（stdout + stderr）到日志文件，同时显示在终端。

------

## **2. `strace` 如何跟踪构建过程**

脚本中使用 `strace` 跟踪 `cmake` 和 `make` 的系统调用：

```bash
strace -f -tt -T cmake .. 2>> "$BUILD_LOG" | tee -a "$BUILD_LOG"
strace -f -tt -T make -j$(nproc) 2>> "$BUILD_LOG" | tee -a "$BUILD_LOG"
```

### **`strace` 参数解析**

| 参数               | 作用                                                 |
| ------------------ | ---------------------------------------------------- |
| `-f`               | 跟踪子进程（`cmake` 和 `make` 通常会启动多个子进程） |
| `-tt`              | 显示精确到微秒的时间戳                               |
| `-T`               | 显示每个系统调用的耗时                               |
| `2>> "$BUILD_LOG"` | 将 `strace` 的输出（stderr）追加到日志文件           |
| `                  | tee -a "$BUILD_LOG"`                                 |

------

## **3. 构建过程中的关键阶段**

### **3.1 `cmake` 阶段**

`cmake ..` 执行时，`strace` 会记录以下关键操作：

1. **解析 `CMakeLists.txt`**
   - `open("CMakeLists.txt", O_RDONLY)`
      → 读取项目根目录的 `CMakeLists.txt`。
   - `stat(".../CMakeCache.txt", ...)`
      → 检查是否已有缓存（避免重复配置）。
2. **检测编译器**
   - `execve("/usr/bin/gcc", ["gcc", "--version"], ...)`
      → 调用 `gcc` 检查编译器版本。
   - `execve("/usr/bin/make", ["make", "--version"], ...)`
      → 检查 `make` 版本。
3. **生成构建系统**
   - `write(3, "add_library(mylib STATIC ...)", ...)`
      → 生成 `Makefile` 或 `build.ninja` 文件。
   - `open("CMakeFiles/CMakeOutput.log", O_WRONLY)`
      → 记录 `cmake` 的输出日志。

### **3.2 `make` 阶段**

`make -j$(nproc)` 执行时，`strace` 会记录：

1. **解析 `Makefile`**
   - `open("Makefile", O_RDONLY)`
      → 读取 `cmake` 生成的 `Makefile`。
   - `stat("main.cpp", ...)`
      → 检查源文件是否存在。
2. **并行编译**
   - `clone(child_stack=NULL, flags=CLONE_CHILD_CLEARTID|CLONE_CHILD_SETTID|SIGCHLD)`
      → 启动多个编译进程（`-j` 参数控制并发数）。
   - `execve("/usr/bin/g++", ["g++", "-c", "main.cpp", "-o", "main.o"], ...)`
      → 调用 `g++` 编译单个文件。
3. **链接**
   - `execve("/usr/bin/ld", ["ld", "-o", "myprogram", "main.o", "lib.a"], ...)`
      → 调用 `ld` 进行链接。
4. **文件操作**
   - `open("build/libmylib.a", O_WRONLY|O_CREAT)`
      → 创建静态库。
   - `rename("libmylib.so.tmp", "libmylib.so")`
      → 原子性更新动态库。

------

## **4. 如何分析 `strace` 日志定位问题**

### **4.1 查找错误**

- **`= -1` 返回值** 表示系统调用失败：

  ```
  open("missing_file.h", O_RDONLY) = -1 ENOENT (No such file or directory)
  ```

  → 文件不存在，检查路径是否正确。

- **`SIGSEGV` 或 `SIGKILL`**：

  ```
  --- SIGSEGV {si_signo=SIGSEGV, si_code=SEGV_MAPERR, si_addr=0x0} ---
  ```

  → 程序崩溃，可能是内存错误。

### **4.2 性能分析**

- **耗时长的系统调用**：

  ```
  stat("/usr/include/very/long/path.h", ...) = 0 <0.123456>
  ```

  → 如果 `stat` 调用耗时较长，可能是磁盘 I/O 瓶颈。

- **频繁的文件访问**：

  ```
  open("/usr/lib/gcc/x86_64-linux-gnu/9/include/stddef.h", O_RDONLY) = 3 <0.000123>
  ```

  → 如果同一个头文件被多次打开，考虑优化 `#include`。

### **4.3 网络问题**

如果 `cmake` 需要下载依赖：

```
connect(3, {sa_family=AF_INET, sin_port=htons(443), sin_addr=inet_addr("192.0.2.1")}, 16) = -1 ETIMEDOUT (Connection timed out)
```

→ 网络连接失败，检查代理或防火墙。

## 源码

```bash	
#!/bin/bash

# 参数检查
if [ $# -ne 1 ]; then
    echo "Usage: $0 <project_dir>"
    exit 1
fi

PROJECT_DIR=$1
PROJECT_NAME=$(basename "$PROJECT_DIR")
TIMESTAMP=$(date +%s)
LOG_PREFIX="${PROJECT_NAME}_${TIMESTAMP}"
LOG_DIR="repos/build_logs"

# 创建日志目录
mkdir -p "$LOG_DIR"

# 构建日志路径
BUILD_LOG="${LOG_DIR}/${LOG_PREFIX}.log"

# 开始记录日志
{
    echo "开始构建项目: $PROJECT_NAME"
    echo "构建时间: $(date)"
    echo "----------------------------------------"

    # 进入项目目录
    cd "$PROJECT_DIR" || exit 1

    # 创建build目录
    mkdir -p build
    cd build || exit 1

    echo "执行 CMake 配置..."
    # 修改strace输出重定向方式
    strace -f -tt -T cmake .. 2>> "$BUILD_LOG" | tee -a "$BUILD_LOG"

    echo "执行 Make 构建..."
    # 修改strace输出重定向方式
    strace -f -tt -T make -j$(nproc) 2>> "$BUILD_LOG" | tee -a "$BUILD_LOG"

    # 检查构建结果
    BUILD_STATUS=${PIPESTATUS[1]}
    if [ $BUILD_STATUS -ne 0 ]; then
        echo "构建失败，退出代码: $BUILD_STATUS"
        exit 1
    fi

    echo "构建成功完成"

    # 添加系统资源使用信息
    echo "----------------------------------------"
    echo "系统资源使用情况:"
    echo "CPU: $(top -bn1 | grep "Cpu(s)" | awk '{print $2}')%"
    echo "Memory: $(free -m | awk '/Mem:/ {printf "%.2f GB", $3/1024}')"
    
} 2>&1 | tee -a "$BUILD_LOG"

exit ${PIPESTATUS[0]}
```



## **6. 总结**

| 阶段          | 关键操作                                           | 常见问题                       |
| ------------- | -------------------------------------------------- | ------------------------------ |
| `cmake`       | 解析 `CMakeLists.txt`、检测编译器、生成 `Makefile` | 编译器缺失、缓存问题           |
| `make`        | 并行编译、链接、文件操作                           | 头文件缺失、链接错误、竞争条件 |
| `strace` 分析 | 检查 `= -1` 错误、耗时长的调用、网络问题           | 文件权限、I/O 瓶颈、超时       |

