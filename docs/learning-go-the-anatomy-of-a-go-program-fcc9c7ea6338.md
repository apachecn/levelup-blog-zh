# 学习围棋:围棋程序剖析

> 原文：<https://levelup.gitconnected.com/learning-go-the-anatomy-of-a-go-program-fcc9c7ea6338>

![](img/67fa6c64dc878ab4e4fbeb17591d54bb.png)

潘卡杰·帕特尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在这篇文章中，我将讨论围棋程序的组成部分。我在本文中讨论的大部分内容都可以在艾伦·多诺万和布莱恩·克尼根所著的《T4:围棋编程语言》一书中找到。

出于讨论的目的，我们将使用一个简单的“你好，世界！”程序为例。代码如下:

```
package mainimport "fmt"func main() {
  fmt.Println("Hello, world!")
}
```

所有 Go 程序都包含在*包*中。包就像 C++中的库或 JavaScript 或 Python 中的模块。每个 Go 程序的第一行表示该程序属于哪个包。像 C 和 C++一样，Go 有一个小的核心语言，它提供了很多你需要的功能，比如输入和输出、图形、处理文本等等。，来自一个包。Go 标准库中有超过 100 个软件包。

包 main 是一个特殊的包，表示在包中找到的程序是一个可执行程序，而不是一个包含函数的库。您还会注意到该程序有一个名为 main 的函数(func 关键字是函数定义的开始)。与 C 和 C++一样，main 函数是程序开始执行的地方，所以每个 Go 项目都必须有一个 main 函数。

下一行是 import 语句，它将 fmt 包导入到程序中。这个包包括输入和输出函数，比如用来写“Hello，world！”的 Println()函数对着屏幕。与大多数其他编程语言一样，如果您想要使用库中的功能，您必须将该库导入到您的程序中。import 语句总是紧跟在包声明之后。

下一行开始我们主函数的函数定义。函数总是以关键字 func 开头，后面是函数名、参数列表(在本例中为空)、结果列表(在本例中也为空)和函数体。与 C 和 C++一样，函数体用花括号括起来。

我们将在后面详细讨论这个问题，但是请注意，开始的花括号与函数定义的开头(函数标题)在同一行。Go 要求这样，并且不能将左花括号放到下一行。这样做会导致语法错误。

这个例子中的函数体只有一行。通过编写库名、*点运算符*和函数名及其参数，从 fmt 库中调用 Println()函数。如果您不熟悉点运算符，它用于将库名与从该库中调用的函数分开。在这种情况下，它的用法很像 C++中的作用域解析操作符。

您会注意到，Go 不需要在语句(或声明，我们将在下一篇文章中看到)的结尾使用分号。在幕后，编译器会将换行符转换成某些标记后的分号，这意味着您放置换行符的位置会影响程序的正确解析。当您想在同一行上放置多个语句时，可以使用分号。

最后，main 的右花括号可以与函数中的最后一条语句在同一行，但这违反了大多数编程风格规则，所以总是将函数的右花括号放在自己的行上。

# 从这里向前看

这就结束了我对围棋程序结构的简要概述。我的下一篇文章将介绍 Go 数据类型、变量声明以及将数据导入 Go 程序的交互式输入。

请将您对这一系列关于学习 Go 编程的文章的任何意见发送给我。我想让这个系列对我的读者有用。