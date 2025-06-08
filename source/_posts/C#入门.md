---
title: C#入门
date: 2025-05-26 10:49:52
categories: 
  - "编程实战"
tags:
  - "C#"
  - "编程语言"
description: |
    总结C#官方文档
---


## C# 入门手册：从零开始，实战提升

### 章节一：C# 简介与开发环境搭建

#### 1.1 什么是 C#？

C#（读作 "C Sharp"）是由微软开发的一种现代的、面向对象的编程语言。它构建在 .NET 框架之上，广泛应用于：

- **Windows 桌面应用程序：** 使用 WPF (Windows Presentation Foundation) 或 WinForms (Windows Forms) 创建图形用户界面应用。
- **Web 应用程序：** 使用 ASP.NET Core 构建强大的网站和 Web API。
- **游戏开发：** 使用 Unity 引擎开发跨平台游戏。
- **移动应用程序：** 使用 Xamarin 或 .NET MAUI 开发 iOS 和 Android 应用。
- **云计算：** 在 Azure 等云平台上开发服务。
- **数据科学与机器学习：** 结合 ML.NET 等库进行数据分析和模型训练。

C# 语言的特点包括：

- **简单易学：** 语法结构清晰，与 C++ 和 Java 相似。
- **面向对象：** 支持封装、继承、多态等面向对象特性。
- **类型安全：** 在编译时检查类型，减少运行时错误。
- **垃圾回收：** 自动管理内存，无需手动释放。
- **强大的类库：** .NET 框架提供了丰富的类库，可以方便地实现各种功能。

#### 1.2 开发环境搭建

要开始C#编程，你需要安装 Visual Studio。Visual Studio 是微软官方提供的一款强大的集成开发环境 (IDE)，它集成了代码编辑器、编译器、调试器等工具。

**步骤：**

1. **下载 Visual Studio Community 版本：** 这是免费的，适用于个人开发者、学生和开源贡献者。访问 Visual Studio 官网下载：https://visualstudio.microsoft.com/zh-hans/downloads/

2. **运行安装程序：** 启动下载的安装程序。

3. 选择工作负载：

    在安装过程中，你会看到“工作负载”选项。根据你的需求选择：

   - **".NET 桌面开发"：** 如果你打算开发桌面应用。
   - **"ASP.NET 和 Web 开发"：** 如果你打算开发 Web 应用。
   - **"使用 Unity 的游戏开发"：** 如果你打算开发游戏。
   - **".NET 多平台应用 UI 开发"：** 如果你打算开发移动应用（Xamarin/.NET MAUI）。
   - 通常，选择 **".NET 桌面开发"** 和 **"ASP.NET 和 Web 开发"** 会覆盖大部分入门需求。

4. **安装：** 点击安装按钮，等待安装完成。

安装完成后，你就可以启动 Visual Studio 并开始你的C#编程之旅了！

#### 1.3 你的第一个 C# 程序：Hello World

让我们从最经典的“Hello World”程序开始。

**操作步骤：**

1. 打开 Visual Studio。
2. 点击 **“创建新项目”**。
3. 在模板列表中搜索 **“控制台应用”** (Console App)，并选择 C# 版本的控制台应用。
4. 点击 **“下一步”**。
5. 输入项目名称（例如：`HelloWorld`），选择项目存放位置。
6. 点击 **“创建”**。

Visual Studio 会为你自动生成一个基本的项目结构，其中包含一个 `Program.cs` 文件。

**`Program.cs` 文件内容：**

C#

```
// Program.cs

using System; // 引入 System 命名空间，包含了 Console 类

namespace HelloWorld // 命名空间，组织代码
{
    class Program // 类，所有代码都写在类中
    {
        static void Main(string[] args) // Main 方法是程序的入口点
        {
            Console.WriteLine("Hello World!"); // 打印 "Hello World!" 到控制台
            Console.ReadKey(); // 等待用户按下任意键，避免程序立即关闭
        }
    }
}
```

**代码解析：**

- `using System;`: 这行代码引入了 `System` 命名空间。`System` 命名空间是 .NET 框架中最基本的命名空间之一，它包含了许多常用的类和功能，例如 `Console` 类，用于控制台输入输出。

- `namespace HelloWorld`: `namespace` 用于组织代码。它有助于避免命名冲突，并提供一种逻辑上的分组方式。在这个例子中，`HelloWorld` 是我们程序的命名空间。

- `class Program`: 在 C# 中，所有的代码都必须在一个类 (class) 中。`Program` 是我们创建的一个类。类是面向对象编程的基本构建块，它封装了数据和行为。

- ```
  static void Main(string[] args)
  ```

  : 这是 C# 程序的入口点。当程序启动时，

  ```
  Main
  ```

   方法会被自动执行。

  - `static`: 表示这个方法是静态的，可以直接通过类名调用，无需创建类的实例。
  - `void`: 表示这个方法不返回任何值。
  - `Main`: 方法的名称，C# 程序的入口点必须是 `Main`。
  - `string[] args`: 这是一个可选的参数，用于接收命令行参数。

- `Console.WriteLine("Hello World!");`: `Console` 是 `System` 命名空间中的一个类，它提供了与控制台交互的方法。`WriteLine` 是 `Console` 类的一个静态方法，用于将文本输出到控制台，并在末尾添加一个换行符。

- `Console.ReadKey();`: 这个方法的作用是让程序在执行完毕后等待用户按下任意键，避免控制台窗口一闪而过。在实际的控制台应用中，这通常用于查看输出结果。

**运行程序：**

在 Visual Studio 中，你可以点击工具栏上的绿色“启动”按钮（通常是“IIS Express”或“本地 Windows 调试器”旁边），或者按下 `F5` 键来运行程序。

你会在控制台窗口中看到输出：

```
Hello World!
```

------

### 章节二：C# 基础语法

本章将介绍 C# 的基本语法元素，包括变量、数据类型、运算符、控制流等。

#### 2.1 变量与数据类型

**变量**用于存储数据。在使用变量之前，你需要声明它的类型，并可以给它一个初始值。

**C# 常用数据类型：**

| 类型      | 描述                                    | 示例                         |
| --------- | --------------------------------------- | ---------------------------- |
| `int`     | 整数（例如：10, -5）                    | `int age = 30;`              |
| `double`  | 双精度浮点数（例如：3.14, 0.001）       | `double pi = 3.14159;`       |
| `float`   | 单精度浮点数（需要f后缀，例如：3.14f）  | `float temperature = 25.5f;` |
| `decimal` | 用于高精度计算（例如：货币，需要m后缀） | `decimal price = 99.99m;`    |
| `bool`    | 布尔值（`true` 或 `false`）             | `bool isStudent = true;`     |
| `char`    | 单个字符（用单引号）                    | `char initial = 'J';`        |
| `string`  | 字符串（用双引号）                      | `string name = "Alice";`     |

导出到 Google 表格

**示例代码：**

C#

```
using System;

namespace VariablesAndDataTypes
{
    class Program
    {
        static void Main(string[] args)
        {
            // 声明并初始化不同类型的变量
            int age = 25; // 整数
            double height = 1.75; // 双精度浮点数
            float weight = 70.5f; // 单精度浮点数，注意f后缀
            decimal salary = 5000.00m; // 高精度浮点数，注意m后缀
            bool isEmployed = true; // 布尔值
            char grade = 'A'; // 字符
            string firstName = "John"; // 字符串
            string lastName = "Doe";

            // 输出变量的值
            Console.WriteLine($"姓名: {firstName} {lastName}");
            Console.WriteLine($"年龄: {age}");
            Console.WriteLine($"身高: {height} 米");
            Console.WriteLine($"体重: {weight} 公斤");
            Console.WriteLine($"月薪: {salary} 元");
            Console.WriteLine($"是否在职: {isEmployed}");
            Console.WriteLine($"成绩等级: {grade}");

            // 变量的重新赋值
            age = 26;
            Console.WriteLine($"新年龄: {age}");

            // 字符串拼接
            string fullName = firstName + " " + lastName;
            Console.WriteLine($"全名: {fullName}");

            // 字符串插值 (C# 6.0 引入，更简洁)
            string message = $"Hello, {firstName}! 你的年龄是 {age} 岁。";
            Console.WriteLine(message);

            Console.ReadKey();
        }
    }
}
```

**注意：**

- 变量名通常遵循 **camelCase** 命名约定（第一个单词小写，后续单词首字母大写，例如 `firstName`）。
- C# 是强类型语言，这意味着你必须在声明变量时指定其类型，并且该变量只能存储该类型的值。
- `$""` 是字符串插值语法，它允许你在字符串中嵌入表达式，使得字符串拼接更加方便和可读。

#### 2.2 常量

**常量**是其值在程序执行期间不能更改的变量。使用 `const` 关键字声明常量。

**示例代码：**

C#

```
using System;

namespace ConstantsExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 声明常量，通常用大写字母和下划线命名（约定）
            const double PI = 3.14159;
            const int MAX_USERS = 1000;
            const string COMPANY_NAME = "MyAwesomeCorp";

            Console.WriteLine($"圆周率: {PI}");
            Console.WriteLine($"最大用户数: {MAX_USERS}");
            Console.WriteLine($"公司名称: {COMPANY_NAME}");

            // 尝试修改常量会引发编译错误
            // PI = 3.14; // 这会报错！

            Console.ReadKey();
        }
    }
}
```

#### 2.3 运算符

C# 提供了丰富的运算符，用于执行各种操作。

**2.3.1 算术运算符：**

| 运算符 | 描述 | 示例           |
| ------ | ---- | -------------- |
| `+`    | 加法 | `a + b`        |
| `-`    | 减法 | `a - b`        |
| `*`    | 乘法 | `a * b`        |
| `/`    | 除法 | `a / b`        |
| `%`    | 取模 | `a % b` (余数) |

导出到 Google 表格

**示例代码：**

C#

```
using System;

namespace ArithmeticOperators
{
    class Program
    {
        static void Main(string[] args)
        {
            int a = 10;
            int b = 3;

            Console.WriteLine($"a + b = {a + b}"); // 13
            Console.WriteLine($"a - b = {a - b}"); // 7
            Console.WriteLine($"a * b = {a * b}"); // 30
            Console.WriteLine($"a / b = {a / b}"); // 3 (整数除法，小数部分截断)
            Console.WriteLine($"a % b = {a % b}"); // 1 (10 除以 3 的余数)

            double x = 10.0;
            double y = 3.0;
            Console.WriteLine($"x / y = {x / y}"); // 3.3333333333333335 (浮点数除法)

            Console.ReadKey();
        }
    }
}
```

**2.3.2 关系运算符（比较运算符）：**

| 运算符 | 描述     | 示例     |
| ------ | -------- | -------- |
| `==`   | 等于     | `a == b` |
| `!=`   | 不等于   | `a != b` |
| `>`    | 大于     | `a > b`  |
| `<`    | 小于     | `a < b`  |
| `>=`   | 大于等于 | `a >= b` |
| `<=`   | 小于等于 | `a <= b` |

导出到 Google 表格

**示例代码：**

C#

```
using System;

namespace RelationalOperators
{
    class Program
    {
        static void Main(string[] args)
        {
            int num1 = 10;
            int num2 = 20;

            Console.WriteLine($"num1 == num2: {num1 == num2}"); // False
            Console.WriteLine($"num1 != num2: {num1 != num2}"); // True
            Console.WriteLine($"num1 > num2: {num1 > num2}");   // False
            Console.WriteLine($"num1 < num2: {num1 < num2}");   // True
            Console.WriteLine($"num1 >= 10: {num1 >= 10}");     // True
            Console.WriteLine($"num2 <= 20: {num2 <= 20}");     // True

            Console.ReadKey();
        }
    }
}
```

**2.3.3 逻辑运算符：**

| 运算符 | 描述   | 示例                       |
| ------ | ------ | -------------------------- |
| `&&`   | 逻辑与 | `condition1 && condition2` |
| `      | `      | 逻辑或                     |
| `!`    | 逻辑非 | `!condition`               |

导出到 Google 表格

**示例代码：**

C#

```
using System;

namespace LogicalOperators
{
    class Program
    {
        static void Main(string[] args)
        {
            bool isSunny = true;
            bool isWarm = false;
            int age = 18;
            bool hasLicense = true;

            // 逻辑与 (&&)：两个条件都为真才为真
            Console.WriteLine($"isSunny && isWarm: {isSunny && isWarm}"); // False

            // 逻辑或 (||)：只要一个条件为真就为真
            Console.WriteLine($"isSunny || isWarm: {isSunny || isWarm}"); // True

            // 逻辑非 (!)：取反
            Console.WriteLine($"!isSunny: {!isSunny}"); // False

            // 组合使用
            bool canDrive = (age >= 18) && hasLicense;
            Console.WriteLine($"Can drive: {canDrive}"); // True

            Console.ReadKey();
        }
    }
}
```

**2.3.4 赋值运算符：**

| 运算符 | 描述   | 示例     | 等价于      |
| ------ | ------ | -------- | ----------- |
| `=`    | 赋值   | `x = 5`  |             |
| `+=`   | 加等于 | `x += 2` | `x = x + 2` |
| `-=`   | 减等于 | `x -= 2` | `x = x - 2` |
| `*=`   | 乘等于 | `x *= 2` | `x = x * 2` |
| `/=`   | 除等于 | `x /= 2` | `x = x / 2` |
| `%=`   | 模等于 | `x %= 2` | `x = x % 2` |

导出到 Google 表格

**示例代码：**

C#

```
using System;

namespace AssignmentOperators
{
    class Program
    {
        static void Main(string[] args)
        {
            int num = 10;
            Console.WriteLine($"初始值: {num}"); // 10

            num += 5; // num = num + 5
            Console.WriteLine($"num += 5: {num}"); // 15

            num -= 3; // num = num - 3
            Console.WriteLine($"num -= 3: {num}"); // 12

            num *= 2; // num = num * 2
            Console.WriteLine($"num *= 2: {num}"); // 24

            num /= 4; // num = num / 4
            Console.WriteLine($"num /= 4: {num}"); // 6

            num %= 3; // num = num % 3
            Console.WriteLine($"num %= 3: {num}"); // 0

            Console.ReadKey();
        }
    }
}
```

#### 2.4 类型转换

在 C# 中，有时需要将一个数据类型的值转换为另一个数据类型。

**2.4.1 隐式转换 (Implicit Conversion)：**

当转换是安全的，不会导致数据丢失时，C# 会自动进行隐式转换。例如，将 `int` 转换为 `double`。

**示例代码：**

C#

```
using System;

namespace TypeConversion
{
    class Program
    {
        static void Main(string[] args)
        {
            int myInt = 100;
            double myDouble = myInt; // 隐式转换：int 到 double，安全
            Console.WriteLine($"Int to Double: {myDouble}"); // 100

            float myFloat = myInt; // 隐式转换：int 到 float，安全
            Console.WriteLine($"Int to Float: {myFloat}"); // 100

            Console.ReadKey();
        }
    }
}
```

**2.4.2 显式转换 (Explicit Conversion / Casting)：**

当转换可能导致数据丢失时，你需要使用显式转换（强制类型转换）。使用括号 `()` 来指定要转换的目标类型。

**示例代码：**

C#

```
using System;

namespace TypeConversion
{
    class Program
    {
        static void Main(string[] args)
        {
            double myDouble = 9.78;
            int myInt = (int)myDouble; // 显式转换：double 到 int，小数部分会被截断
            Console.WriteLine($"Double to Int: {myInt}"); // 9

            int num1 = 10;
            int num2 = 3;
            double result = (double)num1 / num2; // 先将num1转换为double，再进行浮点数除法
            Console.WriteLine($"Int division to Double: {result}"); // 3.3333333333333335

            Console.ReadKey();
        }
    }
}
```

**2.4.3 使用 `Convert` 类：**

`Convert` 类提供了多种方法，用于在不同数据类型之间进行转换，它更安全，并且可以处理一些边界情况（如字符串转换为数字）。

**示例代码：**

C#

```
using System;

namespace TypeConversion
{
    class Program
    {
        static void Main(string[] args)
        {
            string strNumber = "123";
            int number = Convert.ToInt32(strNumber); // 字符串转换为整数
            Console.WriteLine($"String to Int: {number}"); // 123

            string strDouble = "45.67";
            double dblNumber = Convert.ToDouble(strDouble); // 字符串转换为双精度浮点数
            Console.WriteLine($"String to Double: {dblNumber}"); // 45.67

            int value = 200;
            string strValue = Convert.ToString(value); // 整数转换为字符串
            Console.WriteLine($"Int to String: {strValue}"); // "200"

            // 尝试转换非法字符串会导致异常
            string invalidString = "abc";
            try
            {
                int invalidNumber = Convert.ToInt32(invalidString);
            }
            catch (FormatException ex)
            {
                Console.WriteLine($"转换错误: {ex.Message}"); // Input string was not in a correct format.
            }

            Console.ReadKey();
        }
    }
}
```

**2.4.4 使用 `Parse` 或 `TryParse` 方法：**

对于字符串转换为数字类型，通常更推荐使用 `Parse` 或 `TryParse` 方法。

- `Parse`：如果转换失败会抛出 `FormatException` 异常。
- `TryParse`：如果转换失败会返回 `false`，不会抛出异常，更安全，适用于用户输入等不确定数据。

**示例代码：**

C#

```
using System;

namespace TypeConversion
{
    class Program
    {
        static void Main(string[] args)
        {
            string s1 = "100";
            int i1 = int.Parse(s1); // 成功转换
            Console.WriteLine($"Parse string to int: {i1}");

            string s2 = "abc";
            int i2;
            bool success = int.TryParse(s2, out i2); // 尝试转换，不会抛出异常
            if (success)
            {
                Console.WriteLine($"TryParse string to int: {i2}");
            }
            else
            {
                Console.WriteLine($"Failed to parse '{s2}' to int.");
            }

            Console.ReadKey();
        }
    }
}
```

#### 2.5 控制流语句

控制流语句允许你根据条件执行不同的代码块，或者重复执行某些代码。

**2.5.1 `if-else if-else` 语句：**

根据条件执行不同的代码块。

C#

```
using System;

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            int score = 85;

            if (score >= 90)
            {
                Console.WriteLine("A 级");
            }
            else if (score >= 80)
            {
                Console.WriteLine("B 级");
            }
            else if (score >= 70)
            {
                Console.WriteLine("C 级");
            }
            else
            {
                Console.WriteLine("D 级");
            }

            // 示例：判断奇偶数
            int number = 7;
            if (number % 2 == 0)
            {
                Console.WriteLine($"{number} 是偶数。");
            }
            else
            {
                Console.WriteLine($"{number} 是奇数。");
            }

            Console.ReadKey();
        }
    }
}
```

**2.5.2 `switch` 语句：**

当有多个可能的值需要判断时，`switch` 语句比多个 `if-else if` 更简洁。

C#

```
using System;

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            char grade = 'B';

            switch (grade)
            {
                case 'A':
                    Console.WriteLine("优秀！");
                    break; // break 关键字用于跳出 switch 语句
                case 'B':
                    Console.WriteLine("良好！");
                    break;
                case 'C':
                    Console.WriteLine("及格。");
                    break;
                case 'D':
                case 'F': // 多个 case 可以执行相同的代码块
                    Console.WriteLine("不及格。");
                    break;
                default: // 默认情况
                    Console.WriteLine("无效的成绩。");
                    break;
            }

            // 示例：判断星期几
            int dayOfWeek = 3; // 1代表周一，7代表周日

            switch (dayOfWeek)
            {
                case 1:
                    Console.WriteLine("星期一");
                    break;
                case 2:
                    Console.WriteLine("星期二");
                    break;
                case 3:
                    Console.WriteLine("星期三");
                    break;
                case 4:
                    Console.WriteLine("星期四");
                    break;
                case 5:
                    Console.WriteLine("星期五");
                    break;
                case 6:
                    Console.WriteLine("星期六");
                    break;
                case 7:
                    Console.WriteLine("星期日");
                    break;
                default:
                    Console.WriteLine("无效的日期");
                    break;
            }

            Console.ReadKey();
        }
    }
}
```

**2.5.3 `for` 循环：**

用于重复执行一段代码固定次数。

C#

```
using System;

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            // 打印从 0 到 4 的数字
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"for 循环: {i}");
            }

            Console.WriteLine("--------------------");

            // 打印偶数
            for (int i = 0; i <= 10; i += 2) // i += 2 等同于 i = i + 2
            {
                Console.WriteLine($"偶数: {i}");
            }

            Console.WriteLine("--------------------");

            // 倒序打印
            for (int i = 5; i > 0; i--)
            {
                Console.WriteLine($"倒序: {i}");
            }

            Console.ReadKey();
        }
    }
}
```

**2.5.4 `while` 循环：**

只要条件为真，就重复执行一段代码。

C#

```
using System;

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            int count = 0;
            while (count < 5)
            {
                Console.WriteLine($"while 循环: {count}");
                count++; // 每次循环增加 count 的值，否则会无限循环
            }

            Console.WriteLine("--------------------");

            // 示例：用户输入直到输入“quit”
            string input = "";
            while (input != "quit")
            {
                Console.Write("请输入一个单词 (输入 'quit' 退出): ");
                input = Console.ReadLine(); // 从控制台读取一行输入
                Console.WriteLine($"你输入了: {input}");
            }

            Console.ReadKey();
        }
    }
}
```

**2.5.5 `do-while` 循环：**

`do-while` 循环至少执行一次，然后根据条件重复执行。

C#

```
using System;

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            int i = 0;
            do
            {
                Console.WriteLine($"do-while 循环: {i}");
                i++;
            } while (i < 5); // 即使 i 初始值不满足条件，do 块也会执行一次

            Console.WriteLine("--------------------");

            // 示例：强制用户输入一个正数
            int positiveNumber;
            do
            {
                Console.Write("请输入一个正数: ");
                string input = Console.ReadLine();
                // 尝试将用户输入转换为整数，如果转换失败或不是正数，则继续循环
                if (int.TryParse(input, out positiveNumber) && positiveNumber > 0)
                {
                    break; // 输入有效，跳出循环
                }
                else
                {
                    Console.WriteLine("输入无效，请重新输入一个正数。");
                }
            } while (true); // 无限循环，直到 break 跳出

            Console.WriteLine($"你输入的正数是: {positiveNumber}");

            Console.ReadKey();
        }
    }
}
```

**2.5.6 `foreach` 循环：**

用于遍历集合中的每个元素，例如数组、列表。

C#

```
using System;
using System.Collections.Generic; // 引入 List 需要此命名空间

namespace ControlFlow
{
    class Program
    {
        static void Main(string[] args)
        {
            string[] names = { "Alice", "Bob", "Charlie" };

            Console.WriteLine("遍历数组:");
            foreach (string name in names)
            {
                Console.WriteLine(name);
            }

            Console.WriteLine("--------------------");

            List<int> numbers = new List<int> { 10, 20, 30, 40, 50 };

            Console.WriteLine("遍历列表:");
            foreach (int num in numbers)
            {
                Console.WriteLine(num);
            }

            Console.ReadKey();
        }
    }
}
```

------

### 章节三：数组和集合

本章将介绍 C# 中用于存储多个数据的结构：数组和常用的集合类型。

#### 3.1 数组 (Arrays)

**数组**是相同类型的数据的固定大小的有序集合。

**声明和初始化数组：**

C#

```
using System;

namespace ArraysAndCollections
{
    class Program
    {
        static void Main(string[] args)
        {
            // 声明一个整数数组，大小为 5
            int[] numbers = new int[5]; // 默认值为 0

            // 初始化数组元素
            numbers[0] = 10;
            numbers[1] = 20;
            numbers[2] = 30;
            numbers[3] = 40;
            numbers[4] = 50;

            // 访问数组元素
            Console.WriteLine($"第一个元素: {numbers[0]}"); // 10
            Console.WriteLine($"第三个元素: {numbers[2]}"); // 30

            // 声明并同时初始化数组
            string[] fruits = { "Apple", "Banana", "Cherry", "Date" };

            Console.WriteLine($"水果数组的长度: {fruits.Length}"); // 4

            // 遍历数组 (使用 for 循环)
            Console.WriteLine("使用 for 循环遍历水果:");
            for (int i = 0; i < fruits.Length; i++)
            {
                Console.WriteLine($"索引 {i}: {fruits[i]}");
            }

            Console.WriteLine("--------------------");

            // 遍历数组 (使用 foreach 循环，推荐)
            Console.WriteLine("使用 foreach 循环遍历水果:");
            foreach (string fruit in fruits)
            {
                Console.WriteLine(fruit);
            }

            // 多维数组（二维数组）
            int[,] matrix = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

            Console.WriteLine($"矩阵元素 (0,0): {matrix[0, 0]}"); // 1
            Console.WriteLine($"矩阵元素 (1,2): {matrix[1, 2]}"); // 6

            // 遍历二维数组
            Console.WriteLine("遍历二维数组:");
            for (int row = 0; row < matrix.GetLength(0); row++) // GetLength(0) 获取行数
            {
                for (int col = 0; col < matrix.GetLength(1); col++) // GetLength(1) 获取列数
                {
                    Console.Write($"{matrix[row, col]} ");
                }
                Console.WriteLine(); // 换行
            }

            Console.ReadKey();
        }
    }
}
```

#### 3.2 列表 (List&lt;T>)

`List<T>` 是一个泛型集合，它是一个动态大小的数组，比传统数组更灵活，可以方便地添加、删除和查找元素。`T` 是一个类型参数，表示列表中存储的元素类型。

要使用 `List<T>`，你需要引入 `System.Collections.Generic` 命名空间。

**示例代码：**

C#

```
using System;
using System.Collections.Generic; // 引入 List<T> 需要此命名空间

namespace ArraysAndCollections
{
    class Program
    {
        static void Main(string[] args)
        {
            // 声明并初始化一个整数列表
            List<int> scores = new List<int>();

            // 添加元素
            scores.Add(95);
            scores.Add(88);
            scores.Add(72);
            scores.Add(90);

            Console.WriteLine($"列表中的元素数量: {scores.Count}"); // 4

            // 访问元素 (通过索引)
            Console.WriteLine($"第一个分数: {scores[0]}"); // 95

            // 插入元素
            scores.Insert(1, 80); // 在索引 1 处插入 80
            Console.WriteLine("插入 80 后:");
            foreach (int score in scores)
            {
                Console.Write($"{score} "); // 95 80 88 72 90
            }
            Console.WriteLine();

            // 移除元素
            scores.Remove(72); // 移除值为 72 的第一个元素
            Console.WriteLine("移除 72 后:");
            foreach (int score in scores)
            {
                Console.Write($"{score} "); // 95 80 88 90
            }
            Console.WriteLine();

            scores.RemoveAt(0); // 移除索引 0 处的元素 (95)
            Console.WriteLine("移除索引 0 后:");
            foreach (int score in scores)
            {
                Console.Write($"{score} "); // 80 88 90
            }
            Console.WriteLine();

            // 检查元素是否存在
            bool contains90 = scores.Contains(90);
            Console.WriteLine($"列表中是否包含 90: {contains90}"); // True

            // 清空列表
            scores.Clear();
            Console.WriteLine($"清空后元素数量: {scores.Count}"); // 0

            // 声明并初始化一个字符串列表
            List<string> colors = new List<string> { "Red", "Green", "Blue" };
            Console.WriteLine("颜色列表:");
            foreach (string color in colors)
            {
                Console.WriteLine(color);
            }

            Console.ReadKey();
        }
    }
}
```

#### 3.3 字典 (Dictionary&lt;TKey, TValue>)

`Dictionary<TKey, TValue>` 是一种键值对集合，其中每个键都必须是唯一的。它提供了一种快速查找数据的方式，通过键来检索对应的值。

要使用 `Dictionary<TKey, TValue>`，你需要引入 `System.Collections.Generic` 命名空间。

**示例代码：**

C#

```
using System;
using System.Collections.Generic; // 引入 Dictionary<TKey, TValue> 需要此命名空间

namespace ArraysAndCollections
{
    class Program
    {
        static void Main(string[] args)
        {
            // 声明并初始化一个字典，键为 string，值为 int
            Dictionary<string, int> ages = new Dictionary<string, int>();

            // 添加键值对
            ages.Add("Alice", 30);
            ages.Add("Bob", 25);
            ages.Add("Charlie", 35);

            // 另一种添加方式 (推荐，如果键已存在会更新值)
            ages["David"] = 28;

            // 访问值 (通过键)
            Console.WriteLine($"Alice 的年龄: {ages["Alice"]}"); // 30

            // 检查键是否存在
            if (ages.ContainsKey("Bob"))
            {
                Console.WriteLine($"Bob 的年龄: {ages["Bob"]}");
            }
            else
            {
                Console.WriteLine("字典中不包含 Bob。");
            }

            // 安全地获取值 (TryGetValue)
            int charlieAge;
            if (ages.TryGetValue("Charlie", out charlieAge))
            {
                Console.WriteLine($"Charlie 的年龄 (TryGetValue): {charlieAge}");
            }
            else
            {
                Console.WriteLine("字典中不包含 Charlie。");
            }

            // 遍历字典 (遍历键值对)
            Console.WriteLine("遍历字典:");
            foreach (KeyValuePair<string, int> entry in ages)
            {
                Console.WriteLine($"姓名: {entry.Key}, 年龄: {entry.Value}");
            }

            Console.WriteLine("--------------------");

            // 遍历字典 (只遍历键)
            Console.WriteLine("只遍历键:");
            foreach (string name in ages.Keys)
            {
                Console.WriteLine($"姓名: {name}");
            }

            Console.WriteLine("--------------------");

            // 遍历字典 (只遍历值)
            Console.WriteLine("只遍历值:");
            foreach (int age in ages.Values)
            {
                Console.WriteLine($"年龄: {age}");
            }

            // 移除键值对
            ages.Remove("Bob");
            Console.WriteLine($"移除 Bob 后，字典中的元素数量: {ages.Count}"); // 3

            Console.ReadKey();
        }
    }
}
```

------

### 章节四：方法 (Methods)

**方法**是包含一系列语句的代码块，用于执行特定任务。使用方法可以提高代码的重用性、可读性和模块化。

#### 4.1 声明和调用方法

方法的声明包括：访问修饰符、返回类型、方法名、参数列表。

C#

```
using System;

namespace MethodsExample
{
    class Program
    {
        // 1. 无参数无返回值的方法
        static void SayHello()
        {
            Console.WriteLine("你好，世界！");
        }

        // 2. 带参数无返回值的方法
        static void GreetUser(string name)
        {
            Console.WriteLine($"你好，{name}！");
        }

        // 3. 带参数有返回值的方法
        static int Add(int a, int b)
        {
            int sum = a + b;
            return sum; // 返回计算结果
        }

        // 4. 计算圆的面积的方法
        static double CalculateCircleArea(double radius)
        {
            return Math.PI * radius * radius;
        }

        // 5. 带有多个参数的方法
        static void PrintPersonInfo(string name, int age, string city)
        {
            Console.WriteLine($"姓名: {name}, 年龄: {age}, 城市: {city}");
        }

        static void Main(string[] args)
        {
            // 调用无参数无返回值的方法
            SayHello();

            // 调用带参数无返回值的方法
            GreetUser("张三");
            GreetUser("李四");

            // 调用带参数有返回值的方法
            int result = Add(10, 20);
            Console.WriteLine($"10 + 20 = {result}");

            int x = 5;
            int y = 7;
            int sumXY = Add(x, y);
            Console.WriteLine($"{x} + {y} = {sumXY}");

            // 调用计算圆面积的方法
            double circleRadius = 5.0;
            double area = CalculateCircleArea(circleRadius);
            Console.WriteLine($"半径为 {circleRadius} 的圆的面积是: {area:F2}"); // F2 格式化为两位小数

            // 调用带有多个参数的方法
            PrintPersonInfo("王五", 30, "北京");

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `static`: 表示该方法属于类本身，而不是类的某个实例。在 `Main` 方法中调用其他方法时，通常需要将它们声明为 `static`。
- `void`: 表示方法不返回任何值。如果方法需要返回一个值，你需要指定返回值的类型（例如 `int`, `double`, `string` 等）。
- `string name`: `name` 是方法的参数，它的类型是 `string`。
- `return sum;`: `return` 语句用于从方法中返回一个值。

#### 4.2 参数传递

C# 中方法的参数传递主要有两种方式：值传递和引用传递。

**4.2.1 值传递 (Value Parameters)：**

默认情况下，C# 使用值传递。这意味着当一个变量作为参数传递给方法时，实际上是传递了该变量的一个副本。方法内部对参数的修改不会影响原始变量。

C#

```
using System;

namespace MethodsExample
{
    class Program
    {
        static void ChangeValue(int num)
        {
            num = num + 10; // 这里修改的是 num 的副本
            Console.WriteLine($"方法内部的 num: {num}");
        }

        static void Main(string[] args)
        {
            int myNumber = 5;
            Console.WriteLine($"方法调用前的 myNumber: {myNumber}"); // 5

            ChangeValue(myNumber); // 传递的是 myNumber 的值
            Console.WriteLine($"方法调用后的 myNumber: {myNumber}"); // 5 (未改变)

            Console.ReadKey();
        }
    }
}
```

**4.2.2 引用传递 (Reference Parameters - `ref` 关键字)：**

使用 `ref` 关键字可以将参数通过引用传递。这意味着方法操作的是原始变量的内存地址，因此方法内部对参数的修改会影响原始变量。

**注意：** 使用 `ref` 关键字时，参数在传递前必须已被初始化。

C#

```
using System;

namespace MethodsExample
{
    class Program
    {
        static void ChangeReference(ref int num) // 使用 ref 关键字
        {
            num = num + 10; // 这里修改的是原始变量
            Console.WriteLine($"方法内部的 num: {num}");
        }

        static void Main(string[] args)
        {
            int myNumber = 5;
            Console.WriteLine($"方法调用前的 myNumber: {myNumber}"); // 5

            ChangeReference(ref myNumber); // 传递的是 myNumber 的引用
            Console.WriteLine($"方法调用后的 myNumber: {myNumber}"); // 15 (已改变)

            Console.ReadKey();
        }
    }
}
```

**4.2.3 输出参数 (Output Parameters - `out` 关键字)：**

使用 `out` 关键字可以将参数作为输出参数传递。这意味着方法可以在不使用 `return` 语句的情况下返回多个值。

**注意：** 使用 `out` 关键字时，参数在方法内部必须被赋值，且在传递前可以不被初始化。

C#

```
using System;

namespace MethodsExample
{
    class Program
    {
        static void GetMinMax(int[] numbers, out int min, out int max)
        {
            min = numbers[0]; // 必须在方法内部为 out 参数赋值
            max = numbers[0];

            foreach (int num in numbers)
            {
                if (num < min)
                {
                    min = num;
                }
                if (num > max)
                {
                    max = num;
                }
            }
        }

        static void Main(string[] args)
        {
            int[] data = { 10, 5, 20, 8, 15 };
            int minimum; // 无需初始化
            int maximum; // 无需初始化

            GetMinMax(data, out minimum, out maximum);

            Console.WriteLine($"最小值: {minimum}"); // 5
            Console.WriteLine($"最大值: {maximum}"); // 20

            // 示例：TryParse 就是一个典型的 out 参数应用
            string strNum = "123";
            int parsedNum;
            bool success = int.TryParse(strNum, out parsedNum);
            if (success)
            {
                Console.WriteLine($"解析成功: {parsedNum}");
            }

            Console.ReadKey();
        }
    }
}
```

#### 4.3 方法重载 (Method Overloading)

**方法重载**允许在同一个类中定义多个同名的方法，但它们的参数列表必须不同（参数的数量、类型或顺序不同）。编译器会根据调用时提供的参数类型和数量来决定调用哪个重载方法。

C#

```
using System;

namespace MethodsExample
{
    class Program
    {
        // 加法方法 1：两个整数相加
        static int Add(int a, int b)
        {
            Console.WriteLine("调用了 Add(int, int)");
            return a + b;
        }

        // 加法方法 2：三个整数相加
        static int Add(int a, int b, int c)
        {
            Console.WriteLine("调用了 Add(int, int, int)");
            return a + b + c;
        }

        // 加法方法 3：两个双精度浮点数相加
        static double Add(double a, double b)
        {
            Console.WriteLine("调用了 Add(double, double)");
            return a + b;
        }

        // 连接字符串
        static string Concatenate(string s1, string s2)
        {
            Console.WriteLine("调用了 Concatenate(string, string)");
            return s1 + s2;
        }

        // 连接三个字符串
        static string Concatenate(string s1, string s2, string s3)
        {
            Console.WriteLine("调用了 Concatenate(string, string, string)");
            return s1 + s2 + s3;
        }

        static void Main(string[] args)
        {
            Console.WriteLine($"Add(10, 20): {Add(10, 20)}"); // 调用 Add(int, int)
            Console.WriteLine($"Add(10, 20, 30): {Add(10, 20, 30)}"); // 调用 Add(int, int, int)
            Console.WriteLine($"Add(10.5, 20.3): {Add(10.5, 20.3)}"); // 调用 Add(double, double)

            Console.WriteLine($"Concatenate('Hello', 'World'): {Concatenate("Hello", "World")}");
            Console.WriteLine($"Concatenate('C#', 'is', 'fun'): {Concatenate("C#", " is", " fun!")}");

            Console.ReadKey();
        }
    }
}
```

------

### 章节五：面向对象编程 (OOP) 基础

C# 是一种面向对象的语言。面向对象编程 (OOP) 是一种编程范式，它将程序中的实体建模为“对象”，每个对象都包含数据（属性）和行为（方法）。

OOP 的四大核心原则：

- **封装 (Encapsulation)：** 将数据和操作数据的方法捆绑在一起，并对外部隐藏内部实现细节。
- **继承 (Inheritance)：** 允许一个类（子类）继承另一个类（父类）的属性和方法，从而实现代码重用。
- **多态 (Polymorphism)：** 允许不同类的对象对同一个消息做出不同的响应（例如，父类引用指向子类对象）。
- **抽象 (Abstraction)：** 隐藏复杂的实现细节，只向用户暴露必要的功能。

#### 5.1 类 (Class) 和对象 (Object)

- **类 (Class)：** 是创建对象的蓝图或模板。它定义了对象的属性（数据）和行为（方法）。
- **对象 (Object)：** 是类的实例。当你创建一个类的对象时，你就在内存中分配了该类定义的属性和方法。

**示例代码：**

C#

```
using System;

namespace OOP
{
    // 定义一个 Person 类
    class Person
    {
        // 属性 (Properties)
        public string Name { get; set; } // 自动实现的属性，包含 get 和 set 访问器
        public int Age { get; set; }
        public string City { get; set; }

        // 构造函数 (Constructor)
        // 构造函数是一个特殊的方法，在创建对象时被调用，用于初始化对象的属性
        public Person(string name, int age, string city)
        {
            Name = name;
            Age = age;
            City = city;
            Console.WriteLine($"创建了一个新的 Person 对象: {Name}");
        }

        // 方法 (Methods)
        public void Introduce()
        {
            Console.WriteLine($"你好，我叫 {Name}，我今年 {Age} 岁，来自 {City}。");
        }

        public void CelebrateBirthday()
        {
            Age++;
            Console.WriteLine($"{Name} 庆祝了生日，现在 {Age} 岁了！");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 创建 Person 类的对象 (实例化)
            Person person1 = new Person("张三", 30, "北京");
            Person person2 = new Person("李四", 25, "上海");

            // 访问对象的属性
            Console.WriteLine($"Person1 的名字: {person1.Name}");
            Console.WriteLine($"Person2 的年龄: {person2.Age}");

            // 调用对象的方法
            person1.Introduce();
            person2.Introduce();

            person1.CelebrateBirthday(); // 张三的年龄变为 31
            person1.Introduce();

            // 尝试创建另一个 Person 对象，但没有指定所有参数 (会报错，因为没有匹配的构造函数)
            // Person person3 = new Person("王五"); // 编译错误

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `public string Name { get; set; }`: 这是一种 C# 属性的简写语法，称为“自动实现的属性”。它会自动创建私有字段来存储数据，并提供公共的 `get`（读取）和 `set`（写入）访问器。
- `public Person(string name, int age, string city)`: 这是 `Person` 类的构造函数。它的名称与类名相同，没有返回类型。当使用 `new Person(...)` 创建对象时，构造函数会被调用。
- `this.Name = name;`（在此示例中直接 `Name = name;` 也可以，因为参数名与属性名不同）：在构造函数中，`name` 是传入的参数，`Name` 是类的属性。`this` 关键字可以用于区分同名的参数和属性，尽管在本例中不是必需的。

#### 5.2 访问修饰符 (Access Modifiers)

访问修饰符控制类、成员（属性、方法、字段）的可访问性。

- `public`: 成员可以从任何地方访问。
- `private`: 成员只能在声明它们的类内部访问。这是默认的访问修饰符。
- `protected`: 成员可以在声明它们的类内部以及派生类（子类）内部访问。
- `internal`: 成员可以在同一程序集（通常是一个项目）中的任何代码中访问。
- `protected internal`: `protected` 和 `internal` 的组合。
- `private protected`: `private` 和 `protected` 的组合。

**示例代码：**

C#

```
using System;

namespace OOP
{
    class Account
    {
        public string AccountNumber { get; private set; } // 账号可以从外部读取，但只能在 Account 类内部设置
        private decimal _balance; // 私有字段，只能在 Account 类内部访问

        public Account(string accountNumber, decimal initialBalance)
        {
            AccountNumber = accountNumber;
            _balance = initialBalance;
        }

        public decimal GetBalance() // 公共方法，用于获取余额
        {
            return _balance;
        }

        public void Deposit(decimal amount) // 公共方法，用于存款
        {
            if (amount > 0)
            {
                _balance += amount;
                Console.WriteLine($"存款 {amount} 成功。当前余额: {_balance}");
            }
            else
            {
                Console.WriteLine("存款金额必须大于零。");
            }
        }

        public void Withdraw(decimal amount) // 公共方法，用于取款
        {
            if (amount > 0 && _balance >= amount)
            {
                _balance -= amount;
                Console.WriteLine($"取款 {amount} 成功。当前余额: {_balance}");
            }
            else
            {
                Console.WriteLine("取款失败：金额无效或余额不足。");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Account myAccount = new Account("123456789", 1000m);

            Console.WriteLine($"账号: {myAccount.AccountNumber}");
            Console.WriteLine($"初始余额: {myAccount.GetBalance()}");

            myAccount.Deposit(500m);
            myAccount.Withdraw(200m);
            myAccount.Withdraw(2000m); // 余额不足

            // myAccount._balance = 5000m; // 编译错误：_balance 是 private
            // myAccount.AccountNumber = "987654321"; // 编译错误：AccountNumber 的 set 是 private

            Console.ReadKey();
        }
    }
}
```

#### 5.3 继承 (Inheritance)

**继承**允许一个类（子类/派生类）从另一个类（父类/基类）继承属性和方法。子类可以重用父类的代码，并可以添加自己的特有属性和方法，或者覆盖（Override）父类的方法。



使用冒号 `:` 来表示继承。



C#

```
using System;

namespace OOP
{
    // 基类 (父类)
    class Animal
    {
        public string Name { get; set; }
        public int Age { get; set; }

        public Animal(string name, int age)
        {
            Name = name;
            Age = age;
        }

        public void Eat()
        {
            Console.WriteLine($"{Name} 正在吃东西。");
        }

        public virtual void MakeSound() // virtual 关键字表示该方法可以在子类中被重写
        {
            Console.WriteLine($"{Name} 发出声音。");
        }
    }

    // 派生类 (子类) Dog 继承自 Animal
    class Dog : Animal
    {
        public string Breed { get; set; }

        public Dog(string name, int age, string breed) : base(name, age) // base 关键字调用父类的构造函数
        {
            Breed = breed;
        }

        public void Bark()
        {
            Console.WriteLine($"{Name} 汪汪叫！");
        }

        // 重写 (Override) 父类的方法
        public override void MakeSound() // override 关键字表示重写父类方法
        {
            Console.WriteLine($"{Name} 发出狗叫声：汪汪！");
        }
    }

    // 派生类 (子类) Cat 继承自 Animal
    class Cat : Animal
    {
        public Cat(string name, int age) : base(name, age) { }

        public void Meow()
        {
            Console.WriteLine($"{Name} 喵喵叫！");
        }

        public override void MakeSound()
        {
            Console.WriteLine($"{Name} 发出猫叫声：喵喵！");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Animal animal = new Animal("动物", 5);
            animal.Eat();
            animal.MakeSound(); // 动物发出声音。

            Dog myDog = new Dog("旺财", 3, "金毛");
            myDog.Eat(); // 继承自 Animal
            myDog.Bark(); // Dog 自己的方法
            myDog.MakeSound(); // 旺财发出狗叫声：汪汪！ (重写后的方法)

            Cat myCat = new Cat("咪咪", 2);
            myCat.Eat(); // 继承自 Animal
            myCat.Meow(); // Cat 自己的方法
            myCat.MakeSound(); // 咪咪发出猫叫声：喵喵！ (重写后的方法)

            // 多态性：父类引用指向子类对象
            Animal pet1 = new Dog("哈士奇", 4, "哈士奇");
            Animal pet2 = new Cat("布偶", 1);

            pet1.MakeSound(); // 哈士奇发出狗叫声：汪汪！
            pet2.MakeSound(); // 布偶发出猫叫声：喵喵！
            // pet1.Bark(); // 编译错误，pet1 是 Animal 类型，没有 Bark 方法

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `public virtual void MakeSound()`: `virtual` 关键字允许子类重写这个方法。
- `public override void MakeSound()`: `override` 关键字表示子类正在重写父类的一个虚方法。
- `: base(name, age)`: 在子类的构造函数中，使用 `base` 关键字调用父类的构造函数，以初始化父类中定义的属性。
- **多态性 (Polymorphism)：** 在 `Main` 方法中，`Animal pet1 = new Dog(...)` 和 `Animal pet2 = new Cat(...)` 展示了多态性。尽管 `pet1` 和 `pet2` 的类型都是 `Animal`，但当调用 `MakeSound()` 方法时，实际执行的是它们各自子类中重写的方法。

#### 5.4 抽象类 (Abstract Classes) 和抽象方法 (Abstract Methods)

**抽象类**不能被实例化，只能作为其他类的基类。抽象类可以包含抽象方法（没有实现的方法）和非抽象方法。

**抽象方法**没有实现，必须在派生类中被重写。

C#

```
using System;

namespace OOP
{
    // 抽象基类
    abstract class Shape
    {
        public string Color { get; set; }

        public Shape(string color)
        {
            Color = color;
        }

        // 抽象方法 (没有实现，必须在派生类中重写)
        public abstract double GetArea();

        // 非抽象方法
        public void DisplayColor()
        {
            Console.WriteLine($"这个形状的颜色是: {Color}");
        }
    }

    // 派生类 Circle
    class Circle : Shape
    {
        public double Radius { get; set; }

        public Circle(string color, double radius) : base(color)
        {
            Radius = radius;
        }

        // 重写抽象方法 GetArea
        public override double GetArea()
        {
            return Math.PI * Radius * Radius;
        }
    }

    // 派生类 Rectangle
    class Rectangle : Shape
    {
        public double Width { get; set; }
        public double Height { get; set; }

        public Rectangle(string color, double width, double height) : base(color)
        {
            Width = width;
            Height = height;
        }

        // 重写抽象方法 GetArea
        public override double GetArea()
        {
            return Width * Height;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Shape shape = new Shape("红色"); // 编译错误：不能创建抽象类的实例

            Circle circle = new Circle("蓝色", 5.0);
            Rectangle rectangle = new Rectangle("绿色", 4.0, 6.0);

            circle.DisplayColor();
            Console.WriteLine($"圆的面积: {circle.GetArea():F2}");

            rectangle.DisplayColor();
            Console.WriteLine($"矩形的面积: {rectangle.GetArea():F2}");

            // 通过抽象类引用多态地调用 GetArea
            Shape[] shapes = new Shape[2];
            shapes[0] = circle;
            shapes[1] = rectangle;

            Console.WriteLine("\n遍历形状数组，多态调用 GetArea:");
            foreach (Shape s in shapes)
            {
                s.DisplayColor();
                Console.WriteLine($"面积: {s.GetArea():F2}");
            }

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `abstract class Shape`: `abstract` 关键字声明一个抽象类。
- `public abstract double GetArea();`: 抽象方法只有声明，没有方法体。
- 子类 `Circle` 和 `Rectangle` 必须 `override` 抽象方法 `GetArea()`，否则会发生编译错误。

#### 5.5 接口 (Interfaces)

**接口**定义了一组行为（方法、属性、事件、索引器），但没有实现。类可以实现一个或多个接口，从而承诺提供接口中定义的所有行为的实现。接口可以实现多重继承，而类不能。

使用 `interface` 关键字声明接口。接口成员默认是 `public` 的。

C#

```
using System;

namespace OOP
{
    // 定义一个接口
    interface ISwimmable
    {
        void Swim(); // 接口方法没有方法体
    }

    interface IFlyable
    {
        void Fly();
    }

    // Dog 类实现 ISwimmable 接口
    class Dog : ISwimmable
    {
        public string Name { get; set; }

        public Dog(string name)
        {
            Name = name;
        }

        public void Bark()
        {
            Console.WriteLine($"{Name} 汪汪叫！");
        }

        // 实现 ISwimmable 接口的 Swim 方法
        public void Swim()
        {
            Console.WriteLine($"{Name} 正在狗刨式游泳！");
        }
    }

    // Bird 类实现 IFlyable 接口
    class Bird : IFlyable
    {
        public string Name { get; set; }

        public Bird(string name)
        {
            Name = name;
        }

        // 实现 IFlyable 接口的 Fly 方法
        public void Fly()
        {
            Console.WriteLine($"{Name} 正在天空翱翔！");
        }
    }

    // Duck 类实现 ISwimmable 和 IFlyable 两个接口
    class Duck : ISwimmable, IFlyable
    {
        public string Name { get; set; }

        public Duck(string name)
        {
            Name = name;
        }

        public void Swim()
        {
            Console.WriteLine($"{Name} 正在水里嘎嘎地游。");
        }

        public void Fly()
        {
            Console.WriteLine($"{Name} 正在扇动翅膀飞翔。");
        }

        public void Quack()
        {
            Console.WriteLine($"{Name} 嘎嘎叫。");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Dog myDog = new Dog("小黑");
            myDog.Bark();
            myDog.Swim(); // 调用接口实现的方法

            Bird myBird = new Bird("小鸟");
            myBird.Fly();

            Duck myDuck = new Duck("唐老鸭");
            myDuck.Swim();
            myDuck.Fly();
            myDuck.Quack();

            // 多态性：通过接口引用
            ISwimmable swimmer1 = new Dog("金毛");
            ISwimmable swimmer2 = new Duck("小黄鸭");

            Console.WriteLine("\n通过 ISwimmable 接口调用 Swim 方法:");
            swimmer1.Swim();
            swimmer2.Swim();

            IFlyable flyer1 = new Bird("鹦鹉");
            IFlyable flyer2 = new Duck("野鸭");

            Console.WriteLine("\n通过 IFlyable 接口调用 Fly 方法:");
            flyer1.Fly();
            flyer2.Fly();

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `interface ISwimmable`: 声明一个接口。
- `void Swim();`: 接口方法没有访问修饰符（因为默认是 `public`），也没有方法体。
- `class Dog : ISwimmable`: `Dog` 类实现了 `ISwimmable` 接口。
- 当一个类实现一个接口时，它必须提供接口中所有方法的具体实现。

------

### 章节六：异常处理 (Exception Handling)

**异常**是程序在运行时发生的错误或非预期事件。C# 提供了一种结构化的异常处理机制，使用 `try-catch-finally` 块来管理错误。

- `try` 块：包含可能引发异常的代码。
- `catch` 块：用于捕获和处理 `try` 块中抛出的特定类型的异常。
- `finally` 块：无论是否发生异常，`finally` 块中的代码都总会执行（例如，用于释放资源）。

**示例代码：**

C#

```
using System;

namespace ExceptionHandling
{
    class Program
    {
        static void Main(string[] args)
        {
            // 示例 1: 除以零异常
            Console.WriteLine("--- 示例 1: 除以零异常 ---");
            try
            {
                int a = 10;
                int b = 0;
                int result = a / b; // 这里会引发 DivideByZeroException
                Console.WriteLine($"结果: {result}"); // 这行代码不会执行
            }
            catch (DivideByZeroException ex) // 捕获特定类型的异常
            {
                Console.WriteLine($"错误: 除数不能为零！");
                Console.WriteLine($"异常消息: {ex.Message}");
                // Console.WriteLine($"堆栈跟踪: {ex.StackTrace}"); // 打印详细的错误信息
            }
            catch (Exception ex) // 捕获所有其他类型的异常（通常放在最后）
            {
                Console.WriteLine($"发生了未知错误: {ex.Message}");
            }
            finally
            {
                Console.WriteLine("除法操作完成。"); // 无论是否发生异常，都会执行
            }

            Console.WriteLine("\n--- 示例 2: 数组越界异常 ---");
            try
            {
                int[] numbers = { 1, 2, 3 };
                Console.WriteLine($"访问数组元素: {numbers[5]}"); // 这里会引发 IndexOutOfRangeException
            }
            catch (IndexOutOfRangeException ex)
            {
                Console.WriteLine($"错误: 数组索引超出范围！");
                Console.WriteLine($"异常消息: {ex.Message}");
            }
            finally
            {
                Console.WriteLine("数组操作完成。");
            }


            Console.WriteLine("\n--- 示例 3: 用户输入转换异常 ---");
            Console.Write("请输入一个整数: ");
            string input = Console.ReadLine();

            try
            {
                int parsedNumber = int.Parse(input); // 尝试将字符串转换为整数
                Console.WriteLine($"你输入的整数是: {parsedNumber}");
            }
            catch (FormatException ex)
            {
                Console.WriteLine($"输入格式错误: {ex.Message}");
            }
            catch (OverflowException ex)
            {
                Console.WriteLine($"输入值过大或过小: {ex.Message}");
            }
            finally
            {
                Console.WriteLine("用户输入处理完毕。");
            }

            Console.WriteLine("\n--- 示例 4: 使用 throw 抛出自定义异常 ---");
            try
            {
                ProcessAge(-5); // 传递一个无效年龄
            }
            catch (ArgumentOutOfRangeException ex)
            {
                Console.WriteLine($"年龄处理错误: {ex.Message}");
            }

            Console.ReadKey();
        }

        // 模拟一个可能抛出异常的方法
        static void ProcessAge(int age)
        {
            if (age < 0 || age > 150)
            {
                // 抛出自定义的 ArgumentOutOfRangeException 异常
                throw new ArgumentOutOfRangeException(nameof(age), "年龄必须在 0 到 150 之间。");
            }
            Console.WriteLine($"年龄 {age} 已成功处理。");
        }
    }
}
```

**代码解析：**

- `try`: 包含可能发生异常的代码。
- `catch (ExceptionType ex)`: 如果 `try` 块中发生 `ExceptionType` 类型的异常，则执行此 `catch` 块。`ex` 是一个异常对象，包含了关于异常的详细信息。
- 可以有多个 `catch` 块来捕获不同类型的异常。通常，将更具体的异常类型放在前面，将更通用的 `Exception` 类型放在最后。
- `finally`: 无论 `try` 块中是否发生异常，甚至在 `try` 或 `catch` 块中有 `return` 语句，`finally` 块中的代码都一定会执行。这对于资源清理（如关闭文件、数据库连接）非常有用。
- `throw new ExceptionType(...)`: 使用 `throw` 关键字可以手动抛出异常。你可以抛出 .NET 内置的异常类型，也可以自定义异常。

------

### 章节七：文件操作 (File I/O)

C# 提供了 `System.IO` 命名空间中的类来处理文件和目录。

**常用类：**

- `File`: 用于文件操作（读写、复制、删除等）。
- `Directory`: 用于目录操作（创建、删除、移动等）。
- `StreamReader`: 用于从文件中读取文本。
- `StreamWriter`: 用于向文件中写入文本。

**示例代码：**

C#

```
using System;
using System.IO; // 引入 System.IO 命名空间

namespace FileIOExample
{
    class Program
    {
        static void Main(string[] args)
        {
            string filePath = "mydata.txt";
            string directoryPath = "my_folder";

            // --- 1. 写入文件 ---
            Console.WriteLine("--- 写入文件 ---");
            try
            {
                // 使用 StreamWriter 写入文本到文件
                // using 语句确保 StreamWriter 对象在使用完毕后被正确关闭和释放资源
                using (StreamWriter writer = new StreamWriter(filePath))
                {
                    writer.WriteLine("Hello, C#!");
                    writer.WriteLine("这是我的第一个文件。");
                    writer.WriteLine("日期: " + DateTime.Now.ToShortDateString());
                }
                Console.WriteLine($"文本已成功写入到文件: {filePath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"写入文件时发生错误: {ex.Message}");
            }

            // --- 2. 读取文件 ---
            Console.WriteLine("\n--- 读取文件 ---");
            try
            {
                // 使用 StreamReader 从文件中读取文本
                using (StreamReader reader = new StreamReader(filePath))
                {
                    string line;
                    Console.WriteLine($"文件 '{filePath}' 的内容:");
                    while ((line = reader.ReadLine()) != null) // 逐行读取直到文件末尾
                    {
                        Console.WriteLine(line);
                    }
                }
            }
            catch (FileNotFoundException)
            {
                Console.WriteLine($"错误: 文件 '{filePath}' 不存在。");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"读取文件时发生错误: {ex.Message}");
            }

            // --- 3. 检查文件是否存在 ---
            Console.WriteLine("\n--- 检查文件是否存在 ---");
            if (File.Exists(filePath))
            {
                Console.WriteLine($"文件 '{filePath}' 存在。");
            }
            else
            {
                Console.WriteLine($"文件 '{filePath}' 不存在。");
            }

            // --- 4. 复制文件 ---
            Console.WriteLine("\n--- 复制文件 ---");
            string destinationPath = "mydata_copy.txt";
            try
            {
                File.Copy(filePath, destinationPath, true); // true 表示如果目标文件已存在则覆盖
                Console.WriteLine($"文件 '{filePath}' 已复制到 '{destinationPath}'。");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"复制文件时发生错误: {ex.Message}");
            }

            // --- 5. 删除文件 ---
            Console.WriteLine("\n--- 删除文件 ---");
            try
            {
                if (File.Exists(destinationPath))
                {
                    File.Delete(destinationPath);
                    Console.WriteLine($"文件 '{destinationPath}' 已删除。");
                }
                else
                {
                    Console.WriteLine($"文件 '{destinationPath}' 不存在，无法删除。");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"删除文件时发生错误: {ex.Message}");
            }

            // --- 6. 目录操作 ---
            Console.WriteLine("\n--- 目录操作 ---");
            // 创建目录
            if (!Directory.Exists(directoryPath))
            {
                Directory.CreateDirectory(directoryPath);
                Console.WriteLine($"目录 '{directoryPath}' 已创建。");
            }
            else
            {
                Console.WriteLine($"目录 '{directoryPath}' 已存在。");
            }

            // 在新目录中创建文件
            string newFilePath = Path.Combine(directoryPath, "report.txt"); // 组合路径
            try
            {
                File.WriteAllText(newFilePath, "这是报告内容。"); // 写入所有文本到文件
                Console.WriteLine($"文件 '{newFilePath}' 已创建。");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"在新目录中创建文件时发生错误: {ex.Message}");
            }

            // 获取目录中的文件
            Console.WriteLine($"\n'{directoryPath}' 目录中的文件:");
            string[] filesInDir = Directory.GetFiles(directoryPath);
            foreach (string file in filesInDir)
            {
                Console.WriteLine(Path.GetFileName(file)); // 只获取文件名
            }

            // 删除目录 (如果目录非空，需要使用 Directory.Delete(path, true))
            try
            {
                if (Directory.Exists(directoryPath))
                {
                    Directory.Delete(directoryPath, true); // true 表示递归删除目录及其内容
                    Console.WriteLine($"目录 '{directoryPath}' 已删除。");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"删除目录时发生错误: {ex.Message}");
            }

            Console.ReadKey();
        }
    }
}
```

**代码解析：**

- `using (StreamWriter writer = new StreamWriter(filePath))`: `using` 语句是一种 C# 特有的语法糖，它确保 `StreamWriter` 对象在作用域结束时自动调用 `Dispose()` 方法，从而正确关闭文件句柄和释放资源，即使发生异常。
- `File.Exists(filePath)`: 检查文件是否存在。
- `Directory.Exists(directoryPath)`: 检查目录是否存在。
- `Path.Combine(directoryPath, "report.txt")`: `Path.Combine` 方法用于安全地组合路径，它会自动处理路径分隔符。
- `File.WriteAllText(newFilePath, "这是报告内容。")`: 这是一个便捷方法，用于将所有文本一次性写入文件。
- `Directory.Delete(directoryPath, true)`: 第二个参数 `true` 表示递归删除目录及其所有内容。如果目录中存在文件或子目录，不带 `true` 参数的 `Delete` 方法会抛出异常。

------

### 章节八：LINQ (Language Integrated Query) 基础

**LINQ**（Language Integrated Query，语言集成查询）是 C# 3.0 引入的一项强大功能，它允许你使用类似 SQL 的语法来查询和操作各种数据源，如集合、数据库、XML 等。

LINQ 的核心思想是提供一种统一的查询语法，无论数据存储在哪里，都可以用相同的方式进行查询。

**LINQ 语法：**

LINQ 查询可以有两种语法形式：

1. **查询语法 (Query Syntax)：** 更接近 SQL，可读性好。
2. **方法语法 (Method Syntax)：** 使用扩展方法和 Lambda 表达式，更简洁灵活。

通常，方法语法在实际开发中更常用，因为其灵活性更高，并且许多复杂的查询只能通过方法语法实现。

**示例代码：**

C#

```
using System;
using System.Collections.Generic;
using System.Linq; // 引入 System.Linq 命名空间，LINQ 需要此命名空间

namespace LinqExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 示例数据源：整数列表
            List<int> numbers = new List<int> { 1, 5, 8, 12, 15, 20, 25, 30, 35, 40 };

            // 示例数据源：字符串数组
            string[] names = { "Alice", "Bob", "Charlie", "David", "Eve", "Frank" };

            // 示例数据源：自定义对象列表
            List<Student> students = new List<Student>
            {
                new Student("Alice", 20, 85),
                new Student("Bob", 22, 92),
                new Student("Charlie", 21, 78),
                new Student("David", 20, 95),
                new Student("Eve", 23, 88)
            };

            Console.WriteLine("--- LINQ 查询示例 ---");

            // --- 1. 过滤 (Where) ---
            // 查询语法：获取所有偶数
            var evenNumbersQuery = from num in numbers
                                   where num % 2 == 0
                                   select num;
            Console.WriteLine("\n偶数 (查询语法): " + string.Join(", ", evenNumbersQuery));

            // 方法语法：获取所有大于 10 的数字
            var greaterThanTenMethod = numbers.Where(num => num > 10);
            Console.WriteLine("大于 10 的数字 (方法语法): " + string.Join(", ", greaterThanTenMethod));

            // --- 2. 排序 (OrderBy, OrderByDescending) ---
            // 查询语法：按字母顺序排序名字
            var sortedNamesQuery = from name in names
                                   orderby name
                                   select name;
            Console.WriteLine("\n排序后的名字 (查询语法): " + string.Join(", ", sortedNamesQuery));

            // 方法语法：按分数降序排序学生
            var studentsByScoreDesc = students.OrderByDescending(s => s.Score);
            Console.WriteLine("\n按分数降序排序的学生 (方法语法):");
            foreach (var student in studentsByScoreDesc)
            {
                Console.WriteLine($"- {student.Name}, 分数: {student.Score}");
            }

            // --- 3. 投影 (Select) ---
            // 查询语法：只选择学生的名字
            var studentNamesQuery = from student in students
                                    select student.Name;
            Console.WriteLine("\n学生姓名 (查询语法): " + string.Join(", ", studentNamesQuery));

            // 方法语法：选择学生的姓名和分数组成匿名对象
            var studentNameScores = students.Select(s => new { s.Name, s.Score });
            Console.WriteLine("\n学生姓名和分数 (方法语法，匿名对象):");
            foreach (var item in studentNameScores)
            {
                Console.WriteLine($"- 姓名: {item.Name}, 分数: {item.Score}");
            }

            // --- 4. 分组 (GroupBy) ---
            // 方法语法：按年龄分组学生
            var studentsByAge = students.GroupBy(s => s.Age);
            Console.WriteLine("\n按年龄分组的学生 (方法语法):");
            foreach (var group in studentsByAge)
            {
                Console.WriteLine($"年龄: {group.Key}");
                foreach (var student in group)
                {
                    Console.WriteLine($"- {student.Name}");
                }
            }

            // --- 5. 聚合函数 (Count, Sum, Average, Max, Min) ---
            Console.WriteLine("\n聚合函数:");
            Console.WriteLine($"数字总数: {numbers.Count()}");
            Console.WriteLine($"所有数字之和: {numbers.Sum()}");
            Console.WriteLine($"所有数字的平均值: {numbers.Average()}");
            Console.WriteLine($"最大数字: {numbers.Max()}");
            Console.WriteLine($"最小数字: {numbers.Min()}");

            Console.WriteLine($"学生总数: {students.Count()}");
            Console.WriteLine($"学生总分数: {students.Sum(s => s.Score)}"); // 求特定属性的和
            Console.WriteLine($"学生平均分数: {students.Average(s => s.Score):F2}");


            // --- 6. First, FirstOrDefault, Single, SingleOrDefault ---
            Console.WriteLine("\n查找元素:");
            var firstEven = numbers.First(num => num % 2 == 0); // 第一个偶数
            Console.WriteLine($"第一个偶数: {firstEven}");

            var twenty = numbers.FirstOrDefault(num => num == 20); // 找到 20
            Console.WriteLine($"找到 20: {twenty}");

            var nonExistent = numbers.FirstOrDefault(num => num == 999); // 找不到 999，返回默认值 (0)
            Console.WriteLine($"找到 999 (FirstOrDefault): {nonExistent}");

            // var singleStudent = students.Single(s => s.Name == "Alice"); // 找到唯一的 Alice
            // Console.WriteLine($"唯一的 Alice: {singleStudent.Name}");

            // 如果有多个匹配项，Single() 会抛出异常。FirstOrDefault() 返回第一个，SingleOrDefault() 如果有多个匹配项会抛出异常，否则返回唯一一个或默认值
            // var multipleAlice = students.Single(s => s.Age == 20); // 会抛出异常，因为有两个年龄为 20 的学生

            Console.ReadKey();
        }
    }

    class Student
    {
        public string Name { get; set; }
        public int Age { get; set; }
        public int Score { get; set; }

        public Student(string name, int age, int score)
        {
            Name = name;
            Age = age;
            Score = score;
        }
    }
}
```

**代码解析：**

- `using System.Linq;`: 这是使用 LINQ 的必要命名空间。
- **Lambda 表达式 (`=>`)：** LINQ 方法语法大量使用 Lambda 表达式。`num => num > 10` 表示一个匿名函数，它接受一个 `num` 作为输入，并返回 `num > 10` 的布尔值。
- **延迟执行 (Deferred Execution)：** 大多数 LINQ 查询操作都是延迟执行的。这意味着查询定义本身不会立即执行，而是在你遍历查询结果时才真正执行。这允许你构建复杂的查询而无需立即处理大量数据，提高效率。当你调用 `ToList()`, `ToArray()`, `Count()`, `Sum()` 等方法时，查询才会立即执行。