# 学习 Go:变量声明和 Read，Then 提示模板

> 原文：<https://levelup.gitconnected.com/learning-go-6ce86a0a1063>

![](img/a729a156d333e39c2d5b07be8ccf2918.png)

由 [Florian Olivo](https://unsplash.com/@rxspawn?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在本文中，我将讨论四种 Go 数据类型，如何声明变量，以及如何将这些信息用于 Read，Then Prompt 编程模板。

# Go 数据类型

Go 有各种各样的数据类型，从数字类型到字符串、布尔值到复合的用户定义的类型。这里我将只关注其中的一些数据类型——两种整型，两种浮点型，一种布尔型，还有一种文本类型`string`。

整数最常见的类型是`int`。Go 编译器可以将一个 int 数指定为 32 位数字或 64 位数字。还有许多其他的整数数据类型，但是在本文中我们将只关注 int。如果您想指定 32 位或 64 位，您可以使用`int32`或`int64`类型。

浮点值可以存储为`float32`或`float64`。`float32`类型提供大约六位数的精度，而`float64`提供大约十五位数的精度。大多数 Go 程序员使用`float64`是很常见的。

布尔在 Go 中用`bool`类型表示。这种类型的两个值是`true`和`false`。与 C++不同，这些是为一个`bool`变量存储的值，而不是`1`和`0`。

文本数据用`string`数据类型表示。Go 字符串是不可变的字节序列。字符串是通过将字符放在双引号中形成的。

当然，关于 Go 数据类型，我还有很多可以说的，但是与其让你陷入这些细节，我更希望我们坚持基本类型，并继续使用这些类型来创建变量。

# 转到变量名

Go 使用变量来存储数据。与任何其他编程语言一样，变量是计算机内存中存储位置的名称。在 Go 中创建变量的规则很简单。变量名应该以字母或下划线开头，名称的其余字符必须是其他字母、数字或下划线。

为了遵循 Go 编程惯例，由多个单词组成的变量名应该使用“骆驼大小写”，其中变量的第一个单词是小写的，但后续单词的第一个字母是大写的。例如，用于存储某人名字的变量可能叫做`firstName`。根据变量的范围，保持变量名简短也是一种惯例。我将在另一篇文章中更多地讨论范围。

# Go 变量声明

在 Go 中声明变量有几种方法。最常见的方式是使用所谓的*短*变量声明。短变量声明具有以下语法模板:

*变量名:=表达式*

以下是短变量声明的两个示例:

```
name := "Jane Doe"
salary := 50000
```

短声明仅用于声明局部变量。不能在函数定义之外使用短变量声明。因为您将主要在本地声明和使用变量，所以您的变量声明将是短声明。

您还会注意到它使用不同的赋值操作符进行赋值。`:=`操作符是许多程序员希望 C 开发人员从 Algol 中获得的赋值操作符。有时当我向我的 C++入门学生解释`=`和`==`的区别时，我也有这个愿望。

当使用短变量声明时，数据类型基于赋值操作符右边的初始化表达式。

还有另外两种方法来声明变量。如果要声明一个变量供以后使用，请使用以下语法模板:

*var 变量名数据类型*

这种声明的一个例子是:

```
var number int
```

像这样声明的变量被赋予数据类型的默认值。对于数字，那就是`0`。对于字符串，这是空字符串，对于布尔值，这是默认的类型`false`。与 C 和 C++相比，这是一个很大的改进，在 C 和 c++中，未初始化的已声明变量访问它们内存位置中的任何内容，如果变量在赋值前被使用，会导致奇怪的结果。

当使用这种形式的声明但忽略数据类型时，可以在一条语句中声明和初始化不同类型的变量:

```
var name, salary, employed = "John Smith", 55000, true
```

也可以声明一个变量并用表达式初始化它。以下是这种类型声明的语法模板:

*var 变量名数据类型=表达式*

以下是一些例子:

```
var rate float64 = 3.2873
var grade int = 87
var greeting string = "Hello, world!"
var flag bool = true
```

# 提示，然后读取编程模板

在这些文章中，我将在编程模板的背景下教授 Go，编程模板定义了常见的编程使用模式。我给你看的第一个模板是*提示，然后读*。

该模板提示用户输入一个值或一组值，并从键盘读取输入，并将值存储在相应的变量中。以下是该模板的伪代码:

*提示用户输入东西
把输入变成变量*

让我们看看这在 Go 中是如何工作的。

我将从一个简单的程序开始，它从键盘上读取一个名字(字符串)。我们将在这一系列文章的后面更详细地讨论在 go 中执行键盘输入的不同方法，但现在只需要理解这个程序将从键盘获取一个字符串并将其存储在一个变量中:

```
package mainimport "fmt"func main() {
  var firstName string
  fmt.Print("Enter your first name: ")
  fmt.Scan(&firstName)
}
```

我们可以修改这个程序得到两个字符串变量:

```
package mainimport "fmt"func main() {
  var firstName, lastName string
  fmt.Print("Enter your first name: ")
  fmt.Scan(&firstName)
  fmt.Print("Enter your last name: ")
  fmt.Scan(&lastName)
}
```

现在让我们看看如何将数字输入到 Go 程序中:

```
package mainimport "fmt"func main() {
  fmt.Print("Enter a number: ")
  var number int
  fmt.Scan(&number)
}
```

这个过程对于布尔型和浮点型是一样的。

# 转向输入-流程-输出

我教给学生的第一个编程模板是*提示符，然后阅读我在这里展示的*模板。从这里开始，下一步是开始讨论如何处理数据，比如做算术和字符串连接。我教学生如何使用模板*输入-处理-输出*来做这些事情。

在我的下一篇文章中，我将演示 *Input-Process-Output* 模板是如何工作的，您将学习如何在 Go 中进行算术运算，如何进行一些简单的字符串处理，以及如何使用 Print()函数和 Printf()函数执行格式化输出。