---
title: WPF入门
date: 2025-06-09 19:48:34
categories: 
  - "编程实战"
tags:
  - "C#" 
  - "WPF"
  - "框架"
description: |
    WPF 初学者学习手册：构建第一个桌面应用
---


## WPF 初学者学习手册：构建你的第一个桌面应用

欢迎来到 WPF 的世界！本手册将带你从零开始，逐步掌握 Windows Presentation Foundation (WPF) 的核心概念和技术，最终能够独立构建功能丰富的桌面应用程序。

### 章节一：WPF 简介与开发环境准备

#### 1.1 什么是 WPF？

WPF (Windows Presentation Foundation) 是微软 .NET 平台下的一个强大的 UI (用户界面) 框架，用于构建 Windows 桌面应用程序。

- **声明式 UI (XAML)：** WPF 最大的特点之一是使用 **XAML (eXtensible Application Markup Language)** 来定义用户界面。XAML 是一种基于 XML 的标记语言，它允许你以声明性的方式描述 UI 的结构、外观和行为。这种方式使得 UI 设计和业务逻辑的分离变得更加清晰，提高了代码的可读性和可维护性。
- **富媒体支持：** WPF 提供了出色的图形渲染能力，能够支持 2D 和 3D 图形、动画、视频、音频等。它利用 DirectX 进行硬件加速渲染，因此能够提供高性能和高质量的视觉效果。
- **数据绑定：** WPF 拥有强大的数据绑定引擎。你可以将 UI 元素直接连接到 C# 代码中的数据源。当数据改变时，UI 会自动更新，反之亦然，大大简化了 UI 和数据之间的同步。
- **样式和模板：** WPF 提供了丰富的样式 (Styles) 和模板 (Templates) 机制，让你能够轻松地自定义控件的外观和行为，实现高度可定制的 UI，而无需修改控件本身的逻辑。
- **矢量图形：** WPF 的渲染基于矢量图形，这意味着 UI 在不同分辨率的屏幕上都能保持清晰和锐利，而不会出现像素化。
- **事件驱动：** WPF 应用是事件驱动的，UI 元素会触发各种事件（如点击、键盘输入），你可以编写 C# 代码来响应这些事件。

**WPF 的优势：**

- **强大的 UI 表现力：** 能够创建视觉效果出色的应用程序。
- **易于维护：** XAML 和 C# 的分离，加上数据绑定，使得代码更易于组织和维护。
- **高效开发：** 声明式 UI 和数据绑定减少了手动编写 UI 逻辑的工作量。
- **硬件加速：** 利用 GPU 渲染，性能优越。

#### 1.2 开发环境准备

为了开始 WPF 开发，你需要安装 **Visual Studio**。

1. 下载 Visual Studio Community 版本：
   - 访问 Visual Studio 官网：https://visualstudio.microsoft.com/zh-hans/downloads/
   - 选择并下载 **Visual Studio Community** 版本（免费且功能强大）。
2. 运行安装程序并选择工作负载：
   - 启动下载的 `vs_community.exe` 或类似名称的安装程序。
   - 在“工作负载”界面，务必勾选 **".NET 桌面开发"**。这个工作负载包含了 WPF 开发所需的所有组件。
   - 你可以根据需要选择其他工作负载，例如“ASP.NET 和 Web 开发”或“使用 Unity 的游戏开发”，但对于 WPF 来说，".NET 桌面开发" 是必须的。
3. **安装：** 点击“安装”按钮，等待安装完成。这可能需要一些时间，取决于你的网络速度和选择的工作负载。

安装完成后，你就可以启动 Visual Studio，准备好踏上 WPF 学习之旅了！

#### 1.3 你的第一个 WPF 项目：Hello World

让我们从经典的 "Hello World" 开始。

**操作步骤：**

1. 打开 Visual Studio。

2. 点击 **“创建新项目”**。

3. 在搜索框中输入 

   “WPF 应用程序”

   。

   - **重要：** 请选择 **“WPF 应用程序”** 模板，并确保它是 **C#** 语言版本。
   - 通常会看到两个版本：“WPF 应用程序” (基于 .NET Core/.NET 5+) 和 “WPF 应用程序 (.NET Framework)”。**强烈建议选择基于最新 .NET 版本的模板 (例如 .NET 8.0 或更高版本)**，因为它代表了现代 .NET 开发的方向。

4. 点击 **“下一步”**。

5. 输入项目名称（例如：`MyFirstWPFApp`），选择项目存放位置。

6. 点击 **“下一步”**。

7. 选择目标框架（Target Framework），如果你选择了最新的 WPF 应用程序模板，这里会是 `.NET 8.0` 或更高版本。保持默认即可。

8. 点击 **“创建”**。

Visual Studio 会为你自动生成一个基本的 WPF 项目结构。你会看到两个重要的文件：

- `MainWindow.xaml`：这是定义用户界面（UI）的 XAML 文件。
- `MainWindow.xaml.cs`：这是与 `MainWindow.xaml` 相关联的 C# 后台代码文件。
- 



**`MainWindow.xaml` 文件内容 (精简版):**



XML

```
<Window x:Class="MyFirstWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:MyFirstWPFApp"
        mc:Ignorable="d"
        Title="我的第一个WPF应用" Height="450" Width="800">
    <Grid>
        <TextBlock Text="Hello, WPF!"
                   HorizontalAlignment="Center"
                   VerticalAlignment="Center"
                   FontSize="48"
                   FontWeight="Bold"
                   Foreground="Blue"/>
    </Grid>
</Window>
```

**`MainWindow.xaml.cs` 文件内容:**

C#

```
// MainWindow.xaml.cs

using System.Windows; // 引入 WPF 核心命名空间

namespace MyFirstWPFApp
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window // MainWindow 类继承自 Window
    {
        public MainWindow()
        {
            InitializeComponent(); // 这个方法由 WPF 自动生成，用于初始化 UI 元素
        }
    }
}
```

**代码解析：**

- **`MainWindow.xaml`:**

  - `<Window>`：这是 WPF 应用程序的根元素，代表一个窗口。

  - `x:Class="MyFirstWPFApp.MainWindow"`：这行将 XAML 文件与后台 C# 代码文件 `MyFirstWPFApp.MainWindow` 类关联起来。

  - ```
    xmlns="..."
    ```

    ：这些是 XML 命名空间声明，告诉 XAML 处理器如何解析和识别元素。

    - `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`：这是 WPF UI 元素的默认命名空间。
    - `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`：这是 XAML 语言的命名空间，`x:` 前缀用于 XAML 特有的属性，例如 `x:Class`。
    - `xmlns:local="clr-namespace:MyFirstWPFApp"`：将当前项目的命名空间映射为 `local` 前缀，这样你就可以在 XAML 中引用自己定义的类。

  - `Title="我的第一个WPF应用"`：设置窗口的标题。

  - `Height="450" Width="800"`：设置窗口的初始大小。

  - `<Grid>`：这是一个布局面板（将在下一章详细介绍），用于组织子元素。在这里，它是窗口的唯一子元素。

  - `<TextBlock Text="Hello, WPF!" ... />`：这是一个文本块控件，用于显示文本。我们设置了它的文本内容、对齐方式、字体大小、字重和颜色。

- **`MainWindow.xaml.cs`:**

  - `public partial class MainWindow : Window`: `partial` 关键字表示这个类的一部分定义在另一个文件中（即由 XAML 编译生成的代码）。`MainWindow` 继承自 `System.Windows.Window` 类，使其成为一个可显示的窗口。
  - `InitializeComponent()`: 这个方法由 Visual Studio 自动生成，并在构造函数中调用。它的作用是解析 `MainWindow.xaml` 文件并创建其中定义的 UI 元素。**不要手动修改这个方法。**

**运行程序：**

在 Visual Studio 中，点击工具栏上的绿色“启动”按钮（通常是“本地 Windows 调试器”旁边），或者按下 `F5` 键。

你会看到一个带有 "Hello, WPF!" 文本的 Windows 窗口。

### 章节二：XAML 基础与布局系统

#### 2.1 XAML 简介

XAML (eXtensible Application Markup Language) 是一种基于 XML 的标记语言，用于声明性地定义应用程序的用户界面。在 WPF 中，你用 XAML 来描述 UI 的外观，而用 C# 后台代码来处理 UI 的行为和业务逻辑。

**XAML 的优点：**

- **分离关注点：** UI 界面和逻辑代码分离，使得设计师和开发者可以并行工作。
- **直观易读：** 声明性语法比命令式代码更直观地描述 UI 结构。
- **工具支持：** Visual Studio 的设计器可以直接渲染 XAML，提供所见即所得的开发体验。

**XAML 语法基本规则：**

- **元素 (Elements)：** XAML 元素对应于 .NET 中的类。例如，`<Button>` 对应于 `System.Windows.Controls.Button` 类。

- **属性 (Attributes)：** 元素的属性对应于 .NET 类的属性。例如，`<Button Content="Click Me"/>` 中 `Content` 是 `Button` 类的一个属性。

- **嵌套：** 元素可以嵌套，形成 UI 树结构。例如，一个 `Grid` 可以包含多个 `Button`。

- **命名空间：** XAML 文件顶部的 `xmlns` 声明用于映射 XML 命名空间到 .NET 命名空间。`x:` 是 XAML 语言的默认前缀。

- 内容属性：

   某些控件有一个“内容属性”，可以直接在开始标签和结束标签之间放置内容，而无需显式指定属性名。例如，

  ```
  Button
  ```

   的 

  ```
  Content
  ```

   属性：

  XML

  ```
  <Button Content="Click Me"/>
  <Button>Click Me</Button>
  ```

  

- 



**示例：使用 XAML 创建简单 UI**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="XAML 基础" Height="300" Width="400">
    <StackPanel Orientation="Vertical" Margin="20">
        <TextBlock Text="欢迎来到 WPF！" FontSize="24" FontWeight="Bold" Margin="0,0,0,10"/>
        <TextBox Width="200" HorizontalAlignment="Left" Margin="0,0,0,10"
                 Text="请输入你的名字"/>
        <Button Content="点击我" Width="100" HorizontalAlignment="Left" Margin="0,0,0,10"/>
        <CheckBox Content="我同意" Margin="0,0,0,5"/>
        <RadioButton Content="选项 A" GroupName="MyOptions"/>
        <RadioButton Content="选项 B" GroupName="MyOptions"/>
    </StackPanel>
</Window>
```

这段 XAML 代码创建了一个窗口，里面包含了一个垂直堆叠的面板 (`StackPanel`)，面板中依次放置了 `TextBlock`、`TextBox`、`Button`、`CheckBox` 和两个 `RadioButton`。

#### 2.2 布局系统：组织你的 UI 元素

WPF 提供了强大的布局面板来组织和排列 UI 元素。它们能够根据可用空间自动调整子元素的位置和大小，实现响应式 UI。

**2.2.1 `Grid` (网格面板)**

`Grid` 是 WPF 中最常用、最灵活的布局面板，它允许你像表格一样使用行 (Rows) 和列 (Columns) 来排列子元素。

**关键属性：**

- `Grid.Row="index"`：将元素放置在指定行。

- `Grid.Column="index"`：将元素放置在指定列。

- `Grid.RowSpan="count"`：元素跨越的行数。

- `Grid.ColumnSpan="count"`：元素跨越的列数。

- ```
  RowDefinitions
  ```

  ：定义行的集合。

  - ```
    Height
    ```

    ：行的实际高度。

    - `Auto`：根据内容自动调整高度。
    - `*` (Star)：按比例分配可用空间。`*` 表示一份，`2*` 表示两份。
    - `Fixed Value`：固定像素值。
    - 

    

  - 

  

- 

- ```
  ColumnDefinitions
  ```

  ：定义列的集合。

  - 
  - `Width`：列的实际宽度，用法同 `Height`。
  - 

  

- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Grid 布局示例" Height="400" Width="600">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="2*"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="100"/>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="2*"/>
        </Grid.ColumnDefinitions>

        <Border Grid.Row="0" Grid.Column="0" Background="LightBlue" BorderBrush="Blue" BorderThickness="1">
            <TextBlock Text="R0C0 (Auto)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>
        <Border Grid.Row="0" Grid.Column="1" Background="LightCoral" BorderBrush="Red" BorderThickness="1">
            <TextBlock Text="R0C1 (*)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>
        <Border Grid.Row="0" Grid.Column="2" Background="LightGreen" BorderBrush="Green" BorderThickness="1">
            <TextBlock Text="R0C2 (2*)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>

        <Border Grid.Row="1" Grid.Column="0" Background="LightGray" BorderBrush="Gray" BorderThickness="1">
            <TextBlock Text="R1C0 (Fixed)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>
        <Border Grid.Row="1" Grid.Column="1" Grid.ColumnSpan="2" Background="LightPink" BorderBrush="HotPink" BorderThickness="1">
            <TextBlock Text="R1C1 (Span 2)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>

        <Border Grid.Row="2" Grid.Column="0" Grid.ColumnSpan="3" Background="LightYellow" BorderBrush="Orange" BorderThickness="1">
            <TextBlock Text="R2C0 (Span 3)" HorizontalAlignment="Center" VerticalAlignment="Center"/>
        </Border>
    </Grid>
</Window>
```

**小贴士：** 在 Visual Studio 的 XAML 设计器中，你可以直接拖拽 Grid 的行线和列线来调整大小，非常方便。

**2.2.2 `StackPanel` (堆叠面板)** `StackPanel` 用于将子元素沿一个方向（水平或垂直）堆叠排列。



**关键属性：**



- 
- `Orientation`：`Vertical` (默认) 或 `Horizontal`。
- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="StackPanel 布局示例" Height="300" Width="400">
    <Grid>
        <StackPanel Orientation="Vertical" HorizontalAlignment="Center" VerticalAlignment="Center">
            <Button Content="按钮 1" Width="150" Margin="5"/>
            <Button Content="按钮 2" Width="150" Margin="5"/>
            <Button Content="按钮 3" Width="150" Margin="5"/>
            <TextBlock Text="我是文本块" FontSize="18" Margin="5"/>
            <CheckBox Content="勾选我" Margin="5"/>
        </StackPanel>

        <StackPanel Orientation="Horizontal" VerticalAlignment="Bottom" HorizontalAlignment="Center">
            <TextBlock Text="水平项 1" Margin="5"/>
            <TextBlock Text="水平项 2" Margin="5"/>
            <TextBlock Text="水平项 3" Margin="5"/>
        </StackPanel>
    </Grid>
</Window>
```

**2.2.3 `DockPanel` (停靠面板)**

`DockPanel` 允许你将子元素停靠在其边缘（上、下、左、右），最后一个元素可以填充剩余空间。

**关键属性：**

- `DockPanel.Dock="value"`：在子元素上设置，指定停靠方向（`Top`, `Bottom`, `Left`, `Right`）。
- 
- `LastChildFill="true/false"`：指定最后一个子元素是否填充剩余空间（默认为 `true`）。
- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="DockPanel 布局示例" Height="400" Width="500">
    <DockPanel LastChildFill="True">
        <Button DockPanel.Dock="Top" Content="顶部按钮" Height="50" Background="LightCoral"/>
        <Button DockPanel.Dock="Bottom" Content="底部按钮" Height="50" Background="LightBlue"/>
        <Button DockPanel.Dock="Left" Content="左侧按钮" Width="100" Background="LightGreen"/>
        <Button DockPanel.Dock="Right" Content="右侧按钮" Width="100" Background="LightYellow"/>
        <TextBlock Text="中间内容区域" Background="LightGray"
                   HorizontalAlignment="Center" VerticalAlignment="Center" FontSize="24"/>
    </DockPanel>
</Window>
```

**2.2.4 `WrapPanel` (换行面板)**



`WrapPanel` 将子元素按顺序排列，当空间不足时自动换行。



**关键属性：**



- 
- `Orientation`：`Horizontal` (默认) 或 `Vertical`。
- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="WrapPanel 布局示例" Height="300" Width="400">
    <WrapPanel Orientation="Horizontal" Margin="10">
        <Button Content="按钮 1" Margin="5" Width="80"/>
        <Button Content="按钮 2" Margin="5" Width="80"/>
        <Button Content="按钮 3" Margin="5" Width="80"/>
        <Button Content="按钮 4" Margin="5" Width="80"/>
        <Button Content="按钮 5" Margin="5" Width="80"/>
        <Button Content="按钮 6" Margin="5" Width="80"/>
        <Button Content="按钮 7" Margin="5" Width="80"/>
        <TextBlock Text="长文本内容，当空间不足时会自动换行显示。"
                   Width="200" TextWrapping="Wrap" Margin="5"/>
    </WrapPanel>
</Window>
```

**2.2.5 `Canvas` (画布面板)**

`Canvas` 允许你使用绝对坐标来定位子元素。不推荐用于复杂布局，因为它不具备响应式能力。

**关键属性 (在子元素上设置)：**

- `Canvas.Left`：元素左边缘距 Canvas 左边缘的距离。
- 
- `Canvas.Top`：元素上边缘距 Canvas 上边缘的距离。
- 
- `Canvas.Right`, `Canvas.Bottom` 类似。
- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Canvas 布局示例" Height="300" Width="400">
    <Canvas Background="LightGray">
        <Rectangle Fill="Red" Width="100" Height="50" Canvas.Left="50" Canvas.Top="50"/>
        <Ellipse Fill="Blue" Width="80" Height="80" Canvas.Left="150" Canvas.Top="100"/>
        <TextBlock Text="绝对定位文本" FontSize="16" Canvas.Left="200" Canvas.Top="200"/>
    </Canvas>
</Window>
```

**总结布局面板：**

- **`Grid`**：最常用，适合复杂的网格状布局。
- **`StackPanel`**：适合简单的一维列表。
- **`DockPanel`**：适合有固定导航区或页眉页脚的布局。
- **`WrapPanel`**：适合内容需要自动换行的情况（如标签云）。
- **`Canvas`**：用于绘制或精确控制元素位置的场景，不适合常规布局。

在实际开发中，你通常会嵌套使用这些布局面板来构建复杂的 UI。

### 章节三：常用控件与事件处理



本章将介绍 WPF 中常用的 UI 控件，并演示如何通过 C# 代码来响应它们的事件。



#### 3.1 文本控件



- 
- **`TextBlock`：** 用于显示只读文本。
- 
- **`TextBox`：** 用于用户输入和编辑文本。
- 



**示例代码：**



XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="文本控件示例" Height="250" Width="400">
    <StackPanel Margin="20">
        <TextBlock Text="欢迎输入文本：" FontSize="18" Margin="0,0,0,10"/>
        <TextBox x:Name="MyTextBox" Width="300" Height="30" HorizontalAlignment="Left"
                 TextChanged="MyTextBox_TextChanged"/> <TextBlock x:Name="OutputTextBlock" Margin="0,10,0,0" FontSize="16" FontWeight="Bold"
                   Text="你输入的内容将显示在这里。"/>
    </StackPanel>
</Window>
```

C#

```
// MainWindow.xaml.cs
using System.Windows;
using System.Windows.Controls; // 引入 Control 命名空间

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        // MyTextBox 的 TextChanged 事件处理程序
        private void MyTextBox_TextChanged(object sender, TextChangedEventArgs e)
        {
            // 将 TextBox 的文本内容赋给 TextBlock
            OutputTextBlock.Text = MyTextBox.Text;
        }
    }
}
```

**代码解析：**

- `x:Name="MyTextBox"`：在 XAML 中为控件指定一个名称，这样你就可以在 C# 后台代码中通过这个名称引用它。
- `TextChanged="MyTextBox_TextChanged"`：将 `TextBox` 的 `TextChanged` 事件绑定到 C# 后台代码中的 `MyTextBox_TextChanged` 方法。当文本框内容改变时，这个方法就会被调用。
- 在 C# 代码中，我们通过 `MyTextBox.Text` 获取 `TextBox` 的当前文本，并将其赋值给 `OutputTextBlock.Text`。

#### 3.2 按钮 (`Button`)

`Button` 是最常用的交互控件，用于触发操作。

**示例代码：**

代码段

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="按钮示例" Height="200" Width="300">
    <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
        <Button Content="点击我！" Width="120" Height="40" FontSize="20"
                Click="MyButton_Click"/> <TextBlock x:Name="StatusTextBlock" Margin="0,10,0,0" FontSize="16"
                   Text="等待点击..."/>
    </StackPanel>
</Window>
```



C#

```
// MainWindow.xaml.cs
using System.Windows;
using System.Windows.Controls;

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        // 按钮的 Click 事件处理程序
        private void MyButton_Click(object sender, RoutedEventArgs e)
        {
            // 显示一个消息框
            MessageBox.Show("按钮被点击了！", "提示", MessageBoxButton.OK, MessageBoxImage.Information);

            // 更新文本块内容
            StatusTextBlock.Text = "按钮已点击！";
        }
    }
}
```

**代码解析：**

- `Click="MyButton_Click"`：将 `Button` 的 `Click` 事件绑定到 C# 后台代码中的 `MyButton_Click` 方法。
- `MessageBox.Show(...)`：显示一个简单的消息框。

#### 3.3 选择控件



- 
- **`CheckBox`：** 提供一个布尔状态（选中/未选中）。
- 
- **`RadioButton`：** 提供一组互斥的选择。
- 
- **`ComboBox`：** 下拉列表，用于从预定义列表中选择一项。
- 
- **`ListBox`：** 显示可选择的项目列表。
- 



**示例代码：**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="选择控件示例" Height="400" Width="500">
    <StackPanel Margin="20">
        <TextBlock Text="请选择您的偏好：" FontSize="18" FontWeight="Bold" Margin="0,0,0,10"/>

        <CheckBox x:Name="AgreeCheckBox" Content="我同意用户协议" Checked="AgreeCheckBox_Checked" Unchecked="AgreeCheckBox_Unchecked" Margin="0,0,0,10"/>
        <TextBlock x:Name="CheckBoxStatus" Text="状态: 未同意" Margin="0,0,0,10"/>

        <TextBlock Text="请选择性别：" Margin="0,10,0,5"/>
        <StackPanel Orientation="Horizontal" Margin="0,0,0,10">
            <RadioButton x:Name="MaleRadioButton" Content="男" GroupName="Gender" IsChecked="True" Checked="GenderRadioButton_Checked" Margin="0,0,10,0"/>
            <RadioButton x:Name="FemaleRadioButton" Content="女" GroupName="Gender" Checked="GenderRadioButton_Checked"/>
        </StackPanel>
        <TextBlock x:Name="GenderStatus" Text="性别: 男" Margin="0,0,0,10"/>

        <TextBlock Text="请选择城市：" Margin="0,10,0,5"/>
        <ComboBox x:Name="CityComboBox" Width="200" HorizontalAlignment="Left"
                  SelectionChanged="CityComboBox_SelectionChanged">
            <ComboBoxItem Content="北京" IsSelected="True"/>
            <ComboBoxItem Content="上海"/>
            <ComboBoxItem Content="广州"/>
            <ComboBoxItem Content="深圳"/>
        </ComboBox>
        <TextBlock x:Name="CityStatus" Text="城市: 北京" Margin="0,10,0,0"/>

        <TextBlock Text="请选择喜欢的颜色：" Margin="0,10,0,5"/>
        <ListBox x:Name="ColorListBox" Width="200" Height="100" HorizontalAlignment="Left"
                 SelectionChanged="ColorListBox_SelectionChanged">
            <ListBoxItem Content="红色"/>
            <ListBoxItem Content="绿色"/>
            <ListBoxItem Content="蓝色"/>
            <ListBoxItem Content="黄色"/>
            <ListBoxItem Content="紫色"/>
        </ListBox>
        <TextBlock x:Name="ColorStatus" Text="选中的颜色: 无" Margin="0,10,0,0"/>

    </StackPanel>
</Window>
```



C#

```
// MainWindow.xaml.cs
using System.Windows;
using System.Windows.Controls;

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        // CheckBox 事件处理
        private void AgreeCheckBox_Checked(object sender, RoutedEventArgs e)
        {
            CheckBoxStatus.Text = "状态: 已同意";
        }

        private void AgreeCheckBox_Unchecked(object sender, RoutedEventArgs e)
        {
            CheckBoxStatus.Text = "状态: 未同意";
        }

        // RadioButton 事件处理
        private void GenderRadioButton_Checked(object sender, RoutedEventArgs e)
        {
            RadioButton radioButton = sender as RadioButton; // 获取触发事件的 RadioButton
            if (radioButton != null && radioButton.IsChecked == true)
            {
                GenderStatus.Text = $"性别: {radioButton.Content}";
            }
        }

        // ComboBox 事件处理
        private void CityComboBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            // 获取选中的 ComboBoxItem 的内容
            if (CityComboBox.SelectedItem is ComboBoxItem selectedItem)
            {
                CityStatus.Text = $"城市: {selectedItem.Content}";
            }
        }

        // ListBox 事件处理
        private void ColorListBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            // 获取选中的 ListBoxItem 的内容
            if (ColorListBox.SelectedItem is ListBoxItem selectedItem)
            {
                ColorStatus.Text = $"选中的颜色: {selectedItem.Content}";
            }
            else
            {
                ColorStatus.Text = "选中的颜色: 无";
            }
        }
    }
}
```

**代码解析：**

- `GroupName="Gender"`：`RadioButton` 使用 `GroupName` 属性来定义一组互斥的选项。
- `IsChecked="True"`：设置 `RadioButton` 或 `CheckBox` 的初始选中状态。
- `SelectionChanged` 事件：`ComboBox` 和 `ListBox` 在选择项改变时触发此事件。
- `sender as RadioButton` 或 `CityComboBox.SelectedItem is ComboBoxItem selectedItem`：在事件处理程序中，`sender` 参数是触发事件的控件本身。你可以将其强制转换为特定类型以访问其属性。`is` 关键字用于类型检查和模式匹配，更安全。
- 



#### 3.4 图像 (`Image`)



用于在 UI 中显示图像。

**示例代码：**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="图像示例" Height="300" Width="400">
    <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
        <Image Source="myimage.png" Width="200" Height="150" Margin="10"/>
        </StackPanel>
</Window>
```

**重要：**

- 要使 `Image` 控件显示本地图片，你需要将图片文件（例如 `myimage.png`）添加到你的 WPF 项目中。
- 在 **解决方案资源管理器** 中，右键点击你的项目 -> **添加** -> **现有项...**，选择你的图片文件。
- 选中你添加的图片文件，在 **属性窗口** 中，将 **“生成操作”** (Build Action) 设置为 **“内容”** (Content)，将 **“复制到输出目录”** (Copy to Output Directory) 设置为 **“如果较新则复制”** (Copy if newer) 或 **“始终复制”** (Copy always)。

#### 3.5 消息框 (`MessageBox`)

`MessageBox` 类用于显示简单的对话框，向用户显示信息或获取简单的用户输入。

**示例代码：**

C#

```
// 在任意 C# 事件处理程序或方法中调用
// 消息框只会在点击确定后继续执行
MessageBox.Show("这是一个简单的消息。", "标题", MessageBoxButton.OK, MessageBoxImage.Information);

// 带有 Yes/No 按钮的消息框，并获取用户选择
MessageBoxResult result = MessageBox.Show("你确定要删除吗？", "确认删除", MessageBoxButton.YesNo, MessageBoxImage.Question);
if (result == MessageBoxResult.Yes)
{
    // 用户点击了 Yes
    MessageBox.Show("已删除！");
}
else
{
    // 用户点击了 No
    MessageBox.Show("取消删除。");
}
```

### 章节四：数据绑定 (Data Binding)

**数据绑定** 是 WPF 最强大、最核心的特性之一。它允许你将 UI 元素（View）的属性连接到 C# 代码（ViewModel 或 Model）中的数据（Data Source）属性。当数据源改变时，UI 会自动更新；当用户在 UI 中修改数据时，数据源也可以自动更新。

数据绑定大大减少了手动编写代码来同步 UI 和数据的需求，降低了复杂性，提高了开发效率和可维护性。

#### 4.1 数据绑定的基本概念

- **数据源 (Source)：** 包含数据的对象，通常是 C# 类的一个实例。数据源的属性必须是 **公共属性** (Public Properties)。
- **目标 (Target)：** UI 元素（如 `TextBlock`、`TextBox`、`Button` 等）的属性，例如 `TextBlock.Text`、`TextBox.Text`。
- **绑定路径 (Path)：** 数据源中属性的名称，指定要绑定到目标属性的数据。
- 绑定模式 (Mode)：
  - `OneWay` (默认对只读 UI 属性)：数据从数据源流向目标。当数据源属性改变时，目标属性会自动更新。
  - `TwoWay` (默认对可编辑 UI 属性，如 `TextBox.Text`)：数据在数据源和目标之间双向流动。数据源或目标属性改变时，另一方都会自动更新。
  - `OneTime`：数据只从数据源流向目标一次。
  - `OneWayToSource`：数据从目标流向数据源。
- **数据上下文 (DataContext)：** 在 WPF 中，你可以为任何 UI 元素设置一个 `DataContext` 属性。这个属性指定了该元素及其子元素的数据源。当在 XAML 中使用绑定时，如果没有明确指定 `Source`，绑定引擎会从 `DataContext` 中查找数据。

#### 4.2 简单数据绑定示例

让我们创建一个简单的例子，一个 `TextBox` 用于输入姓名，一个 `TextBlock` 用于显示问候语。

**Step 1: 定义一个简单的 C# 类 (Model/ViewModel 雏形)**

C#

```
// Person.cs (可以添加到项目根目录，或者创建一个 Models 文件夹)
using System.ComponentModel; // 引入 INotifyPropertyChanged 命名空间

namespace MyWPFApp.Models
{
    // 实现 INotifyPropertyChanged 接口，以便在属性值改变时通知 UI
    public class Person : INotifyPropertyChanged
    {
        private string _name;
        public string Name
        {
            get { return _name; }
            set
            {
                if (_name != value)
                {
                    _name = value;
                    OnPropertyChanged(nameof(Name)); // 通知 UI Name 属性已改变
                    OnPropertyChanged(nameof(Greeting)); // 也要通知 Greeting 属性改变
                }
            }
        }

        public string Greeting
        {
            get { return $"你好，{Name}！"; }
        }

        // INotifyPropertyChanged 接口的实现
        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

**代码解析：**

- `Person` 类：这是我们的数据模型。
- `INotifyPropertyChanged` 接口：**非常重要！** 当你希望数据源的属性改变时，UI 也能自动更新，你的数据源类必须实现这个接口。
- `PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));`：这是 `INotifyPropertyChanged` 的实现细节。当 `Name` 属性的 `set` 方法被调用时，我们会调用这个方法，并传入属性名，通知订阅者（这里是 UI）`Name` 属性发生了变化。

**Step 2: 修改 `MainWindow.xaml`**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="clr-namespace:MyWPFApp.Models" Title="数据绑定示例" Height="250" Width="400">
    <Grid Margin="20">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <TextBlock Grid.Row="0" Text="请输入你的名字：" FontSize="18" Margin="0,0,0,10"/>
        <TextBox Grid.Row="1" Width="250" HorizontalAlignment="Left" FontSize="16"
                 Text="{Binding Name, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"/> <TextBlock Grid.Row="2" Margin="0,10,0,0" FontSize="24" FontWeight="Bold"
                   Text="{Binding Greeting}"/> </Grid>
</Window>
```

**代码解析：**

- `xmlns:local="clr-namespace:MyWPFApp.Models"`：你需要添加这个命名空间声明，以便在 XAML 中引用你的 `Person` 类。

- ```
  Text="{Binding Name, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"
  ```

  ：

  - `{Binding Name}`：这是一个绑定表达式，表示将 `TextBox.Text` 属性绑定到数据上下文中的 `Name` 属性。
  - `Mode=TwoWay`：指定双向绑定。当 `TextBox` 中的文本改变时，`Person` 对象的 `Name` 属性也会更新；当 `Person` 对象的 `Name` 属性在 C# 中改变时，`TextBox` 的文本也会更新。
  - `UpdateSourceTrigger=PropertyChanged`：指定数据源更新的时机。默认情况下，`TextBox` 的绑定是在失去焦点时更新数据源。`PropertyChanged` 表示只要 `TextBox` 的文本改变，就立即更新数据源。

- `Text="{Binding Greeting}"`：将 `TextBlock.Text` 绑定到数据上下文中的 `Greeting` 属性。这是一个 `OneWay` 绑定（因为 `TextBlock` 是只读的），当 `Name` 改变时，`Greeting` 也会自动更新。

**Step 3: 修改 `MainWindow.xaml.cs` (设置 `DataContext`)**

C#

```
// MainWindow.xaml.cs
using System.Windows;
using MyWPFApp.Models; // 引入 Model 命名空间

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        private Person _person; // 私有字段用于存储 Person 对象

        public MainWindow()
        {
            InitializeComponent();

            _person = new Person { Name = "WPF 用户" }; // 创建 Person 对象并初始化 Name
            this.DataContext = _person; // 将 Person 对象设置为窗口的数据上下文
        }
    }
}
```

**代码解析：**

- `this.DataContext = _person;`：这是关键一步！它将 `_person` 对象设置为 `MainWindow` 的数据上下文。这意味着 `MainWindow` 中所有未指定 `Source` 的绑定都将从 `_person` 对象中查找属性。

**运行程序：**

运行应用程序，你会看到一个文本框和一行问候语。当你开始在文本框中输入时，下面的问候语会实时更新！这就是数据绑定的魔力。

#### 4.3 `ListBox` 和 `ObservableCollection<T>` 的数据绑定

`ListBox` 是一个常用的列表显示控件。当列表中的数据需要动态添加、删除或更新时，我们通常使用 `ObservableCollection<T>` 作为数据源，因为它能够自动通知 UI 集合的变化。



**Step 1: 定义一个 Student 类**



C#

```
// Student.cs
using System.ComponentModel;

namespace MyWPFApp.Models
{
    public class Student : INotifyPropertyChanged
    {
        private string _name;
        public string Name
        {
            get { return _name; }
            set
            {
                if (_name != value)
                {
                    _name = value;
                    OnPropertyChanged(nameof(Name));
                }
            }
        }

        private int _age;
        public int Age
        {
            get { return _age; }
            set
            {
                if (_age != value)
                {
                    _age = value;
                    OnPropertyChanged(nameof(Age));
                }
            }
        }

        public Student(string name, int age)
        {
            Name = name;
            Age = age;
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

**Step 2: 修改 `MainWindow.xaml`**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:models="clr-namespace:MyWPFApp.Models"
        Title="ListBox 数据绑定示例" Height="400" Width="500">
    <Grid Margin="20">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <StackPanel Grid.Row="0" Orientation="Horizontal" Margin="0,0,0,10">
            <TextBlock Text="姓名：" VerticalAlignment="Center"/>
            <TextBox x:Name="NameTextBox" Width="100" Margin="5,0"/>
            <TextBlock Text="年龄：" VerticalAlignment="Center"/>
            <TextBox x:Name="AgeTextBox" Width="50" Margin="5,0"/>
            <Button Content="添加学生" Width="80" Margin="10,0,0,0" Click="AddStudentButton_Click"/>
        </StackPanel>

        <ListBox Grid.Row="1" x:Name="StudentsListBox" ItemsSource="{Binding Students}"
                 DisplayMemberPath="Name" SelectionChanged="StudentsListBox_SelectionChanged"/>

        <TextBlock Grid.Row="2" x:Name="SelectedStudentTextBlock" Margin="0,10,0,0"
                   Text="选中的学生：无" FontWeight="Bold"/>
    </Grid>
</Window>
```

**代码解析：**

- `ItemsSource="{Binding Students}"`：这是将 `ListBox` 绑定到 C# 后台代码中一个名为 `Students` 的集合属性。
- `DisplayMemberPath="Name"`：指定 `ListBox` 中每个项目要显示 `Student` 对象的哪个属性（这里是 `Name`）。

**Step 3: 修改 `MainWindow.xaml.cs`**

C#

```
// MainWindow.xaml.cs
using System.Collections.ObjectModel; // 引入 ObservableCollection 命名空间
using System.Windows;
using System.Windows.Controls;
using MyWPFApp.Models;

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        // 使用 ObservableCollection<T> 作为列表数据源
        public ObservableCollection<Student> Students { get; set; }

        public MainWindow()
        {
            InitializeComponent();

            Students = new ObservableCollection<Student>();
            Students.Add(new Student("张三", 20));
            Students.Add(new Student("李四", 22));
            Students.Add(new Student("王五", 21));

            // 将窗口的数据上下文设置为自身，以便绑定到 Students 属性
            this.DataContext = this;
        }

        // 添加学生按钮点击事件
        private void AddStudentButton_Click(object sender, RoutedEventArgs e)
        {
            string name = NameTextBox.Text;
            if (int.TryParse(AgeTextBox.Text, out int age) && !string.IsNullOrWhiteSpace(name))
            {
                Students.Add(new Student(name, age));
                NameTextBox.Clear();
                AgeTextBox.Clear();
            }
            else
            {
                MessageBox.Show("请输入有效的姓名和年龄。", "错误", MessageBoxButton.OK, MessageBoxImage.Error);
            }
        }

        // ListBox 选中项改变事件
        private void StudentsListBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            if (StudentsListBox.SelectedItem is Student selectedStudent)
            {
                SelectedStudentTextBlock.Text = $"选中的学生: {selectedStudent.Name} ({selectedStudent.Age}岁)";
            }
            else
            {
                SelectedStudentTextBlock.Text = "选中的学生: 无";
            }
        }
    }
}
```

**代码解析：**

- `public ObservableCollection<Student> Students { get; set; }`: 声明一个 `ObservableCollection` 属性，它会自动通知 UI 集合的添加/删除/更新。
- `this.DataContext = this;`: 在这个例子中，我们将 `MainWindow` 自身设置为数据上下文，这样 XAML 中的绑定就可以直接访问 `MainWindow` 类的公共属性（如 `Students`）。
- `AddStudentButton_Click`：处理添加逻辑，并直接向 `Students` 集合中添加新的 `Student` 对象。由于是 `ObservableCollection`，UI 会自动更新。
- 



### 章节五：样式 (Styles) 和模板 (Templates)



样式和模板是 WPF 中用于自定义 UI 外观和行为的强大机制，它们可以帮助你实现一致的设计和高度可定制的 UI。



#### 5.1 样式 (Styles)

**样式** 允许你定义一组属性值，并将其应用于多个控件。这样可以避免重复设置相同的属性，并确保 UI 的一致性。

**示例代码：**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="样式示例" Height="300" Width="400">
    <Window.Resources>
        <Style TargetType="Button">
            <Setter Property="Width" Value="150"/>
            <Setter Property="Height" Value="40"/>
            <Setter Property="Margin" Value="10"/>
            <Setter Property="FontSize" Value="18"/>
            <Setter Property="Background" Value="LightBlue"/>
            <Setter Property="Foreground" Value="Navy"/>
            <Setter Property="FontWeight" Value="Bold"/>
            <Style.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter Property="Background" Value="DodgerBlue"/>
                </Trigger>
            </Style.Triggers>
        </Style>

        <Style x:Key="ImportantTextBlockStyle" TargetType="TextBlock">
            <Setter Property="FontSize" Value="24"/>
            <Setter Property="Foreground" Value="Red"/>
            <Setter Property="FontWeight" Value="ExtraBold"/>
        </Style>
    </Window.Resources>

    <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Text="样式化按钮示例" FontSize="20" Margin="0,0,0,20"/>
        <Button Content="按钮 1"/> <Button Content="按钮 2"/> <Button Content="按钮 3"/> <TextBlock Text="重要提示！" Style="{StaticResource ImportantTextBlockStyle}" Margin="0,20,0,0"/>
    </StackPanel>
</Window>
```

**代码解析：**

- `<Window.Resources>`：资源字典，你可以在这里定义样式、模板等资源，这些资源可以在其父元素及其子元素中使用。
- `<Style TargetType="Button">`：定义一个样式，`TargetType` 指定了该样式将应用于哪种类型的控件。如果没有 `x:Key`，它将成为该类型控件的默认样式。
- `<Setter Property="Width" Value="150"/>`：`Setter` 用于设置控件的属性值。
- `<Style x:Key="ImportantTextBlockStyle" TargetType="TextBlock">`：通过 `x:Key` 属性为样式命名。这样，你就可以使用 `Style="{StaticResource ImportantTextBlockStyle}"` 来将样式应用于特定的控件。
- **触发器 (Triggers)：** `Style.Triggers` 允许你定义当某个条件（如属性值改变、事件发生）满足时，应用额外的样式设置。在示例中，当 `Button` 的 `IsMouseOver` 属性为 `True` 时，背景颜色会改变。
- 



#### 5.2 控件模板 (Control Templates)



**控件模板** 允许你完全重新定义控件的视觉结构和外观，而不改变其行为。例如，你可以让一个按钮看起来像一个图片，但仍然保留按钮的点击功能。

**示例代码：** (这是一个相对复杂的概念，这里只提供一个简单示例让你感受其作用)

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="控件模板示例" Height="250" Width="400">
    <Window.Resources>
        <ControlTemplate x:Key="CustomButtonTemplate" TargetType="Button">
            <Border Background="{TemplateBinding Background}"
                    BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}"
                    CornerRadius="5">
                <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}"
                                  VerticalAlignment="{TemplateBinding VerticalContentAlignment}"/>
            </Border>
            <ControlTemplate.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter TargetName="border" Property="Background" Value="LightGreen"/>
                </Trigger>
            </ControlTemplate.Triggers>
        </ControlTemplate>
    </Window.Resources>

    <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Text="自定义按钮模板" FontSize="20" Margin="0,0,0,20"/>
        <Button Content="点击我"
                Template="{StaticResource CustomButtonTemplate}"
                Background="LightBlue" BorderBrush="Blue" BorderThickness="2"
                Width="150" Height="50" Click="Button_Click"/>
    </StackPanel>
</Window>
```

代码段

```
// MainWindow.xaml.cs
using System.Windows;

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("自定义模板的按钮被点击了！");
        }
    }
}
```

**代码解析：**

- `<ControlTemplate x:Key="CustomButtonTemplate" TargetType="Button">`：定义一个名为 `CustomButtonTemplate` 的 `ControlTemplate`，它适用于 `Button` 类型。
- `<Border>`：在模板中，我们使用了 `Border` 控件来定义按钮的形状和边框。
- `{TemplateBinding Background}`：`TemplateBinding` 是一个特殊的绑定，用于将模板内部的属性绑定到应用该模板的控件本身的属性。这意味着当你设置按钮的 `Background` 属性时，这个值会被应用到模板内部的 `Border` 的 `Background`。
- `<ContentPresenter>`：这个元素是必须的！它用于显示控件的“内容”。对于 `Button`，它的 `Content` 属性（如“点击我”）会显示在这里。
- 
- `Template="{StaticResource CustomButtonTemplate}"`：将自定义模板应用于按钮。
- 



#### 5.3 数据模板 (Data Templates)



**数据模板** 定义了如何显示数据对象在 UI 控件中（如 `ListBox`、`ComboBox`、`ContentControl`）的视觉呈现。这在显示自定义数据集合时非常有用。

**示例代码：**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:models="clr-namespace:MyWPFApp.Models"
        Title="数据模板示例" Height="400" Width="500">
    <Window.Resources>
        <DataTemplate DataType="{x:Type models:Student}">
            <Grid Margin="5">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="Auto"/>
                    <ColumnDefinition Width="*"/>
                    <ColumnDefinition Width="Auto"/>
                </Grid.ColumnDefinitions>
                <Grid.RowDefinitions>
                    <RowDefinition Height="Auto"/>
                    <RowDefinition Height="Auto"/>
                </Grid.RowDefinitions>

                <TextBlock Grid.Row="0" Grid.Column="0" Text="姓名: " FontWeight="Bold"/>
                <TextBlock Grid.Row="0" Grid.Column="1" Text="{Binding Name}" Margin="5,0,0,0"/>

                <TextBlock Grid.Row="1" Grid.Column="0" Text="年龄: " FontWeight="Bold"/>
                <TextBlock Grid.Row="1" Grid.Column="1" Text="{Binding Age}" Margin="5,0,0,0"/>

                <Button Grid.Row="0" Grid.RowSpan="2" Grid.Column="2" Content="详情" Width="60" Height="30"
                        Margin="10,0,0,0" Click="StudentDetails_Click"/>
            </Grid>
        </DataTemplate>
    </Window.Resources>

    <Grid Margin="20">
        <Grid.RowDefinitions>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>

        <ListBox Grid.Row="0" x:Name="StudentsListBox" ItemsSource="{Binding Students}"
                 SelectionChanged="StudentsListBox_SelectionChanged"/>

        <TextBlock Grid.Row="1" x:Name="SelectedStudentDetails" Margin="0,10,0,0"
                   Text="选中的学生详情: 无" FontWeight="Bold"/>
    </Grid>
</Window>
```



C#

```
// MainWindow.xaml.cs
using System.Collections.ObjectModel;
using System.Windows;
using System.Windows.Controls;
using MyWPFApp.Models; // 确保引入 Student 类所在的命名空间

namespace MyWPFApp
{
    public partial class MainWindow : Window
    {
        public ObservableCollection<Student> Students { get; set; }

        public MainWindow()
        {
            InitializeComponent();

            Students = new ObservableCollection<Student>
            {
                new Student("陈明", 20),
                new Student("林芳", 22),
                new Student("赵刚", 21),
                new Student("孙丽", 23)
            };

            this.DataContext = this;
        }

        private void StudentsListBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            if (StudentsListBox.SelectedItem is Student selectedStudent)
            {
                SelectedStudentDetails.Text = $"选中的学生详情: 姓名: {selectedStudent.Name}, 年龄: {selectedStudent.Age}岁";
            }
            else
            {
                SelectedStudentDetails.Text = "选中的学生详情: 无";
            }
        }

        private void StudentDetails_Click(object sender, RoutedEventArgs e)
        {
            // 获取点击按钮所在的 DataContext (即对应的 Student 对象)
            Button button = sender as Button;
            if (button != null)
            {
                Student student = button.DataContext as Student;
                if (student != null)
                {
                    MessageBox.Show($"学生姓名: {student.Name}\n学生年龄: {student.Age}", "学生详情", MessageBoxButton.OK, MessageBoxImage.Information);
                }
            }
        }
    }
}
```

**代码解析：**

- `<DataTemplate DataType="{x:Type models:Student}">`：这定义了一个数据模板，它将应用于所有类型为 `models:Student` 的数据对象。当 `ListBox` 发现其 `ItemsSource` 中的元素是 `Student` 类型时，它会使用这个模板来渲染每个 `Student` 对象。
- 在 `DataTemplate` 内部，你可以像构建普通 UI 一样使用布局面板和控件，并通过 `{Binding PropertyName}` 来绑定 `Student` 对象的属性。
- `StudentDetails_Click`：在这个事件处理程序中，我们通过 `button.DataContext as Student` 来获取触发点击事件的按钮所绑定的 `Student` 对象。这是在数据模板中获取数据模型的重要技巧。

### 章节六：MVVM (Model-View-ViewModel) 模式初步

MVVM 模式是 WPF 应用程序开发中最推荐的架构模式。它有助于实现代码的清晰分离，提高可测试性、可维护性和可扩展性。

**MVVM 的核心组件：**

- **Model (模型)：** 代表应用程序的数据和业务逻辑。通常是 POCO (Plain Old C# Objects) 类，不依赖于 UI 层。
- **View (视图)：** 用户界面，通常是 XAML 文件。它负责显示数据和接收用户输入。View 不包含任何业务逻辑，只通过数据绑定和命令绑定与 ViewModel 交互。
- **ViewModel (视图模型)：** 连接 View 和 Model 的桥梁。它暴露 Model 中的数据供 View 绑定，并处理 View 的交互逻辑（通过命令）。ViewModel 不直接引用 View，而是通过数据绑定和 `INotifyPropertyChanged` 来通知 View 数据变化。

**MVVM 的优势：**

- **分离关注点：** View、ViewModel 和 Model 各司其职，互不依赖。
- **可测试性：** ViewModel 不依赖 UI，因此可以独立进行单元测试。
- **可维护性：** 更改 UI 或业务逻辑不会相互影响。
- **团队协作：** UI 设计师和开发者可以并行工作。

#### 6.1 实现 MVVM 模式的准备

为了更好地实现 MVVM，我们通常会用到以下工具：

- **`INotifyPropertyChanged`：** 确保 Model 和 ViewModel 中的属性在改变时能通知 View。
- 
- **`ICommand`：** 用于将 View 中的 UI 事件（如按钮点击）绑定到 ViewModel 中的方法。
- 



我们将创建一个简单的计数器应用来演示 MVVM。



**Step 1: 创建 Model (CountModel.cs)**



C#

```
// Models/CountModel.cs
using System.ComponentModel;

namespace MyWPFApp.Models
{
    public class CountModel : INotifyPropertyChanged
    {
        private int _count;
        public int Count
        {
            get { return _count; }
            set
            {
                if (_count != value)
                {
                    _count = value;
                    OnPropertyChanged(nameof(Count));
                }
            }
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

**Step 2: 创建 ViewModel (CounterViewModel.cs)**

C#

```
// ViewModels/CounterViewModel.cs
using System.Windows.Input; // 引入 ICommand 命名空间
using MyWPFApp.Models;
using MyWPFApp.Commands; // 假设你将 RelayCommand 放在这个命名空间下

namespace MyWPFApp.ViewModels
{
    public class CounterViewModel : BaseViewModel // 继承一个基类，通常用于实现 INotifyPropertyChanged
    {
        private CountModel _model; // ViewModel 引用 Model

        public CounterViewModel()
        {
            _model = new CountModel { Count = 0 };
            IncrementCommand = new RelayCommand(Increment); // 绑定命令到方法
            DecrementCommand = new RelayCommand(Decrement);
        }

        public int CurrentCount
        {
            get { return _model.Count; }
            set
            {
                // 注意：这里通常不会直接设置 Model 的属性，而是通过命令来修改
                // 但为了演示，也可以在 ViewModel 内部设置 Model
                if (_model.Count != value)
                {
                    _model.Count = value;
                    OnPropertyChanged(nameof(CurrentCount)); // 通知 UI 属性改变
                }
            }
        }

        // 定义命令
        public ICommand IncrementCommand { get; private set; }
        public ICommand DecrementCommand { get; private set; }

        // 命令执行逻辑
        private void Increment(object parameter)
        {
            CurrentCount++; // 通过属性的 set 方法更新 Model，并通知 UI
        }

        private void Decrement(object parameter)
        {
            CurrentCount--;
        }
    }

    // 为了简化，我们创建一个 BaseViewModel 用于 INotifyPropertyChanged 的实现
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void OnPropertyChanged(string propertyName)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }

    // 辅助类：RelayCommand (用于简化 ICommand 的实现)
    // 通常放在 Commands 文件夹或单独的帮助类库中
    namespace Commands
    {
        public class RelayCommand : ICommand
        {
            private readonly Action<object> _execute;
            private readonly Predicate<object> _canExecute;

            public event EventHandler CanExecuteChanged
            {
                add { CommandManager.RequerySuggested += value; }
                remove { CommandManager.RequerySuggested -= value; }
            }

            public RelayCommand(Action<object> execute, Predicate<object> canExecute = null)
            {
                _execute = execute ?? throw new ArgumentNullException(nameof(execute));
                _canExecute = canExecute;
            }

            public bool CanExecute(object parameter)
            {
                return _canExecute == null || _canExecute(parameter);
            }

            public void Execute(object parameter)
            {
                _execute(parameter);
            }
        }
    }
}
```

**代码解析：**

- `CounterViewModel`：包含了 `CountModel` 的实例。

- `CurrentCount` 属性：这是一个“包装”了 `_model.Count` 的属性，它负责将 Model 的数据暴露给 View，并处理 `INotifyPropertyChanged` 通知。

- ```
  ICommand
  ```

   和 

  ```
  RelayCommand
  ```

  ：

  - 
  - `ICommand` 是一个接口，定义了 `Execute` (执行命令) 和 `CanExecute` (判断命令是否可执行) 方法。
  - 
  - `RelayCommand` 是一个自定义的 `ICommand` 实现，它是一个通用的命令，可以接收一个 `Action` 作为执行逻辑。这避免了为每个命令都编写一个完整的类。`CommandManager.RequerySuggested` 用于通知 WPF 重新评估 `CanExecute` 方法。

**Step 3: 修改 `MainWindow.xaml`**

XML

```
<Window x:Class="MyWPFApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:vm="clr-namespace:MyWPFApp.ViewModels" Title="MVVM 计数器示例" Height="250" Width="400">
    <Window.DataContext>
        <vm:CounterViewModel/>
    </Window.DataContext>

    <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Text="当前计数：" FontSize="24" Margin="0,0,0,10"/>
        <TextBlock Text="{Binding CurrentCount}" FontSize="48" FontWeight="Bold" Margin="0,0,0,20"/>

        <StackPanel Orientation="Horizontal">
            <Button Content="增加" Width="100" Height="40" FontSize="18" Margin="0,0,10,0"
                    Command="{Binding IncrementCommand}"/> <Button Content="减少" Width="100" Height="40" FontSize="18"
                    Command="{Binding DecrementCommand}"/> </StackPanel>
    </StackPanel>
</Window>
```

**代码解析：**

- `<Window.DataContext><vm:CounterViewModel/></Window.DataContext>`：这是 MVVM 中常见的做法。在 XAML 中直接实例化 `CounterViewModel` 并将其设置为窗口的 `DataContext`。这样，窗口中的所有绑定就都可以直接指向 `CounterViewModel` 的属性和命令。
- `Text="{Binding CurrentCount}"`：`TextBlock` 绑定到 ViewModel 的 `CurrentCount` 属性。
- 
- `Command="{Binding IncrementCommand}"` 和 `Command="{Binding DecrementCommand}"`: `Button` 使用 `Command` 属性绑定到 ViewModel 中的 `ICommand`。当按钮被点击时，`Command` 会调用其 `Execute` 方法。
- 



**Step 4: 清理 `MainWindow.xaml.cs` (只保留必要的代码)**

C#

```
// MainWindow.xaml.cs
using System.Windows;

namespace MyWPFApp
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            // 在 MVVM 模式下，通常不在后台代码中直接操作 UI 元素，
            // 而是通过 DataContext 和数据绑定来连接 View 和 ViewModel。
            // 因此，这里不再需要设置 DataContext，因为它已经在 XAML 中完成了。
        }
    }
}
```

**运行程序：**

运行应用程序，你会看到一个显示“当前计数”的窗口和两个按钮。点击“增加”或“减少”按钮，计数会实时更新，而你没有在 C# 后台代码中编写任何直接操作 UI 的逻辑！这就是 MVVM 的力量。

### 章节七：部署你的 WPF 应用程序

当你完成 WPF 应用程序的开发后，你需要将其部署给其他用户使用。

#### 7.1 发布应用程序

Visual Studio 提供了一个方便的发布功能，可以将你的应用程序打包成可执行文件或其他安装格式。

**操作步骤：**

1. 在 **解决方案资源管理器** 中，右键点击你的 WPF 项目（例如 `MyWPFApp`）。
2. 选择 **“发布”** (Publish...)。
3. 选择发布目标：
   - **文件夹：** 最简单的方式，将应用程序文件发布到本地文件夹，然后你可以手动复制这些文件给用户。
   - **ClickOnce：** 用于 Web 或网络共享部署，支持自动更新。
   - **Microsoft Store：** 发布到 Windows 应用商店。
   - **FTP/Web 服务器：** 直接发布到远程服务器。
   - 对于初学者，**“文件夹”** 是最直接和易于理解的选项。
4. 选择目标位置（输出文件夹）。
5. 点击 **“下一步”**。
6. 选择部署模式：
   - **框架依赖 (Framework-dependent)：** 应用程序需要用户安装相应版本的 .NET 运行时才能运行。这种方式生成的包较小。
   - **独立 (Self-contained)：** 应用程序包含所有必要的 .NET 运行时组件，无需用户额外安装 .NET。这种方式生成的包较大，但方便分发。
   - 对于初学者，选择 **“独立”** 更简单，因为它减少了用户的安装步骤。
7. 选择目标运行时（Target Runtime），例如 `win-x64` (64位 Windows)。
8. 点击 **“完成”**。
9. 点击 **“发布”** 按钮。

Visual Studio 会编译你的应用程序，并将发布文件放在你指定的文件夹中（通常在项目的 `bin\Release\netX.Y\publish` 路径下，其中 `X.Y` 是你的 .NET 版本）。你可以将这个文件夹复制到其他 Windows 电脑上运行。

**分发给用户：**

将发布文件夹中的所有文件（包括 `.exe` 文件）复制到目标计算机上。用户可以直接双击 `.exe` 文件来运行你的应用程序。

### 总结与展望

恭喜你完成了这份 WPF 初学者学习手册！你已经掌握了以下核心概念：

- WPF 的基本特性和优势。
- XAML 语法以及如何定义 UI。
- 各种布局面板（`Grid`、`StackPanel`、`DockPanel`、`WrapPanel`、`Canvas`）来组织 UI 元素。
- 常用控件（`TextBlock`、`TextBox`、`Button`、`CheckBox`、`RadioButton`、`ComboBox`、`ListBox`、`Image`）的使用和事件处理。
- **WPF 的核心功能：数据绑定，以及如何使用 `INotifyPropertyChanged` 和 `ObservableCollection<T>`。**
- 样式和模板（`Style`、`ControlTemplate`、`DataTemplate`）来自定义 UI 外观。
- **MVVM 模式** 的初步认识和实践，学习如何使用 `ICommand` 和 `RelayCommand` 实现逻辑分离。
- 如何发布你的 WPF 应用程序。

**接下来你可以继续深入学习的方面：**

- **更深入的 MVVM：** 学习更高级的 MVVM 框架（如 Prism、MVVM Light Toolkit），它们提供了更多开箱即用的功能。
- **路由事件 (Routed Events)：** 深入理解 WPF 事件的传递机制。
- **依赖属性 (Dependency Properties)：** 它是 WPF 属性系统的核心，理解它的工作原理对高级开发至关重要。
- **附加属性 (Attached Properties) 和附加事件 (Attached Events)：** 扩展控件功能的强大机制。
- **用户控件 (User Controls) 和自定义控件 (Custom Controls)：** 创建可重用的 UI 组件。
- **动画 (Animations)：** 为你的 UI 添加动态效果。
- **转换器 (Converters)：** 学习更复杂的 `IValueConverter` 应用，以及 `IMultiValueConverter`。
- **验证 (Validation)：** 如何在数据绑定中实现数据输入验证。
- **异步编程 (`async`/`await`)：** 在 WPF 应用中保持 UI 响应性的关键。
- **多线程：** 理解 UI 线程和后台线程。
- **数据库交互：** 使用 Entity Framework Core 或 ADO.NET 与数据库进行交互。
- **单元测试：** 为你的 ViewModel 编写单元测试。

**学习建议：**

- **持续练习：** 编写更多的小项目，巩固所学知识。
- **阅读官方文档：** Microsoft Learn 是最好的 WPF 学习资源。
- **分析现有项目：** 尝试理解开源 WPF 项目的代码结构和设计模式。
- **保持好奇心：** 遇到问题时，积极搜索和提问。

WPF 是一个强大而富有表现力的 UI 框架。通过不断学习和实践，你将能够构建出令人印象深刻的桌面应用程序。祝你旅途愉快！

 来源









 我已经把你之前发的c#手册看完了，基础语法我都了解了，你能写一个小项目，让我练练手吗 





太棒了！很高兴你已经学完了 C# 基础手册。现在，让我们来做一个小项目，把之前学的 WPF 和 C# 基础知识结合起来练练手。

------

## WPF 练手小项目：简单的待办事项列表应用

这个项目将带你构建一个功能简单的待办事项列表（To-Do List）应用。通过它，你将实践 WPF 的布局、控件、事件处理、数据绑定以及 `ObservableCollection` 的使用。

### 项目目标：

- 用户可以输入待办事项的名称。
- 用户可以将待办事项添加到列表中。
- 列表显示所有待办事项。
- 用户可以标记待办事项为已完成或未完成（通过一个复选框）。
- 用户可以从列表中删除待办事项。

### 项目结构概览：

我们将使用一个基本的 MVVM 思想，虽然不会完全实现所有模式，但会让你对数据与 UI 分离有初步的感受。

- **Models 文件夹：** 存放 `TodoItem` 类，代表一个待办事项的数据。
- **MainWindow.xaml：** 应用程序的主窗口，定义 UI 布局和控件。
- **MainWindow.xaml.cs：** 关联 `MainWindow.xaml` 的后台代码，处理 UI 交互逻辑。

------

### 第一步：创建 WPF 项目

1. 打开 **Visual Studio**。
2. 点击 **“创建新项目”**。
3. 搜索并选择 **“WPF 应用程序”** (C#，基于最新 .NET 版本)。
4. 项目名称输入 `SimpleTodoList`，选择一个存放位置。
5. 点击 **“创建”**。

------

### 第二步：定义数据模型 (TodoItem.cs)

我们需要一个类来表示每个待办事项。这个类需要实现 `INotifyPropertyChanged` 接口，以便当待办事项的属性（例如 `IsCompleted`）改变时，UI 能够自动更新。

1. 在 **解决方案资源管理器** 中，右键点击你的项目 `SimpleTodoList`。

2. 选择 **“添加”** -> **“新建文件夹”**，命名为 `Models`。

3. 右键点击 `Models` 文件夹 -> **“添加”** -> **“类”**。

4. 类名称输入 `TodoItem.cs`，点击 **“添加”**。

5. 将 `TodoItem.cs` 的内容替换为以下代码：

   C#

   ```
   // Models/TodoItem.cs
   using System.ComponentModel; // 引入 INotifyPropertyChanged 命名空间
   
   namespace SimpleTodoList.Models
   {
       public class TodoItem : INotifyPropertyChanged
       {
           private string _description;
           public string Description
           {
               get { return _description; }
               set
               {
                   if (_description != value)
                   {
                       _description = value;
                       OnPropertyChanged(nameof(Description));
                   }
               }
           }
   
           private bool _isCompleted;
           public bool IsCompleted
           {
               get { return _isCompleted; }
               set
               {
                   if (_isCompleted != value)
                   {
                       _isCompleted = value;
                       OnPropertyChanged(nameof(IsCompleted));
                   }
               }
           }
   
           // INotifyPropertyChanged 接口的实现
           public event PropertyChangedEventHandler PropertyChanged;
   
           protected void OnPropertyChanged(string propertyName)
           {
               PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
           }
       }
   }
   ```

   **代码解释：**

   - `Description`：待办事项的文本描述。
   - `IsCompleted`：一个布尔值，表示待办事项是否已完成。
   - `INotifyPropertyChanged`：确保 `Description` 或 `IsCompleted` 属性改变时，任何绑定到它们的 UI 元素都会被通知并更新。

------

### 第三步：设计用户界面 (MainWindow.xaml)

我们将使用 `Grid` 和 `StackPanel` 来布局，并使用 `TextBox`、`Button` 和 `ListBox` 等控件。

1. 打开 `MainWindow.xaml` 文件。

2. 将 `<Grid>` 标签内的所有内容替换为以下 XAML 代码：

   XML

   ```
   <Window x:Class="SimpleTodoList.MainWindow"
           xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
           xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
           xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
           xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
           xmlns:local="clr-namespace:SimpleTodoList"
           xmlns:models="clr-namespace:SimpleTodoList.Models"  mc:Ignorable="d"
           Title="我的待办事项" Height="500" Width="400">
       <Grid Margin="10">
           <Grid.RowDefinitions>
               <RowDefinition Height="Auto"/>      <RowDefinition Height="*"/>          <RowDefinition Height="Auto"/>      </Grid.RowDefinitions>
   
           <StackPanel Grid.Row="0" Orientation="Horizontal" Margin="5">
               <TextBox x:Name="NewTodoDescriptionTextBox" Width="250" Height="30"
                        VerticalContentAlignment="Center" FontSize="14"
                        Text="在这里输入待办事项..."/>
               <Button x:Name="AddTodoButton" Content="添加" Width="80" Height="30" Margin="10,0,0,0"
                       Click="AddTodoButton_Click"/> </StackPanel>
   
           <ListBox Grid.Row="1" x:Name="TodoListBox" Margin="5"
                    ItemsSource="{Binding Todos}"> <ListBox.ItemTemplate>
                   <DataTemplate DataType="{x:Type models:TodoItem}">
                       <Grid Margin="5">
                           <Grid.ColumnDefinitions>
                               <ColumnDefinition Width="Auto"/>  <ColumnDefinition Width="*"/>     <ColumnDefinition Width="Auto"/>  </Grid.ColumnDefinitions>
   
                           <CheckBox Grid.Column="0" IsChecked="{Binding IsCompleted, Mode=TwoWay}"
                                     VerticalAlignment="Center" Margin="0,0,10,0"/>
                           <TextBlock Grid.Column="1" Text="{Binding Description}"
                                      VerticalAlignment="Center" FontSize="16"
                                      TextWrapping="Wrap">
                               <TextBlock.Style>
                                   <Style TargetType="TextBlock">
                                       <Style.Triggers>
                                           <DataTrigger Binding="{Binding IsCompleted}" Value="True">
                                               <Setter Property="TextDecorations" Value="Strikethrough"/>
                                               <Setter Property="Foreground" Value="Gray"/>
                                           </DataTrigger>
                                       </Style.Triggers>
                                   </Style>
                               </TextBlock.Style>
                           </TextBlock>
                           <Button Grid.Column="2" Content="删除" Width="60" Height="25" Margin="10,0,0,0"
                                   Click="DeleteTodoButton_Click"/> </Grid>
                   </DataTemplate>
               </ListBox.ItemTemplate>
           </ListBox>
   
           <StackPanel Grid.Row="2" Orientation="Horizontal" HorizontalAlignment="Right" Margin="5">
               <TextBlock Text="总数: " FontSize="14"/>
               <TextBlock x:Name="TotalItemsTextBlock" Text="0" FontSize="14"/>
               <TextBlock Text=" | 完成: " FontSize="14" Margin="10,0,0,0"/>
               <TextBlock x:Name="CompletedItemsTextBlock" Text="0" FontSize="14"/>
           </StackPanel>
       </Grid>
   </Window>
   ```

   **代码解释：**

   - `xmlns:models="clr-namespace:SimpleTodoList.Models"`：引入 `TodoItem` 类所在的命名空间。

   - 顶部的 StackPanel：

      包含一个 

     ```
     TextBox
     ```

      用于输入新待办事项，一个 

     ```
     Button
     ```

      用于添加。

     - `x:Name="NewTodoDescriptionTextBox"`：给 `TextBox` 命名，以便在 C# 代码中引用。
     - `Click="AddTodoButton_Click"`：将按钮的 `Click` 事件连接到 C# 后台代码中的一个方法。

   - `ListBox`：

      用于显示待办事项列表。

     - `x:Name="TodoListBox"`：给 `ListBox` 命名。

     - `ItemsSource="{Binding Todos}"`：这是一个关键的数据绑定！它告诉 `ListBox` 去查找 `DataContext` 中一个名为 `Todos` 的属性，并将其作为列表的数据源。

     - `ListBox.ItemTemplate` 和 `DataTemplate`：

        这是数据模板。它定义了 

       ```
       ListBox
       ```

        中每个 

       ```
       TodoItem
       ```

        对象应该如何被视觉呈现。

       - `DataType="{x:Type models:TodoItem}"`：表示这个模板应用于 `TodoItem` 类型的对象。

       - 在 

         ```
         DataTemplate
         ```

          内部，我们用 

         ```
         Grid
         ```

          来布局每个待办事项：

         - `CheckBox`：`IsChecked="{Binding IsCompleted, Mode=TwoWay}"` 实现了双向绑定。当用户勾选或取消勾选复选框时，`TodoItem` 对象的 `IsCompleted` 属性会自动更新；反之，如果 `IsCompleted` 属性在代码中改变，复选框也会更新。
         - `TextBlock`：`Text="{Binding Description}"` 绑定到 `TodoItem` 的 `Description` 属性。
         - **`TextBlock.Style` 和 `DataTrigger`：** 这是一个小技巧！当 `IsCompleted` 为 `True` 时，文本会显示删除线并变灰。
         - `Button`：每个待办事项都有一个“删除”按钮，绑定了 `Click="DeleteTodoButton_Click"` 事件。

------

### 第四步：编写后台代码 (MainWindow.xaml.cs)

现在，我们将实现 UI 的交互逻辑，包括添加、删除待办事项，并维护 `ObservableCollection`。

1. 打开 `MainWindow.xaml.cs` 文件。

2. 将文件的内容替换为以下代码：

   C#

   ```
   // MainWindow.xaml.cs
   using System.Collections.ObjectModel; // 引入 ObservableCollection 命名空间
   using System.ComponentModel; // 引入 INotifyPropertyChanged 命名空间
   using System.Linq; // 引入 Linq 命名空间，用于 Count
   using System.Windows;
   using System.Windows.Controls;
   using SimpleTodoList.Models; // 引入 TodoItem 所在的命名空间
   
   namespace SimpleTodoList
   {
       /// <summary>
       /// Interaction logic for MainWindow.xaml
       /// </summary>
       public partial class MainWindow : Window, INotifyPropertyChanged // MainWindow 自身也实现 INotifyPropertyChanged
       {
           // ObservableCollection 能够自动通知 UI 集合的变化 (添加/删除/移动)
           public ObservableCollection<TodoItem> Todos { get; set; }
   
           // 用于统计信息的属性
           private int _totalItems;
           public int TotalItems
           {
               get { return _totalItems; }
               set
               {
                   if (_totalItems != value)
                   {
                       _totalItems = value;
                       OnPropertyChanged(nameof(TotalItems));
                   }
               }
           }
   
           private int _completedItems;
           public int CompletedItems
           {
               get { return _completedItems; }
               set
               {
                   if (_completedItems != value)
                   {
                       _completedItems = value;
                       OnPropertyChanged(nameof(CompletedItems));
                   }
               }
           }
   
   
           public MainWindow()
           {
               InitializeComponent();
   
               // 初始化 Todos 集合
               Todos = new ObservableCollection<TodoItem>();
               // 为了演示，添加一些初始数据
               Todos.Add(new TodoItem { Description = "学习 WPF 基础", IsCompleted = false });
               Todos.Add(new TodoItem { Description = "完成待办事项小项目", IsCompleted = false });
               Todos.Add(new TodoItem { Description = "购买食材", IsCompleted = true });
   
               // 将窗口的数据上下文设置为自身，以便 XAML 中的绑定能够找到 Todos 属性
               this.DataContext = this;
   
               // 订阅集合的 ItemChanged 事件，以便在 TodoItem 属性改变时更新统计信息
               // 注意：ObservableCollection 本身不提供 ItemChanged 事件，我们需要手动处理
               // 更常见的做法是在 ViewModel 中处理，但这里为了简化，直接在后台代码处理
               Todos.CollectionChanged += Todos_CollectionChanged;
               foreach (var item in Todos)
               {
                   item.PropertyChanged += TodoItem_PropertyChanged;
               }
   
               UpdateStatistics(); // 首次加载时更新统计信息
           }
   
           // 当 Todos 集合发生变化时触发
           private void Todos_CollectionChanged(object sender, System.Collections.Specialized.NotifyCollectionChangedEventArgs e)
           {
               // 处理添加的项
               if (e.NewItems != null)
               {
                   foreach (TodoItem item in e.NewItems)
                   {
                       item.PropertyChanged += TodoItem_PropertyChanged; // 订阅新添加项的属性改变事件
                   }
               }
               // 处理删除的项
               if (e.OldItems != null)
               {
                   foreach (TodoItem item in e.OldItems)
                   {
                       item.PropertyChanged -= TodoItem_PropertyChanged; // 取消订阅已删除项的属性改变事件
                   }
               }
               UpdateStatistics();
           }
   
           // 当 TodoItem 的属性发生变化时触发 (例如 IsCompleted 改变)
           private void TodoItem_PropertyChanged(object sender, PropertyChangedEventArgs e)
           {
               if (e.PropertyName == nameof(TodoItem.IsCompleted))
               {
                   UpdateStatistics();
               }
           }
   
           // 更新底部统计信息的私有方法
           private void UpdateStatistics()
           {
               TotalItems = Todos.Count;
               CompletedItems = Todos.Count(item => item.IsCompleted);
   
               // 更新 UI 上的 TextBlock
               TotalItemsTextBlock.Text = TotalItems.ToString();
               CompletedItemsTextBlock.Text = CompletedItems.ToString();
           }
   
           // “添加”按钮的点击事件处理程序
           private void AddTodoButton_Click(object sender, RoutedEventArgs e)
           {
               string description = NewTodoDescriptionTextBox.Text.Trim(); // 获取输入文本并去除前后空格
   
               if (!string.IsNullOrWhiteSpace(description) && description != "在这里输入待办事项...")
               {
                   TodoItem newItem = new TodoItem { Description = description, IsCompleted = false };
                   Todos.Add(newItem); // 添加到 ObservableCollection，UI 会自动更新
   
                   NewTodoDescriptionTextBox.Clear(); // 清空输入框
                   NewTodoDescriptionTextBox.Text = "在这里输入待办事项..."; // 重新设置提示文本
               }
               else
               {
                   MessageBox.Show("请输入有效的待办事项描述！", "提示", MessageBoxButton.OK, MessageBoxImage.Warning);
               }
           }
   
           // “删除”按钮的点击事件处理程序 (在 DataTemplate 内部)
           private void DeleteTodoButton_Click(object sender, RoutedEventArgs e)
           {
               // 获取触发事件的按钮
               Button deleteButton = sender as Button;
               if (deleteButton != null)
               {
                   // 获取按钮所在的 DataContext，即对应的 TodoItem 对象
                   TodoItem itemToDelete = deleteButton.DataContext as TodoItem;
   
                   if (itemToDelete != null)
                   {
                       // 从集合中移除 TodoItem，UI 会自动更新
                       Todos.Remove(itemToDelete);
                   }
               }
           }
   
           // MainWindow 自身实现 INotifyPropertyChanged 的事件
           public event PropertyChangedEventHandler PropertyChanged;
   
           protected void OnPropertyChanged(string propertyName)
           {
               PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
           }
       }
   }
   ```

   **代码解释：**

   - `public ObservableCollection<TodoItem> Todos { get; set; }`：声明一个 `ObservableCollection` 类型的属性 `Todos`，它将作为 `ListBox` 的数据源。`ObservableCollection` 的好处是，当你向其中添加、删除或移动元素时，`ListBox` 会自动响应并更新 UI。

   - `this.DataContext = this;`：将 `MainWindow` 自身设置为窗口的 `DataContext`。这意味着 XAML 中的 `ItemsSource="{Binding Todos}"` 会在 `MainWindow` 类中查找名为 `Todos` 的公共属性。

   - `AddTodoButton_Click`：

     - 获取 `NewTodoDescriptionTextBox.Text`。
     - `string.IsNullOrWhiteSpace(description)`：检查文本是否为空或只包含空格。
     - 创建新的 `TodoItem` 对象。
     - `Todos.Add(newItem);`：将新项目添加到 `ObservableCollection`。由于 `ObservableCollection` 的特性，`ListBox` 会自动显示新添加的项。
     - 清空 `TextBox`。

   - `DeleteTodoButton_Click`：

     - `Button deleteButton = sender as Button;`：`sender` 参数是触发事件的控件（这里是“删除”按钮）。我们将其转换为 `Button` 类型。
     - `TodoItem itemToDelete = deleteButton.DataContext as TodoItem;`：**关键！** 在 `DataTemplate` 内部的控件（如这个删除按钮），其 `DataContext` 就是它所代表的数据对象（这里是 `TodoItem`）。通过这种方式，我们可以获取到用户想要删除的具体 `TodoItem` 对象。
     - `Todos.Remove(itemToDelete);`：从 `ObservableCollection` 中移除该项，`ListBox` 也会自动更新。

   - `UpdateStatistics()`、`Todos_CollectionChanged` 和 `TodoItem_PropertyChanged`：

      这部分是为了实现底部的统计功能。

     - `Todos.CollectionChanged += Todos_CollectionChanged;`：订阅 `ObservableCollection` 集合自身的改变事件。
     - `item.PropertyChanged += TodoItem_PropertyChanged;`：由于 `ObservableCollection` **只通知集合自身的添加/删除/移动**，而 **不通知集合中项的属性改变**，所以我们需要手动订阅每个 `TodoItem` 对象的 `PropertyChanged` 事件。这样当 `IsCompleted` 改变时，我们也能更新统计信息。
     - `UpdateStatistics()`：负责计算总数和完成数，并更新底部的 `TextBlock`。

------

### 第五步：运行和测试

1. 在 Visual Studio 中，按下 **F5** 键或点击工具栏上的 **“启动”** 按钮。
2. 你的待办事项列表应用窗口将出现。
3. 测试功能：
   - 在文本框中输入新的待办事项，点击 **“添加”** 按钮。
   - 尝试勾选或取消勾选列表中的待办事项旁边的复选框。
   - 点击每个待办事项旁边的 **“删除”** 按钮。
   - 观察底部统计信息是否实时更新。