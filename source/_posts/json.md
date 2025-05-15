---
title: json
date: 2025-05-15 21:39:40
categories: 
  - "编程理论"
tags:
  - "json"
description: |
    json简介
---


---

**1. JSON简介**
• 定义：JSON是一种轻量级的数据交换格式，易于人阅读和编写，也易于机器解析和生成。

• 特点：

  • 基于JavaScript的子集（ECMA-262标准）。

  • 完全独立于语言，但借鉴了C语言家族的习惯（如C、Java、Python等）。

  • 采用文本格式，支持嵌套结构。


---

**2. JSON的两种核心结构**
1. 对象（Object）  
   • 无序的“名称/值”对集合，用花括号 `{}` 包裹。  

   • 语法：`{"key1": value1, "key2": value2}`  

   • 键名必须是字符串（双引号包裹），值可以是任意JSON类型。


2. 数组（Array）  
   • 值的有序列表，用方括号 `[]` 包裹。  

   • 语法：`[value1, value2, ...]`  

   • 值之间用逗号分隔。


---

**3. JSON支持的数据类型**
• 字符串（String）：双引号包裹的Unicode字符，支持转义字符（如`\"`、`\n`）。

• 数值（Number）：整数或浮点数，不支持八进制/十六进制。

• 布尔值（Boolean）：`true` 或 `false`。

• 空值（Null）：`null`。

• 对象（Object）和数组（Array）：可嵌套使用。


---

**4. 语法规则**
• 对象语法：  

  ```json
  {
    "key": "value",
    "nested": { "child": 123 }
  }
  ```
• 数组语法：  

  ```json
  [1, "text", true, null]
  ```
• 空白字符：空格、制表符、换行符可自由添加以提高可读性。


---

**5. 语法图示**
• 文件通过图片展示了JSON的语法规则：

  • 对象：`{` → 键值对 → `}`。

  • 数组：`[` → 值列表 → `]`。

  • 字符串/数值/布尔值的详细格式。


---

**6. 相关资源**
• 官方标准：[ECMA-404 JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)。

• 多语言支持：列出了几乎所有编程语言的JSON库（如Python的`json`模块、Java的`Jackson`、C++的`RapidJSON`等）。

• 视频教程：提供了关于JSON和JSON标志的YouTube播放列表链接。


---

**7. 其他信息**
• 设计哲学：强调简洁性和跨语言兼容性。

• 与XML对比：JSON更轻量，更适合数据交换场景。


---

**总结**
JSON的核心是键值对和有序列表的组合，通过简单明确的语法实现跨平台数据交换。其广泛支持的语言库使其成为现代Web开发中最常用的数据格式之一。