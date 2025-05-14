---
title: python正则表达式处理信息
date: 2025-05-14 09:17:17
categories: 
  - "编程实战"
tags:
  - "python" 
  - "正则表达式"
  - "数据处理"
description: |
    正则表达式(Regular Expression)是Python中强大的文本处理工具，可以用来从字符串中提取特定模式的信息。
---


# 正则表达式基本语法详解

正则表达式(Regular Expression)是一种强大的文本模式匹配工具，下面将详细介绍其基本语法和常用元字符。

## 1. 基本匹配

- **字面字符**：大多数字符（字母、数字）直接匹配自身
  - `a` 匹配字符 "a"
  - `1` 匹配数字 "1"
- **特殊字符**（需要转义）：`. ^ $ * + ? { } [ ] \ | ( )`
  - 要匹配这些字符本身，需要加反斜杠转义，如 `\.` 匹配点号

## 2. 常用元字符

| 元字符 | 描述                                                      |
| ------ | --------------------------------------------------------- |
| `.`    | 匹配任意单个字符（除了换行符）                            |
| `\d`   | 匹配数字，等价于 `[0-9]`                                  |
| `\D`   | 匹配非数字，等价于 `[^0-9]`                               |
| `\w`   | 匹配单词字符（字母、数字、下划线），等价于 `[a-zA-Z0-9_]` |
| `\W`   | 匹配非单词字符                                            |
| `\s`   | 匹配空白字符（空格、制表符、换行符等）                    |
| `\S`   | 匹配非空白字符                                            |
| `\b`   | 匹配单词边界                                              |
| `\B`   | 匹配非单词边界                                            |

## 3. 字符类 `[]`

- `[abc]` 匹配 "a"、"b" 或 "c"
- `[a-z]` 匹配任何小写字母
- `[0-9]` 匹配任何数字
- `[^abc]` 匹配**不是** "a"、"b" 或 "c" 的任何字符

## 4. 量词（重复）

| 量词    | 描述                                   |
| ------- | -------------------------------------- |
| `*`     | 匹配前一个元素零次或多次               |
| `+`     | 匹配前一个元素一次或多次               |
| `?`     | 匹配前一个元素零次或一次               |
| `{n}`   | 匹配前一个元素恰好 n 次                |
| `{n,}`  | 匹配前一个元素至少 n 次                |
| `{n,m}` | 匹配前一个元素至少 n 次，但不超过 m 次 |

## 5. 位置锚点

| 锚点 | 描述                                   |
| ---- | -------------------------------------- |
| `^`  | 匹配字符串的开头（多行模式下匹配行首） |
| `$`  | 匹配字符串的结尾（多行模式下匹配行尾） |

## 6. 分组与捕获 `()`

- `(abc)` 将多个字符组合为一个单元，并可捕获匹配的文本
- `(?:abc)` 非捕获分组，只分组不捕获

## 7. 或操作 `|`

- `a|b` 匹配 "a" 或 "b"

## 8. 转义字符 `\`

- `\.` 匹配字面点号
- `\\` 匹配反斜杠
- `\n` 匹配换行符
- `\t` 匹配制表符

## 示例应用

```
import re

# 匹配日期格式 YYYY-MM-DD
date_pattern = r'\d{4}-\d{2}-\d{2}'
text = "日期：2023-05-20，另一个日期：2024-01-15"
dates = re.findall(date_pattern, text)  # ['2023-05-20', '2024-01-15']

# 匹配邮箱地址
email_pattern = r'[\w.-]+@[\w.-]+\.\w+'
emails = re.findall(email_pattern, "联系我：user@example.com 或 support@test.org")

# 提取HTML标签内容
html = "<div>内容1</div><p>内容2</p>"
contents = re.findall(r'<[^>]+>(.*?)</[^>]+>', html)  # ['内容1', '内容2']
```

## 9. 修饰符（标志）

| 修饰符                    | 描述                                         |
| ------------------------- | -------------------------------------------- |
| `re.I` 或 `re.IGNORECASE` | 忽略大小写                                   |
| `re.M` 或 `re.MULTILINE`  | 多行模式，使 `^` 和 `$` 匹配每行的开头和结尾 |
| `re.S` 或 `re.DOTALL`     | 使 `.` 匹配包括换行符在内的所有字符          |

```
# 使用修饰符
text = "Python is great\nPYTHON is powerful"
matches = re.findall(r'^python', text, re.I | re.M)  # ['Python', 'PYTHON']
```

## 10.示例使用

### 提取html内容

```python
import re

html = """
<div class="content">
    <h1>标题</h1>
    <p>第一段内容</p>
    <p class="special">特殊段落</p>
</div>
"""

# 提取所有段落内容
paragraphs = re.findall(r'<p.*?>(.*?)</p>', html)
print("段落内容:", paragraphs)  # ['第一段内容', '特殊段落']

# 提取带class的标签内容
special_content = re.findall(r'<p\s+class=".*?">(.*?)</p>', html)
print("特殊段落:", special_content)  # ['特殊段落']

```

### 提取日志信息

```python
log_data = """
192.168.1.1 - - [10/Oct/2023:13:55:36 +0800] "GET /index.html"
10.0.0.2 - - [10/Oct/2023:13:56:12 +0800] "POST /login"
"""

# 提取IP和完整时间
matches = re.findall(r'(\d+\.\d+\.\d+\.\d+).*?$$(.*?)$$', log_data)
for ip, timestamp in matches:
    print(f"IP: {ip}, 时间: {timestamp}")

# 提取日期和时间部分
date_times = re.findall(r'\[(\d{2}/\w+/\d{4}):(\d{2}:\d{2}:\d{2})', log_data)
for date, time in date_times:
    print(f"日期: {date}, 时间: {time}")
```

### 提取中文和标点符号

```python
text = "Python是一种面向对象的解释型计算机程序设计语言，由Guido van Rossum于1989年发明。"

# 提取所有中文字符
chinese_chars = re.findall(r'[\u4e00-\u9fa5]', text)
print("中文字符:", chinese_chars)

# 提取中文段落（包含标点）
chinese_passage = re.findall(r'[\u4e00-\u9fa5，。、；：？！""''（）【】]+', text)
print("中文段落:", chinese_passage)

# 提取中英文混合的专有名词
mixed_terms = re.findall(r'[a-zA-Z]+（[\u4e00-\u9fa5]+）', text)
print("混合术语:", mixed_terms)  # ['Python']
```

