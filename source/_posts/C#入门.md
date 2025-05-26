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

。

**C# 官方教程资源推荐:**

1.  **Microsoft Learn - C# 文档:** [https://learn.microsoft.com/zh-cn/dotnet/csharp/](https://learn.microsoft.com/zh-cn/dotnet/csharp/) (这是最权威的官方文档和教程入口)
2.  **Microsoft Learn - C# 101 视频系列 (英文，但有字幕):** 通常在 .NET YouTube 频道或 Microsoft Learn 上能找到。
3.  **.NET 官网 - 入门:** [https://dotnet.microsoft.com/learn/csharp](https://dotnet.microsoft.com/learn/csharp)

---

**C# 入门教程总结 (含实操案例)**


**教程大纲:**

1.  **环境搭建与第一个程序 (Hello World)**
2.  **变量与数据类型**
3.  **运算符**
4.  **控制流 (条件语句与循环)**
5.  **方法 (函数)**
6.  **数组与集合 (列表)**
7.  **面向对象编程 (OOP) 基础**
    *   类 (Class) 与对象 (Object)
    *   封装 (Encapsulation) - 属性 (Properties)
    *   继承 (Inheritance)
    *   (多态 (Polymorphism) - 简单提及)
8.  **异常处理 (Error Handling)**
9.  **文件操作 (简单示例)**
10. **LINQ (语言集成查询) 简介**

---

**1. 环境搭建与第一个程序 (Hello World)**

*   **目标:** 创建并运行你的第一个C#程序。

*   **步骤 (以 Visual Studio Code 和 .NET SDK 为例):**
    1.  安装 .NET SDK ([https://dotnet.microsoft.com/download](https://dotnet.microsoft.com/download))。
    2.  安装 VS Code ([https://code.visualstudio.com/](https://code.visualstudio.com/))。
    3.  在 VS Code 中安装 C# 扩展 (来自 Microsoft)。
    4.  打开终端 (Terminal) 或命令提示符：
        ```bash
        mkdir MyFirstApp
        cd MyFirstApp
        dotnet new console
        code .
        ```
        这会创建一个名为 `MyFirstApp` 的文件夹，在其中创建一个新的控制台应用程序，并用 VS Code 打开它。
    5.  打开 `Program.cs` 文件，你会看到类似内容：

        ```csharp
        // Program.cs
        Console.WriteLine("Hello, World!");
        ```
        (对于较新版本的 .NET, `Program.cs` 可能更简洁，只有上面这一行。旧版本会有一个 `Main` 方法。)

    6.  在 VS Code 的终端中运行:
        ```bash
        dotnet run
        ```
    7.  **输出:** `Hello, World!`

---

**2. 变量与数据类型**

*   **目标:** 理解如何存储和使用不同类型的数据。
*   **核心数据类型:**
    *   `int`: 整数 (e.g., 10, -5)
    *   `double`: 双精度浮点数 (e.g., 3.14, -0.5)
    *   `string`: 文本字符串 (e.g., "你好", "C#")
    *   `bool`: 布尔值 (true 或 false)
    *   `char`: 单个字符 (e.g., 'A', 'x')

*   **案例:**

    ```csharp
    // 在 Program.cs 中 (可以替换掉 Hello World 的内容)
    using System; // 确保 System 命名空间被引用，Console 就在里面

    class Program
    {
        static void Main(string[] args) // 如果你的 Program.cs 没有 Main, 可以加上
        {
            // 声明和初始化变量
            int age = 30;
            double pi = 3.14159;
            string name = "Alice";
            bool isActive = true;
            char initial = 'A';

            // 输出变量的值
            Console.WriteLine("姓名: " + name); // 字符串拼接
            Console.WriteLine($"年龄: {age}");   // 字符串插值 (推荐)
            Console.WriteLine($"圆周率: {pi}");
            Console.WriteLine($"激活状态: {isActive}");
            Console.WriteLine($"首字母: {initial}");

            // 从用户那里获取输入
            Console.Write("请输入你的名字: "); // Write 不换行
            string? userName = Console.ReadLine(); // ReadLine 返回 string? (可空字符串)
            Console.WriteLine($"你好, {userName}!");
        }
    }
    ```
    **运行:** `dotnet run`，并按提示输入。

---

**3. 运算符**

*   **目标:** 学习如何对数据进行操作。
*   **主要运算符:**
    *   **算术:** `+`, `-`, `*`, `/`, `%` (取模)
    *   **赋值:** `=`, `+=`, `-=`, `*=`, `/=`, `++`, `--`
    *   **比较:** `==`, `!=`, `>`, `<`, `>=`, `<=`
    *   **逻辑:** `&&` (与), `||` (或), `!` (非)

*   **案例:**

    ```csharp
    // ... 在 Main 方法内 ...
    int a = 10;
    int b = 3;

    Console.WriteLine($"a + b = {a + b}");         // 13
    Console.WriteLine($"a - b = {a - b}");         // 7
    Console.WriteLine($"a * b = {a * b}");         // 30
    Console.WriteLine($"a / b = {a / b}");         // 3 (整数除法，舍去小数)
    Console.WriteLine($"a % b = {a % b}");         // 1 (余数)

    double c = 10.0;
    double d = 3.0;
    Console.WriteLine($"c / d = {c / d}");         // 3.333... (浮点数除法)

    int x = 5;
    x += 2; // x = x + 2;  x 现在是 7
    Console.WriteLine($"x: {x}");
    x++;    // x = x + 1;  x 现在是 8
    Console.WriteLine($"x after increment: {x}");

    bool condition1 = (a > b);    // true
    bool condition2 = (a == 10);  // true
    Console.WriteLine($"a > b: {condition1}");
    Console.WriteLine($"a > b AND a == 10: {condition1 && condition2}"); // true
    Console.WriteLine($"NOT (a > b): {!condition1}"); // false
    ```

---

**4. 控制流 (条件语句与循环)**

*   **目标:** 控制程序的执行流程。

*   **`if-else if-else` 语句:**

    ```csharp
    // ... 在 Main 方法内 ...
    Console.Write("请输入一个数字: ");
    string? input = Console.ReadLine();
    // int number = int.Parse(input); // 这行如果输入非数字会抛异常，后面学异常处理
    
    // 更安全的转换
    if (int.TryParse(input, out int number))
    {
        if (number > 0)
        {
            Console.WriteLine("你输入的是一个正数。");
        }
        else if (number < 0)
        {
            Console.WriteLine("你输入的是一个负数。");
        }
        else
        {
            Console.WriteLine("你输入的是零。");
        }
    }
    else
    {
        Console.WriteLine("无效的输入，请输入一个数字。");
    }
    ```

*   **`switch` 语句:**

    ```csharp
    // ... 在 Main 方法内 ...
    Console.Write("请输入星期几 (1-7): ");
    string? dayInput = Console.ReadLine();
    if (int.TryParse(dayInput, out int dayNumber))
    {
        string dayName;
        switch (dayNumber)
        {
            case 1:
                dayName = "星期一";
                break;
            case 2:
                dayName = "星期二";
                break;
            // ... 其他 case ...
            case 6:
            case 7:
                dayName = "周末";
                break;
            default:
                dayName = "无效的日期";
                break;
        }
        Console.WriteLine(dayName);
    }
    ```

*   **`for` 循环:**

    ```csharp
    // ... 在 Main 方法内 ...
    Console.WriteLine("使用 for 循环打印数字 1 到 5:");
    for (int i = 1; i <= 5; i++)
    {
        Console.WriteLine(i);
    }
    ```

*   **`while` 循环:**

    ```csharp
    // ... 在 Main 方法内 ...
    int countdown = 3;
    Console.WriteLine("使用 while 循环进行倒计时:");
    while (countdown > 0)
    {
        Console.WriteLine(countdown);
        countdown--; // 关键：改变循环条件，避免死循环
    }
    Console.WriteLine("发射!");
    ```

*   **`do-while` 循环 (至少执行一次):**

    ```csharp
    // ... 在 Main 方法内 ...
    string? secretCode;
    do
    {
        Console.Write("请输入密码 (输入 'exit' 退出): ");
        secretCode = Console.ReadLine();
    } while (secretCode != "1234" && secretCode != "exit");

    if (secretCode == "1234")
    {
        Console.WriteLine("密码正确!");
    }
    else
    {
        Console.WriteLine("已退出。");
    }
    ```

---

**5. 方法 (函数)**

*   **目标:** 将代码组织成可重用的块。
*   **语法:** `[修饰符] 返回类型 方法名([参数列表]) { // 方法体 }`

*   **案例:**

    ```csharp
    // 放在 Program 类的内部，Main 方法的外部或内部 (局部函数，C# 7.0+)
    // 这里作为 Program 类的静态方法
    class Program
    {
        static void Main(string[] args)
        {
            SayHello("张三"); // 调用方法
            SayHello("李四");

            int sum = Add(5, 7);
            Console.WriteLine($"5 + 7 = {sum}");

            double area = CalculateCircleArea(2.5);
            Console.WriteLine($"半径为 2.5 的圆面积是: {area:F2}"); // F2 格式化为两位小数
        }

        // 无返回值的方法 (void)
        static void SayHello(string personName)
        {
            Console.WriteLine($"你好, {personName}!");
        }

        // 有返回值的方法
        static int Add(int num1, int num2)
        {
            return num1 + num2;
        }

        // 另一个有返回值的方法
        static double CalculateCircleArea(double radius)
        {
            return Math.PI * radius * radius;
        }
    }
    ```

---

**6. 数组与集合 (列表)**

*   **目标:** 存储一组相同类型的数据。

*   **数组 (Array):** 固定大小。

    ```csharp
    // ... 在 Main 方法内 ...
    // 声明并初始化数组
    int[] numbers = { 10, 20, 30, 40, 50 };
    string[] names = new string[3]; // 创建一个能存3个字符串的空数组
    names[0] = "小明";
    names[1] = "小红";
    names[2] = "小刚";

    Console.WriteLine("数组中的数字:");
    // 使用 for 循环遍历数组
    for (int i = 0; i < numbers.Length; i++)
    {
        Console.WriteLine(numbers[i]);
    }

    Console.WriteLine("\n数组中的名字 (使用 foreach):");
    // 使用 foreach 循环遍历数组 (更简洁)
    foreach (string name in names)
    {
        Console.WriteLine(name);
    }
    ```

*   **列表 (List<T>):** 动态大小，更灵活。需要 `using System.Collections.Generic;`

    ```csharp
    using System;
    using System.Collections.Generic; // 引用 List 所在的命名空间

    class Program
    {
        static void Main(string[] args)
        {
            // 创建一个字符串列表
            List<string> fruits = new List<string>();

            // 添加元素
            fruits.Add("苹果");
            fruits.Add("香蕉");
            fruits.Add("橙子");

            Console.WriteLine("水果列表:");
            foreach (string fruit in fruits)
            {
                Console.WriteLine(fruit);
            }

            // 访问元素
            Console.WriteLine($"\n第一个水果: {fruits[0]}");

            // 插入元素
            fruits.Insert(1, "葡萄"); // 在索引1处插入
            Console.WriteLine("\n插入葡萄后的列表:");
            foreach (string fruit in fruits)
            {
                Console.WriteLine(fruit);
            }

            // 移除元素
            fruits.Remove("香蕉");
            Console.WriteLine("\n移除香蕉后的列表:");
            foreach (string fruit in fruits)
            {
                Console.WriteLine(fruit);
            }

            Console.WriteLine($"\n列表中的水果数量: {fruits.Count}");
        }
    }
    ```

---

**7. 面向对象编程 (OOP) 基础**

*   **目标:** 理解类、对象、封装和继承的基本概念。

*   **类 (Class) 与对象 (Object):**
    *   **类:** 对象的蓝图或模板。定义了对象的属性 (数据) 和方法 (行为)。
    *   **对象:** 类的实例。

*   **案例 (创建一个 `Person` 类):**

    1.  在你的项目 `MyFirstApp` 中创建一个新文件，例如 `Person.cs`。
    2.  编辑 `Person.cs`:

        ```csharp
        // Person.cs
        using System;

        public class Person
        {
            // 字段 (Fields) - 通常设为 private，通过属性访问
            private string _name;
            private int _age;

            // 属性 (Properties) - 控制对字段的访问 (封装)
            public string Name
            {
                get { return _name; }
                set { _name = value; } // value 是赋过来的值
            }

            public int Age
            {
                get { return _age; }
                set
                {
                    if (value >= 0 && value <= 150) // 简单的年龄验证
                    {
                        _age = value;
                    }
                    else
                    {
                        Console.WriteLine("无效的年龄!");
                    }
                }
            }

            // 构造函数 (Constructor) - 用于创建对象时初始化
            public Person(string name, int age)
            {
                this.Name = name; // 使用属性来赋值，这样会经过验证
                this.Age = age;
            }

            // 方法 (Methods)
            public void Introduce()
            {
                Console.WriteLine($"大家好，我叫 {Name}，今年 {Age} 岁。");
            }
        }
        ```

    3.  修改 `Program.cs` 来使用 `Person` 类:

        ```csharp
        // Program.cs
        using System;
        // 如果 Person.cs 和 Program.cs 在同一个命名空间下 (默认情况)，则不需要额外 using

        class Program
        {
            static void Main(string[] args)
            {
                // 创建 Person 对象 (实例化)
                Person person1 = new Person("王五", 28);
                Person person2 = new Person("赵六", 35);

                // 调用对象的方法
                person1.Introduce();
                person2.Introduce();

                // 访问和修改属性
                person1.Age = 29;
                Console.WriteLine($"{person1.Name} 明年就 {person1.Age} 岁了。");

                Person person3 = new Person("小宝宝", -2); // 年龄验证会起作用
                person3.Introduce(); // 年龄可能为0或上次的有效值，取决于你的set逻辑
            }
        }
        ```

*   **继承 (Inheritance):**
    *   允许创建一个新类 (子类/派生类) 来继承现有类 (父类/基类) 的属性和方法。
    *   实现代码重用和创建层次结构。

*   **案例 (创建一个 `Student` 类继承自 `Person`):**
    1.  创建新文件 `Student.cs`:

        ```csharp
        // Student.cs
        using System;

        public class Student : Person // 使用 : 表示继承 Person 类
        {
            public string StudentID { get; set; }
            public string Major { get; set; }

            // Student 类的构造函数
            // base(name, age) 调用父类 Person 的构造函数
            public Student(string name, int age, string studentID, string major)
                : base(name, age)
            {
                this.StudentID = studentID;
                this.Major = major;
            }

            // 可以重写 (override) 父类的方法，如果父类方法标记为 virtual
            // 这里我们添加一个新方法
            public void Study()
            {
                Console.WriteLine($"{Name} 正在学习 {Major} 专业。学号是 {StudentID}。");
            }

            // 重写 Introduce 方法 (需要 Person.Introduce 标记为 virtual)
            // 假设 Person.Introduce() 已经改为: public virtual void Introduce() { ... }
            /*
            public override void Introduce()
            {
                base.Introduce(); // 调用父类的 Introduce 方法
                Console.WriteLine($"我是一名学生，主修 {Major}。");
            }
            */
        }
        ```
        **注意:** 为了能 `override` (重写) `Introduce` 方法，你需要回到 `Person.cs` 中，将 `public void Introduce()` 修改为 `public virtual void Introduce()`。

    2.  修改 `Program.cs` 来使用 `Student` 类:

        ```csharp
        // ... 在 Main 方法中 ...
        Student student1 = new Student("小华", 20, "S1001", "计算机科学");
        student1.Introduce(); // 调用 Person 类的 Introduce 方法
        student1.Study();
        ```

---

**8. 异常处理 (Error Handling)**

*   **目标:** 优雅地处理程序运行时可能发生的错误。
*   **`try-catch-finally` 块:**
    *   `try`: 包含可能引发异常的代码。
    *   `catch`: 如果 `try` 块中发生特定类型的异常，则执行此块。
    *   `finally`: 无论是否发生异常，总会执行此块 (通常用于资源清理)。

*   **案例:**

    ```csharp
    // ... 在 Main 方法内 ...
    Console.Write("请输入一个数字作为除数: ");
    string? divisorInput = Console.ReadLine();
    int dividend = 100;

    try
    {
        int divisor = int.Parse(divisorInput!); // ! 是null包容操作符，告诉编译器我们确定它不为null
                                                // 但如果用户不输入，这里仍然是null，int.Parse会抛异常
                                                // 更好的做法是检查 divisorInput 是否为 null 或 empty

        if (string.IsNullOrEmpty(divisorInput))
        {
            throw new ArgumentNullException(nameof(divisorInput), "除数不能为空");
        }

        int result = dividend / int.Parse(divisorInput);
        Console.WriteLine($"结果: {result}");
    }
    catch (FormatException ex) //捕获转换错误
    {
        Console.WriteLine($"输入格式错误: {ex.Message}");
    }
    catch (DivideByZeroException ex) // 捕获除以零错误
    {
        Console.WriteLine($"算术错误: {ex.Message}");
    }
    catch (ArgumentNullException ex) // 捕获我们自己抛出的 ArgumentNullException
    {
        Console.WriteLine($"参数错误: {ex.Message}");
    }
    catch (Exception ex) // 捕获所有其他类型的异常 (通常放在最后)
    {
        Console.WriteLine($"发生未知错误: {ex.Message}");
    }
    finally
    {
        Console.WriteLine("计算结束。");
    }
    ```

---

**9. 文件操作 (简单示例)**

*   **目标:** 读写文本文件。
*   需要 `using System.IO;`

*   **案例:**

    ```csharp
    using System;
    using System.IO; // 引用文件操作相关的命名空间

    class Program
    {
        static void Main(string[] args)
        {
            string filePath = "MyTextFile.txt"; // 文件将在程序运行目录下创建

            // 写入文件
            try
            {
                string contentToWrite = "这是第一行。\n这是第二行。\n你好，C#!";
                File.WriteAllText(filePath, contentToWrite);
                Console.WriteLine($"内容已写入到 {filePath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"写入文件时发生错误: {ex.Message}");
            }

            // 读取文件
            try
            {
                if (File.Exists(filePath))
                {
                    string fileContent = File.ReadAllText(filePath);
                    Console.WriteLine($"\n从 {filePath} 读取的内容:");
                    Console.WriteLine(fileContent);
                }
                else
                {
                    Console.WriteLine($"文件 {filePath} 不存在。");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"读取文件时发生错误: {ex.Message}");
            }
        }
    }
    ```

---

**10. LINQ (语言集成查询) 简介**

*   **目标:** 学习一种强大的查询数据的方式。
*   LINQ 可以用于查询各种数据源 (集合、数据库、XML 等)。
*   需要 `using System.Linq;`

*   **案例 (查询一个数字列表):**

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq; // 引用 LINQ 相关的命名空间

    class Program
    {
        static void Main(string[] args)
        {
            List<int> numbers = new List<int> { 1, 5, 3, 8, 2, 7, 4, 6, 9, 0 };

            // 1. 使用方法语法 (Method Syntax)
            var evenNumbers = numbers.Where(n => n % 2 == 0) // 筛选偶数
                                     .OrderBy(n => n);      // 按升序排序

            Console.WriteLine("偶数 (方法语法):");
            foreach (var num in evenNumbers)
            {
                Console.Write(num + " "); // 输出: 0 2 4 6 8
            }
            Console.WriteLine();

            // 2. 使用查询语法 (Query Syntax) - 更像 SQL
            var oddNumbersGreaterThanThree = from num in numbers
                                             where num % 2 != 0 && num > 3
                                             orderby num descending // 按降序排序
                                             select num;

            Console.WriteLine("\n大于3的奇数 (查询语法，降序):");
            foreach (var num in oddNumbersGreaterThanThree)
            {
                Console.Write(num + " "); // 输出: 9 7 5
            }
            Console.WriteLine();

            // 案例：查询 Person 对象列表
            List<Person> people = new List<Person>
            {
                new Person("Alice", 30),
                new Person("Bob", 25),
                new Person("Charlie", 35),
                new Person("Diana", 25)
            };

            // 找到所有年龄为 25 的人，并按名字排序
            var peopleAged25 = people.Where(p => p.Age == 25)
                                     .OrderBy(p => p.Name);

            Console.WriteLine("\n年龄为25岁的人:");
            foreach(var person in peopleAged25)
            {
                person.Introduce();
            }
        }
    }
    // 确保你的 Person 类在这个文件或项目可访问的地方定义
    // public class Person { ... } // (前面已定义的 Person 类)
    ```
    **注意:** 上面这个 LINQ 查询 Person 的例子需要 `Person` 类。如果 `Person.cs` 和 `Program.cs` 在同一个项目和默认命名空间下，它应该能直接工作。

---



