# Pro 之路—流量控制和环路

> 原文：<https://levelup.gitconnected.com/road-to-go-pro-flow-control-dfcc7b9a5395>

*开始前的几句话。你可以在这个* [*资源库*](https://github.com/songx23/RoadToGoPro) *中找到本教程使用的代码。你可以在这里* *找到《路要走》Pro* [*的全部内容。如果你错过了最后一个，可以通过这个*](https://medium.com/@songx/road-to-go-pro-f9d1f8a51fad) [*链接*](https://medium.com/swlh/road-to-go-pro-types-structures-21e5fedc5fe0) *找到。*

我们在教程的最后一部分讨论了基本类型和数据结构。在这一篇中，我们将讨论流量控制、循环和`fmt`包。

# 流控制

![](img/43d9b3f11da0e59afff3f4b90a527789.png)

照片由 [Igal Ness](https://unsplash.com/@igalness?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

## 如果

首先，我们来看一下`if`语句。最基本的流控制之一是 if 和 else 语句。它们控制程序根据条件执行不同的代码块。`if`语句的语法如下。

if…else… condition 伪代码

当 if 语句中的 conditionA 返回 true 时，就会执行`if`括号内的代码。否则，将依次评估以下条件，直到到达最后一个`else`代码块。Go 接下来计算 conditionB，如果 conditionB 返回 true，将执行里面的代码。如果 conditionB 返回 false，那么将执行最后一个代码块。在`if`、`else if`和`else`语句的组合中，求值的顺序总是从上到下。所以最后用`else`作为通吃块。当然，如果不需要一个包罗万象的函数，可以省略最后一个`else`块。

那么条件是什么样的呢？任何返回布尔值的语句都可以放在条件中。这里有一个例子。顺便说一下，我们已经使用`fmt.Println`有一段时间了，但我还没有正式介绍它。在本教程的最后一节，我们将讨论`fmt`包。

如果…否则…举例

您也可以在条件中使用逻辑运算符。有三种逻辑运算符，即 and ( `&&`)、or ( `||`)、not( `!`)。可以通过逻辑运算符将条件链接在一起，形成复杂的条件。

复杂条件示例

在一个`if…else if … else`链中，你可以写多少个`else if`语句是没有限制的。然而为了可读性，我们不建议使用很长的 if/else 语句列表。`switch`是处理这种情况的正确选择。在我们开始之前，我想在 Go to you 中介绍一种特殊语法的`if`语句。

Go 可以在`if` / `else if`语句中的条件前接受一个“短语句”。这种语法使代码更加简洁。它广泛用于错误处理，我们将在后面的教程中介绍。让我们来看看这个语法的一个例子。

if 中的简短语句

“短语句”是一个或多个变量的声明:它们是短暂的，只能在最近的括号内访问。在上面的例子中，如果我们试图访问`if`代码块之外的短语句中的变量，我们将得到一个错误返回。Go 中一个常见的错误处理模式是使用短语句来检查函数是否返回了错误。由于返回的错误只与`if`条件相关，我们可以使用“短语句”语法使代码更简洁，避免变量范围的混淆。

**变量范围**

让我快速解释一下变量的范围是什么。并非所有的变量都被同等地声明。它们的可访问性取决于声明的位置。例如，如果一个变量在`if`块中声明，我们只能在同一个代码块中访问它，而不能从外部访问。一个通用的经验法则是:变量的范围以它最近的括号(`{}`)为界。

可变范围示例

在上面的例子中，`anotherPlace`和`newPlace`只能在最近的括号内访问。如果变量周围没有括号，那么它就是包内的全局变量。我们将在谈到包时讨论可访问性。目前，记住括号规则就足够了。

## 转换

好了，分心够了。让我们回到流量控制。我提到过，当我们有一个很长的条件列表时，最好使用`switch`语句，而不是`if`语句。`switch`是`if`更干净的形式，看起来是这样的。

开关示例

示例 switch 语句可以转换为下面的 if 语句。

转换开关到 if…else…

switch 语句将其关联变量与内部的`case`语句中的值进行比较。如果找到匹配，将执行该`case`块中的代码。一旦该程序块完成，程序就退出切换程序块，而不检查其他情况。最后一个`default`块类似于`else`语句。

如果只检查 3 个条件，您可能不会觉得编写`switch`语句更容易。但是想象一下，如果你需要像这样写 10 个条件。`switch`看起来会比`if`干净简洁很多。

`switch`也有一个更通用的形式，我们不需要在它后面指定变量。相反，可以在`case`语句中指定条件。例如:

通用开关语句

是的，通用 switch 语句中的 case 条件可以是符合`if`语句的任何条件(不包括特殊的短语句语法)。

那么什么时候该用`if`什么时候该用`switch`？在我看来，它们在很多情况下是可以互换的。就我个人而言，我会选择视觉上更干净、代码行更少的那种。

# 环

![](img/8f12fd54c06b82e26889051573c6b576.png)

照片由[Tine ivani](https://unsplash.com/@tine999?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

当我们需要重复执行逻辑时，循环就是最好的帮手。没有人想一遍又一遍地复制粘贴重复的代码。在其他语言中，你可能见过像`for`循环和`while`循环这样的循环。但在围棋中，只有`for`循环。

## 为

For 循环在 Go 中有四种形式。

**基本形式**

最基本的循环形式在许多语言中看起来完全一样。供您参考，我在实际项目中很少使用这种形式。

for 循环—基本形式

让我们快速浏览一下基本的表单语法。

上面的 for 循环中有三个短语句，它们由`;` s 分隔。第一个短语句用于启动循环索引。通常，它以 0 开头。第二个简短的语句是循环条件。只要满足循环条件，循环就一直执行，直到循环条件返回`false`。最后一个语句是步进函数。我们指定在每次迭代中要改变什么。大多数时候，它会增加/减少循环索引。上面的例子向我们展示了如何循环遍历一个切片。我们从将循环索引设置为 0 开始。循环应该在到达切片中的最后一个元素后退出。因此，我们将条件设置为“循环索引需要小于切片的长度”。最后，我们将步进函数设置为“将索引增加 1”。

需要注意的是，这三个简短的语句都是可选的。我们将在下面看到它的不同含义。

**而表格**

围棋中没有`while`这个关键词。而 form 只是基本`for`循环的一个变种。如果我们从基本形式中省略初始化和步进函数，我们将得到 while 形式。因此，只要满足循环条件，循环就会一直执行。上面的例子可以很容易地转换成这样的 while 形式。

for 循环— while 形式

**无尽形态**

死循环(Endless loop)，又称“死循环”，是一种危险的循环。通常情况下，如果我们有一个死循环，它会破坏程序，因为它会吞噬程序可以获得的所有资源，从而导致主机系统崩溃。这通常是一件非常糟糕的事情。然而，在 Go 中，有一些特殊的用例，我们可以使用无限循环。例如，当您想要运行一个异步后台进程时，您可以创建一个无限循环并让它在后台运行。我保证，那不会产生灾难性的结果。要编写一个无限循环，只需省略基本形式中的所有三个语句。

for 循环—无限形式

当然，我不会让你直接在 main 函数中运行一个死循环来弄坏你的电脑。我们在这里做的是在一个 goroutine 中运行它(将在以后介绍)。Goroutine 支持异步处理，因此我们的无限循环与主进程并行运行。当主进程休眠 5 秒钟时，异步进程应该连续执行无限循环，直到主进程退出。这就是为什么我们看到“我是一个死循环。”在控制台中打印 5 次。

**范围运算符**

最后，我们来谈谈范围运算符。它有助于轻松迭代切片/数组、映射、通道和字符串等类型。让我们看看如何简化基本形式。

for 循环-范围运算符(切片/数组)

当在切片或数组上应用范围运算符时，它为每次迭代提供两个变量，即当前迭代的索引和值。请注意，这些变量是短暂的，只限于每次迭代，并且只能在循环内部访问。通常，我们不需要索引，所以我们可以通过使用`_`省略对变量的赋值。会是这个样子的`for _, value := range slice {…}`。事实上，如果你不使用循环内部的任何变量，Go 会强迫你省略它们。

使用 range 操作符遍历地图也会返回两个变量。不同的是，它返回映射的键而不是索引。

for 循环-范围运算符(映射)

类似地，如果我们不使用范围操作符返回的变量，我们需要省略它们。

应用于字符串或字符串类型时，范围运算符返回两个变量。第一个和 slice/array 一样，都是索引。第二个是字符的 Unicode(以`int32`为代表)。

for 循环—范围运算符(字符串)

在这个例子中，你可以看到我们使用了`fmt`包中的一个新函数。是时候解释一下`fmt`包的格式化功能了。你可以跳到最后一节先睹为快。

**继续&中断**

`continue`和`break`是跳过迭代的短路语句。使用`continue`时，程序会跳过`continue`后的代码执行，开始下一次迭代。虽然`break`更有力，但程序在看到`break`时会跳过整个循环。

继续和中断示例

**转到&标签**

`goto`和`label`允许在同一个函数中从一个语句跳转到另一行代码。标签名称的惯例是全部使用大写字母。

转到标签示例

`goto`和`label`在那里没有最好的名声。误用它们可能是意大利面条代码的标志，这是每个人都想避免的。然而，他们并不是天生邪恶的。它们确实有特定的用途。例如，在内置的[数学](https://golang.org/src/math/gamma.go)包中，我们可以找到`goto`语句的正确用法。

**延期**

`defer`是我想在本教程中介绍的最后一个流控制语句。它用于推迟函数执行，直到最近的周围函数退出。这里有一个例子。

延期示例

如示例所示，最后在退出主函数时执行了`defer`之后的语句。需要注意的是，一系列`defer`语句的执行顺序是相反的。换句话说，最后声明的`defer`将在退出功能时首先执行。另外，`defer`语句中的参数是内联计算的。这是唯一不能推迟的事情。

当我们创建最好在函数结束时关闭或删除的东西时,`defer`很有用。没有`defer`，我们需要在开头写一个 open 语句，然后在结尾关闭它。这很容易出错，因为很容易忘记关闭它。使用`defer`，我们可以在打开后立即编写一个`defer Close()`语句。这样，就不太可能忘记。我们将在高级主题中讨论数据库连接和 HTTP 服务器时使用它。

# **奖励内容:** `**fmt**` **套餐**

![](img/82eb3aea94ba3780ae0945747884b275.png)

[梁杰森](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

我相信你见过很多`fmt.Println`函数。我们经常使用它在控制台中打印结果。`fmt`是 Go 强大的内置格式化包。`Println`是软件包中的功能之一。你可以在这里找到`fmt`包[的文档。那里的内容还真不少。在本教程中，我不打算逐一介绍它们。我想指出的是这个包里的格式化程序。当操作字符串时，使用格式化程序可以节省我们的时间和代码行。](https://golang.org/pkg/fmt/)

你会发现一些函数的名字后面有一个“f”。这表明这些函数接受 formatter 作为参数。那么我们如何使用格式化程序呢？让我们来看看这个`Printf` 函数的例子。

格式化程序—基本用法

`Printf`中的第一个参数是格式字符串，后面的参数是将替换格式“动词”的自变量。在上面的例子中，格式动词`%s`被替换为`whoami`值。您可以在格式字符串后放置任意数量的参数。但是，唯一的要求是格式谓词的数量需要与参数的数量相匹配。

这个格式器的核心在于格式动词，下面我们来看看不同类型的格式动词，如果你想看格式动词的完整列表，你可以在`fmt`包的文档中找到它们。

## **布尔型**

布尔值唯一可用的格式动词是`%t`，它将布尔值格式化为字符串值(“真”或“假”)。

格式化程序—布尔值

## 数字

数字有更多的格式动词。下面是一些使用最广泛的方法。

*   `%b`:基数 2 的数字
*   `%d`:十进制数
*   `%U` : Unicode 格式
*   `%e` / `%E`:科学记数法
*   `%f`:小数点数字

让我们看看他们的行动。

格式化程序—数字

*注意:用反勾号括起来的格式字符串与普通双引号相同。然而，反勾号允许在多行中写入单个字符串。*

## **琴弦**

字符串的格式谓词:

*   `%s`:字符串
*   `%q`:字符串用双引号括起来，安全转义

格式化程序—字符串

## **一般**

上面提到的动词是针对特定类型的。也有通用的格式动词，适用于任何类型。

*   `%v``:默认格式的值
*   `%+v`:当值为结构时打印字段名称
*   `%#v`:打印值的 Go 语法表示

格式化程序—一般值

更多时候，我们并不真的需要在控制台中打印出字符串。我们只需要格式化字符串并在程序中使用它们。幸运的是，还有一个函数叫做`Sprintf`。它与`Printf`相同，唯一的区别是`Sprintf`将格式化的字符串作为变量返回。

# 下一步是什么？

![](img/d3ac6875264fce2204700a92b4ee764f.png)

照片由 [Olesya Grichina](https://unsplash.com/@lsgr?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

在下一个教程中，我们将讨论指针和函数。敬请期待，下一集再见。

如果你遇到任何问题或者需要帮助，请在下面留下你的评论。随时欢迎反馈。感谢您的阅读！

***特别感谢*** [***马克谟-库克***](https://medium.com/@mhumecook) ***对本教程的点评。***