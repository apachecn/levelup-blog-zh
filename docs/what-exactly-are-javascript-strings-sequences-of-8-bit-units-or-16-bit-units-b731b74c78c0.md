# JavaScript 字符串到底是什么？8 位单位序列还是 16 位单位序列？

> 原文：<https://levelup.gitconnected.com/what-exactly-are-javascript-strings-sequences-of-8-bit-units-or-16-bit-units-b731b74c78c0>

![](img/794cc0a921bc3df18a03145be6fde349.png)

照片由[拍摄，这是来自 Pexels](https://www.pexels.com/photo/two-man-and-woman-wooden-couple-keychains-hanging-on-rope-overlooking-bokeh-lights-1194025/) 的尊

几乎每次编写 JavaScript 代码时，我们都会用到字符串。知道如何在 JavaScript 中使用字符串对于每个开发人员来说都是非常重要的；事实上，字符串的概念适用于几乎所有的编程语言。毫无疑问。

但是，虽然我们可能知道如何在 JavaScript 中处理字符串，但我们真的熟悉 JavaScript 处理字符串的方式吗？我们能解释为什么`'🙂'.length`返回`2`而不是`1`吗？

所有这些都将在本文中详细讨论。让我们开始吧…

# JavaScript 中的字符串到底是什么？

任何编程语言中的字符串都是以非常典型和简单的方式定义的。也就是说，

> **字符串是一系列文本字符。**

这个定义没有错——毕竟，字符串实际上是一系列字符。

但是如果我们真的放大记忆的深度，我们会发现这个定义有点模糊。我们真的不知道这里的*‘字符’*到底是什么意思。

每种编程语言都可能有不同的解释。

现在我们关心的是 JavaScript，对吗？

因此，从 JavaScript 的角度来看，按照 ECMAScript 规范[的规定，字符串是以如下方式定义的:](https://tc39.es/ecma262/#sec-terms-and-definitions-string-value)

> **原始值，是零个或多个 16 位无符号整数值的有限有序序列。**

首先，从这个定义中有一点是绝对清楚的——不管是什么情况，字符串都是一个**序列**类型。

继续，这个序列中的每个元素都是一个 16 比特的数，一般称为一个*16 比特码单元，或者简称为一个 ***码单元*** 。最重要的是每个元素严格来说都不是一个字符。*

*让我们进一步阐述这一点…*

*JavaScript 中的大多数字符确实消耗了一个代码单元(即一个 16 位数)，然而这并不适用于所有的字符。有些角色如`🙂`消耗 2 个代码单位。*

*这马上澄清了一个事实，从技术上来说，字符串不是字符序列；相反，它是一个代码单元序列，当被解析时，形成一个(可视的)字符序列。*

*这听起来可能很复杂，但本质上，这是一个非常简单的想法。*

*根据这个想法，`**length**`字符串属性**不返回给定字符串**中的字符数，而是这些 16 位代码单元的数量。*

*这解释了下面的代码:*

*在本文的后半部分，我们将了解为什么🙂跨越 2 个代码单位。*

*现在的问题是，如果 JavaScript 中的字符串是一个 16 位整数序列，**这些单纯的数字是如何转换成字符的？***

*此外，【JavaScript 如何判断一个代码单元何时不单独表示一个字符，而是必须与下一个单元合并来共同表示一个字符？*

*所有这些都将在下一节中回答。*

# *Unicode 和 UTF-16*

*JavaScript 字符串是 16 位代码单元的序列。那很清楚。*

*但是这并没有真正告诉我们 JavaScript 是如何从一个数字`97`变成字符`a`的。*

*嗯，这就是 ***Unicode*** 及其 ***UTF-16*** 编码方案进入游戏的地方。*

*Unicode 是处理文本信息的国际编码标准。它可以用来方便地表示各种各样的字符，从 14.0 版本开始，有 144，697 个字符在全球范围内使用。*

*通俗地说，Unicode 可以被认为是一个巨大的表，其中一个唯一的数字与一个特定的字符相关联。这个唯一的数字叫做角色的 ***码点*** 。*

*例如，`a`的码位是`97`,`b`的码位是`98`,`A`的码位是`61`,`B`的码位是`62`，一个空格字符的码位是`32`等等。`🙂`的码位也在那里——`128578`。*

*你可以在 [Unicode 字符表](https://unicode-table.com/en/)看到表格的部分或完整版本。*

*现在 Unicode 只是整数到字符的映射，或者更好地说是整数到字形(字符的可视化表示)的映射。*

*帮助我们在编程环境中从这些整数(代码点)和可视表示(字形)来回转换的是一个 ***编码方案*** 。*

*Unicode 使用了几种编码方案:*

1.  ****【UTF】-8 位*** ，为 ***Unicode 转换格式-8 位****
2.  ****UTF-16*** ，为 ***Unicode 转换格式— 16 位****
3.  ****UTF-32*** ，为 ***Unicode 转换格式— 32 位****

*JavaScript 使用第二种，即 UTF-16。*

*让我们更深入地研究 UTF-16…*

*顾名思义，UTF-16 中最基本的单位是 16 位整数。Unicode 中的每个字符都被转换为 UTF-16 下的 16 位整数序列。*

*注意，我们在这里使用了术语*‘序列’*，而不是说 Unicode 中的每个字符都被转换成 UTF-16 下的*单个* 16 位整数。这是因为有些字符可以转换成不止一个，而是两个 16 位单位，比如🙂。*

*这就是 ***平面的概念*** 和 ***替代了*** 步骤的所在。*

*首先从**开始用*刨*刨**。平面只是一个花哨的术语，用来指 Unicode 中的字符集合。总共有 17 架飞机，可分为两类:*

1.  ****基本多语言平面*** —包含大多数常用字符。只有一架这样的飞机，那是第一架。它覆盖的码位范围如下(以十六进制提及):`0x0000 — 0xFFFF`。*
2.  ****补充平面*** —包含不太常见的字符，如数学符号、表情符号、乐谱等。所有剩余的 16 个平面都是补充平面，覆盖代码点范围的剩余部分。*

*接下来，我们来说说 ***代孕*** 。*

*回想一下，UTF-16 中最简单的单位跨越 16 位内存。这意味着我们只能有效地表示范围`0x0000 — 0xFFFF`中的数字。*

**是不是这样？**

*但是人物又是怎样的呢🙂用 UTF-16 表示，谁的码位超过了 16 位整数的最大限制？*

*答案是 ***代孕*** 。Unicode 中有一系列字符，特别是从`0xDC00`到`0xDFFF`，它们被称为 ***低代*** 。这些角色没有任何视觉表现，只是因为他们有一个特殊的目的。*

*也就是说，低代理字符的目的是指示另一个 16 位代码单元跟随其后，**与其**一起表示单个字符。低代理后的值称为 ***高代理*** 。*

*UTF-16 负责将给定的 Unicode 码位转换成一个 16 位代码单元，或一对 16 位代码单元(即低代理后跟高代理)，完全基于该码位。*

*更准确地说，如果一个字符的码位可以用 16 位表示，UTF-16 将把它转换成一个单一的代码单元。否则，UTF-16 会将其转换为一对两个代码单元(总共跨越 32 位)。*

*这种 UTF-16 处理的具体工作方式超出了本文的范围。你可以在 [UTF-8、UTF-16、UTF-32 & BOM](https://unicode.org/faq/utf_bom.html) 上阅读更多细节。*

*现在让我们来讨论一个 JavaScript 特性，它可以帮助我们将字符串视为一个字符序列，而不是一个代码单元序列。*

# ***字符串@迭代器方法***

*ECMAScript 6 在 JavaScript 中引入了符号。我们现在不讨论符号的细节，而只是了解这样一个事实，即由`Symbol.iterator`属性返回的值是 ECMAScript 6 中的`String`类的一个键，它帮助我们迭代字符串的字符，而不是它的代码单元。*

*按照惯例，给定对象的符号属性以`@`为前缀。因此，`String`的`Symbol.iterator`属性引用了一个函数，简称为`@iterator()`字符串方法。*

*现在，在 JavaScript 中有两种方法可以使用这个方法:*

1.  *使用`for...of`回路*
2.  *使用数组展开运算符(`...`)*

*(实际上，有三种方法可以使用这个方法，但是第三种方法依赖于手动使用 string `@iterator()`方法返回的迭代器对象，这反过来要求我们对迭代器有一点了解，如果不是很多的话。如果你想深入了解 JavaScript 中的迭代器，你可以参考我们自己的[高级 JavaScript](https://www.codeguage.com/courses/advanced-js/) 课程中的 [**高级 JavaScript——迭代器**](https://www.codeguage.com/courses/advanced-js/iteration-introduction) 介绍一章。*

*让我们一个接一个地看看这些…*

## *`for...of`循环*

*在下面的代码中，我们迭代字符串`str`并逐个记录它的每个字符:*

*注意数组是如何处理的🙂作为一个单独的实体，尽管在字符串`str`内部，它消耗了两个代码单元。*

## *数组扩展运算符(…)*

*利用这种基于字符而不是基于代码单元的字符串`@iterator()`方法的第二种方式是使用数组扩展操作符(`...`*

*在下面的代码中，我们使用`...`来确定给定字符串中的字符总数(不是代码单元的总数):*

*如前所述，`str.length`不返回`str`中**字符**的数量。相反，它返回代码单元的数量。*

*相反，`[...str].length`返回`str`中的字符总数。*

*`[...str]`首先使用字符串的`@iterator()`方法将`str`转换成一个字符数组。然后，`length`属性(在数组上调用)返回该数组中的项目总数。*

**简单，不是吗？**

# *最后*

*简而言之，JavaScript 将字符串视为 16 位整数(称为代码单元)的**序列。该语言中几乎所有的字符串工具都以这种方式处理字符串——例如，string `length`属性、字符串的词典比较等等。***

*如果我们想以一种无错误的方式在 JavaScript 中处理字符串，我们必须意识到语言的这种行为。*

*如果你想进一步了解 JavaScript 字符串中的 Unicode，你可以参考[JavaScript Strings—Unicode](https://www.codeguage.com/courses/js/strings-unicode)。*

*祝您愉快地学习 JavaScript 并使用它开发令人惊叹的程序！🙂*

```
*Learn JavaScript From Scratch[**JavaScript Course at CodeGuage**](https://www.codeguage.com/courses/js/)*
```

# *分级编码*

*感谢您成为我们社区的一员！更多内容见[级编码出版物](https://levelup.gitconnected.com/)。
跟随:[推特](https://twitter.com/gitconnected)，[领英](https://www.linkedin.com/company/gitconnected)，[通迅](https://newsletter.levelup.dev/)
**升一级正在改造理工大招聘➡️** [**加入我们的人才集体**](https://jobs.levelup.dev/talent/welcome?referral=true)*