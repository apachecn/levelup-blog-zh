# 正则表达式教程—匹配 URL

> 原文：<https://levelup.gitconnected.com/regex-tutorial-matching-a-url-25792ec7193c>

![](img/5488479ba5a76622cf80108264748dc1.png)

正则表达式的快照

在本教程中，我们将研究匹配 URL 的正则表达式。使用这个例子，我们可以开始建立对正则表达式的基本理解，每个组件代表什么，如何在代码中实现它们来定义搜索模式，以及如何使用它们来验证某些字符串是否匹配特定的标准。本教程是对正则表达式的一个非常基本的介绍，还有更多复杂的内容超出了本文的范围。

# 摘要

如前所述，下面的正则表达式可以用来验证字符串实际上是一个 URL

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

简单地说，这个表达式可以分解为:

*   该字符串必须以`https://`开头
*   该字符串可以包含任何数值`0-9`、任何小写字母`a-z`、`.`或`-`。该字符串可能会与此模式匹配一次或多次
*   `.`必须遵循以前的模式
*   字符串的下一部分必须包括来自`a-z`、`.`的任何小写字母，长度在`2-6`个字符之间
*   接下来，字符串可以包括`/`，后跟来自基本拉丁字母的`any alphanumeric character`(包括`_`)、`.`或`-`。这种模式可以重复 0 次或更多次
*   前一模式可以跟随`/` 0 或一次

# 正则表达式组件

构建正则表达式有许多单独的组件。因为 regex 被认为是一个文字，所以记住这些表达式必须用斜杠字符`/`括起来是很重要的。当查看我们匹配 URL 的示例表达式时，我们可以在开头和结尾看到`/`。

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

我们现在来看看组成这个表达式的每个组件。

## 锚

`^`和`$`是 regex 中使用的两个锚点字符。

`^` -这个锚是表达式的开始，标识应该跟在它后面的字符串的开始。这种锚有两种不同的用途:

*   表示精确匹配，例如`^ABC`。`"ABC"`和`"ABCDEFG"`都是匹配的。
*   使用括号表达式表示可能匹配的范围。我们将在后面的部分研究括号表达式。

## 量词

在 regex 中，量词定义要匹配的字符或表达式的数量。首先，我们将查看所有不同类型的量词，然后查看正则表达式示例中用于匹配 URL 的特定量词。

*   `*` -匹配前面的模式 0 次或更多次。例如:`/fun*/`匹配`"funny"`中的`"fun"`和`"thunder"`中的`"un"`，但是`"bird"`中没有匹配
*   `+` -匹配前面的模式 1 次或更多次。示例:`/k+/`匹配`"kick"`中的每个`k`
*   `?` -匹配前面的模式 0 或 1 次。示例:`/e?el?/`匹配`"gel"`中的`"el"`和`"cradle"` *中的`"le"`关于* `*?*` *的一个重要注意事项是，如果它紧接着另一个量词(* `***` *、* `*+*` *、* `*?*` *、* `*{}*` *)使用，它会使量词非贪婪，这意味着它将匹配最小次数，与默认情况相反*
*   `{ n, x }` -匹配前面的模式最少`n`次，最多`x`次

回头看看匹配 URL 的正则表达式示例，我们可以检查表达式中出现的不同量词。

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

*   我们看到`?`用在一些不同的地方。首先表示`"https"`可能匹配 0 次或 1 次，然后表示`"https//"`可能匹配 0 次或 1 次，最后表示`/`可能匹配 0 次或 1 次
*   我们看到`*`用来表示`[\/\w \.-]`可能匹配 0 次或更多次，而`([a-z\.]{2,6})([\/\w \.-]*)`可能匹配 0 次或更多次

## 分组结构

regex 中使用分组构造来检查字符串的多个部分或节，以满足不同的需求。通过在正则表达式的不同部分使用括号(`()`)，我们可以创建具有彼此独立需求的子表达式。

除非另有说明，否则子表达式会查找精确匹配。例如，给定子表达式`(abc):(def)`，`"abc:def"`匹配，而`"cba:fed"`不匹配。

在我们匹配 URL 的正则表达式示例中:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

我们看到以下子表达式:

*   `(https?:\/\/)`
*   `([\da-z\.-]+)`
*   `([a-z\.]{2,6})`
*   `([\/\w \.-]*)`

## 括号表达式

括号表达式，也称为正字符组，表示我们希望在字符串中匹配的一系列字符。在编写括号表达式时，我们可以包含我们想要匹配的所有字符，但更常见的做法是使用连字符来表示这些字符的范围。例如,`[abcdef]`与`[a-f]`有相同的含义，并表明我们正在寻找一个包含`a`或`b`或`c`或`d`或`e`或`f`的字符串。只要字符串包含指定的字符之一，它就会被视为匹配。

在我们匹配 URL 的正则表达式示例中:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

我们看到以下括号表达式:

*   `[\da-z\.-]` -该括号表达式表示任何数字、任何小写字母 a-z、斜线、点或连字符都将产生匹配
*   `[a-z\.]` -这个括号表达式表示任何小写字母 a-z、斜线或点都将产生匹配
*   `[\/\w \.-]` -该括号表达式表示任何斜杠、任何字母数字字符、点或连字符都将产生匹配

## 字符类别

字符类在 regex 中用于定义字符集，其中一个字符可以出现在字符串中以产生匹配。在前一节中讨论的括号表达式是一种流行的字符类类型。以下是一些其他常见的字符类。

*   `.` -匹配除`/n`(新行)以外的任何字符
*   `/d` -匹配任何数字
*   `/w` -匹配拉丁字母中的任何字母数字字符，包括下划线(`_`)
*   `/s` -匹配单个空白字符，包括制表符和换行符

*注意，* `*/d*` *，* `*/w*` *，* `*/s*` *，可以通过字母的大写来改成逆匹配。*

在我们匹配 URL 的正则表达式示例中:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

我们看到字符类以下列方式应用:

*   `[\da-z\.-]` -在这个括号表达式(本身是一个字符类)中，我们看到`/d`被用来表示任何数字都会产生一个匹配
*   `[\/\w \.-]` -在这个括号表达式中，我们看到`/w`被用来表示拉丁字母中的任何字母数字字符将产生一个匹配。

## 字符转义

在 regex 中，字符转义使用反斜杠(`\`)表示。当一个字符不打算按字面意思解释时，使用字符转义。例如，`{`通常表示量词的开始，但是如果我们在花括号前面加一个反斜杠(`\{`)，regex 会寻找一个开花括号，而不是量词的开始。这在查找包含特殊字符的字符串时非常有用。对字符转义(以及所有其他特殊字符)的一个警告是，当包含在括号表达式中时，它们会失去功能。

看看我们匹配 URL 的正则表达式示例:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

我们可以看到在哪里使用了字符转义。

*   `\.` -这里用来表示我们正在明确地寻找字符`.`，而不是字符类

# 作者

安德鲁·梅森 2022 年在加州大学伯克利分校学习网页开发。他喜欢创建新项目，并且是开发人员社区的活跃成员。要查看更多他的作品，你可以访问他的 [GitHub 简介](https://github.com/atmason90)。

【http://github.com】最初发表于[](https://gist.github.com/atmason90/0bafb2aed1302f65ba507b0846023c71)**。**