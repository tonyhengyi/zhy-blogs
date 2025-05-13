---
title: "Linux 套接字编程"
date: 2025-05-13
categories: 
  - "编程"
tags:
  - "Linux"
  - "网络"
  - "Socket"
description: |
    简单的套接字介绍
---



# 编程套接字

## 目录
1. [基础概念](#基础概念)
2. [Socket API详解](#socket-api详解)
3. [UDP编程](#udp编程)
4. [TCP编程](#tcp编程)
5. [地址转换函数](#地址转换函数)
6. [TCP vs UDP](#tcp-vs-udp)
7. [总结](#总结)

---

## 基础概念

### IP地址与端口号
- **IP地址**：标识网络中的一台主机（如 `192.168.1.1`）。
- **端口号**：2字节整数（0-65535），标识主机上的进程。  
  示例：QQ消息需通过IP地址发送到目标机器，再通过端口号区分具体进程。

### 网络字节序
- **大端字节序**：高位字节存储在低地址（网络传输标准）。
- **小端字节序**：高位字节存储在高地址（常见于x86架构）。
- 转换函数：  
  ```c
  #include <arpa/inet.h>
  uint32_t htonl(uint32_t hostlong);  // 主机转网络（32位）
  uint16_t htons(uint16_t hostshort); // 主机转网络（16位）
  ```

### TCP与UDP协议对比
| 特性         | TCP                | UDP                |
|--------------|--------------------|--------------------|
| 连接方式     | 有连接（三次握手） | 无连接             |
| 可靠性       | 可靠传输           | 不可靠传输         |
| 数据形式     | 字节流             | 数据报             |
| 典型场景     | 文件传输、网页浏览 | 实时视频、DNS查询  |

---

## Socket API详解
### 核心函数
```c
int socket(int domain, int type, int protocol); // 创建socket
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen); // 绑定端口
int listen(int sockfd, int backlog);            // 监听连接
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen); // 接受连接
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen); // 建立连接
```

### 关键数据结构
- **sockaddr**：通用地址结构，需强制转换为具体类型（如 `sockaddr_in`）。
- **sockaddr_in**（IPv4）：
  ```c
  struct sockaddr_in {
      sa_family_t sin_family; // 地址类型（AF_INET）
      in_port_t sin_port;     // 端口号（16位）
      struct in_addr sin_addr; // IP地址（32位）
  };
  ```

---

## UDP编程
### 服务器实现（C++示例）
```cpp
// 创建UDP Socket并绑定端口
UdpSocket sock;
sock.Socket();
sock.Bind("0.0.0.0", 8888);

// 接收数据
std::string req, client_ip;
uint16_t client_port;
sock.RecvFrom(&req, &client_ip, &client_port);

// 发送响应
std::string resp = "Hello from server!";
sock.SendTo(resp, client_ip, client_port);
```


### 客户端实现
```cpp
UdpClient client("127.0.0.1", 8888);
client.SendTo("Hello from client!");
std::string resp;
client.RecvFrom(&resp);
```

---

## TCP编程
### 单线程服务器
```cpp
TcpServer server("0.0.0.0", 9999);
server.Start([](const std::string& req, std::string* resp) {
    *resp = "Response: " + req;
});
```

### 多进程版本
```cpp
// 父进程处理连接请求后fork子进程
int ret = fork();
if (ret == 0) {
    // 子进程处理数据读写
    ProcessRequest(new_sock);
    exit(0);
}
```

### 多线程版本
```cpp
pthread_t tid;
pthread_create(&tid, NULL, ThreadEntry, arg); // 创建线程处理请求
pthread_detach(tid); // 分离线程
```

---

## 地址转换函数
- **字符串转IP**：`inet_aton("127.0.0.1", &addr.sin_addr);`
- **IP转字符串**：`char* ip_str = inet_ntoa(addr.sin_addr);`
- **注意**：`inet_ntoa` 非线程安全，推荐使用 `inet_ntop`。

---

## TCP vs UDP
### 三次握手与四次挥手
- **三次握手**：  
  1. 客户端发送SYN  
  2. 服务端回复SYN-ACK  
  3. 客户端发送ACK  
- **四次挥手**：  
  1. 客户端发送FIN  
  2. 服务端回复ACK  
  3. 服务端发送FIN  
  4. 客户端回复ACK  

### 适用场景
- **TCP**：需可靠传输的场景（如HTTP、FTP）。  
- **UDP**：低延迟、可容忍丢包（如直播、VoIP）。

---

## 总结
- **TCP** 提供可靠连接，适合需要数据完整性的场景。  
- **UDP** 轻量高效，适合实时性要求高的场景。  


