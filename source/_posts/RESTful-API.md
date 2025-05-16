---
title: RESTful-API
date: 2025-05-16 20:59:15
categories: 
  - "编程理论"
tags:
  - "restful" 
  - "服务器"
description: |
    一种服务器接口的规范
---


# RESTful API 

## 1. 什么是RESTful API

REST(Representational State Transfer)是一种软件架构风格，旨在指导网络应用的架构设计和开发。RESTful API是基于REST原则设计的Web API，它使用HTTP协议的标准方法对资源进行操作。

## 2. REST的六个约束条件

1. **客户端-服务器架构**：关注点分离，客户端负责用户界面，服务器负责数据存储
2. **无状态**：每个请求必须包含处理所需的所有信息
3. **可缓存**：响应必须明确表明是否可缓存
4. **统一接口**：简化系统架构，提高可见性
5. **分层系统**：客户端不需要知道是否直接连接到最终服务器
6. **按需代码(可选)**：服务器可以临时扩展或自定义客户端功能

## 3. RESTful API设计原则

### 3.1 URL设计

- **使用名词而非动词**：

  - 正确：`/users` (获取用户列表)
  - 错误：`/getUsers`

- **资源使用复数形式**：

  - 正确：`/users/123`
  - 错误：`/user/123`

- **URL层级表示关系**：

  ```
  /users/{userId}/orders  # 获取某用户的所有订单
  /users/{userId}/orders/{orderId}  # 获取某用户的特定订单
  ```

- **版本控制**（可选）：

  ```
  /v1/users  # 版本1的用户API
  /v2/users  # 版本2的用户API
  ```

  或者通过HTTP头控制：

  ```
  Accept: application/vnd.myapi.v1+json
  ```

### 3.2 HTTP方法使用

| HTTP方法 | 操作           | 幂等性 | 安全性 |
| -------- | -------------- | ------ | ------ |
| GET      | 获取资源       | 是     | 是     |
| POST     | 创建资源       | 否     | 否     |
| PUT      | 更新整个资源   | 是     | 否     |
| PATCH    | 部分更新资源   | 否     | 否     |
| DELETE   | 删除资源       | 是     | 否     |
| HEAD     | 获取资源元数据 | 是     | 是     |
| OPTIONS  | 获取可用操作   | 是     | 是     |

### 3.3 状态码使用

| 状态码 | 含义                  | 使用场景         |
| ------ | --------------------- | ---------------- |
| 200    | OK                    | 成功请求         |
| 201    | Created               | 资源创建成功     |
| 204    | No Content            | 成功但无返回内容 |
| 400    | Bad Request           | 请求参数错误     |
| 401    | Unauthorized          | 未认证           |
| 403    | Forbidden             | 无权限           |
| 404    | Not Found             | 资源不存在       |
| 405    | Method Not Allowed    | 不支持的HTTP方法 |
| 429    | Too Many Requests     | 请求过于频繁     |
| 500    | Internal Server Error | 服务器内部错误   |
| 503    | Service Unavailable   | 服务不可用       |

## 4. 请求和响应示例

### 4.1 获取用户列表

**请求**:

```
GET /v1/users HTTP/1.1
Host: api.example.com
Accept: application/json
```

**响应**:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    {
      "id": 1,
      "name": "张三",
      "email": "zhangsan@example.com",
      "links": {
        "self": "/v1/users/1"
      }
    },
    {
      "id": 2,
      "name": "李四",
      "email": "lisi@example.com",
      "links": {
        "self": "/v1/users/2"
      }
    }
  ],
  "pagination": {
    "total": 2,
    "page": 1,
    "per_page": 20
  },
  "links": {
    "self": "/v1/users?page=1",
    "next": "/v1/users?page=2"
  }
}
```

### 4.2 创建用户

**请求**:

```
POST /v1/users HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "王五",
  "email": "wangwu@example.com",
  "password": "securepassword"
}
```

**响应**:

```
HTTP/1.1 201 Created
Content-Type: application/json
Location: /v1/users/3

{
  "data": {
    "id": 3,
    "name": "王五",
    "email": "wangwu@example.com",
    "links": {
      "self": "/v1/users/3"
    }
  }
}
```

### 4.3 更新用户

**请求**:

```
PATCH /v1/users/3 HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "王五(更新)"
}
```

**响应**:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": {
    "id": 3,
    "name": "王五(更新)",
    "email": "wangwu@example.com",
    "links": {
      "self": "/v1/users/3"
    }
  }
}
```

## 5. 最佳实践

1. **使用HTTPS**：所有API请求都应通过HTTPS进行

2. **认证**：使用OAuth2.0或JWT进行认证

3. **分页**：对于可能返回大量数据的端点实现分页

4. 过滤、排序和字段选择：

   ```
   GET /v1/users?fields=name,email&sort=-created_at&status=active
   ```

5. **速率限制**：防止滥用API

6. **HATEOAS**：在响应中包含相关资源的链接

7. **文档**：提供清晰、完整的API文档

8. 错误处理：提供详细的错误信息

   ```
   {
     "error": {
       "code": "invalid_email",
       "message": "The provided email is invalid",
       "target": "email",
       "details": [
         {
           "code": "format_error",
           "message": "Email must be a valid email address"
         }
       ]
     }
   }
   ```

## 6. Richardson成熟度模型

RESTful API可以分为四个成熟度级别：

1. **Level 0 - The Swamp of POX**：使用HTTP作为传输协议，但所有请求都是POST
2. **Level 1 - Resources**：引入资源概念，不同URL对应不同资源
3. **Level 2 - HTTP Verbs**：正确使用HTTP方法(GET, POST, PUT, DELETE等)
4. **Level 3 - Hypermedia Controls**：响应中包含链接，指导客户端下一步操作

现代RESTful API通常至少达到Level 2，优秀的API会努力实现Level 3。

