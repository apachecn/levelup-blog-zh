# 使用模式匹配来避免大量的“如果”语句

> 原文：<https://levelup.gitconnected.com/using-pattern-matching-to-avoid-massive-if-statements-ce286e2f0ea5>

![](img/30693e68e0b8ca6f9c09e866b44cf7de.png)

随着应用程序中业务逻辑的日益复杂，代码中的“if”语句将变得越来越臃肿，从而难以阅读和维护。*提醒一句*:我并不是说“如果”语句是邪恶的或代码味道的。我确实相信“if”语句在某些用例中有其优势，但是对于今天讨论的用例，我们将尝试找到一种替代方法来编写易读的代码。

这篇博文将向您展示一种方法，通过使用模式匹配和决策表来避免笨拙或嵌套的“if”语句。我将首先解释决策表的用例，然后用 C#举例说明使用模式匹配的实现。你可以在[我的 GitHub 库](https://github.com/dotnet-labs/PatternMatchingDemos)中找到完整的代码样本。

# 决策表

我们的客户和业务分析师通常在一个*决策表*中记录复杂的逻辑，多维条件导致不同的系统行为。**决策表**是一个可视化的表示，它列出了影响结果的所有可能的条件，并根据每个给定的条件组合指定要执行的动作。*决策表*中的条件可以显示为具有两个或更多可能答案的问题。下图是一个示例*决策表*，它是根据 Karl Wiegers 的书*软件需求(微软出版社；第三版，2013)* 。

决策表示例([要点链接](https://gist.github.com/changhuixu/c1d1f6b7816f98e7a06a7a0080e8d58d))

*决策表*提供了一种直观的方式来陈述复杂的业务规则，这有助于开发人员以及测试人员理解这些业务规则。我们可以很容易地浏览由不同输入组合引起的所有效果。此外，当软件需求发生变化时，我们可以通过添加/删除列/行来轻松地修复该表，并检查是否有缺失的组合。这些好东西使得*决策表*优于其等价的文本规范，以便表示大量重复的逻辑。

在*决策表*中表示的信息也可以表示为*决策树*或使用 *if-then-else* 和 *switch-case* 语句的编程语言。

以下代码片段显示了使用“if”语句的示例实现。

决策表实现使用“if”语句([要点链接](https://gist.github.com/changhuixu/2c15d1ae743f40a86c423214daee368c))

阅读这段代码并不困难，因为在每种情况下，由于“短路”，参数的排列是有限的。但是，修改这段代码时需要小心。即使案例足够简单，*还有改进的空间吗？*答案是肯定的！

# 模式匹配

代码胜过千言万语。让我们看看下面的代码片段，它实现了与上一节中使用“if”语句的代码片段相同的功能。

使用模式匹配的决策表实现([要点链接](https://gist.github.com/changhuixu/68907422478663b3c9b22357a878b3f0)

是不是很优雅？代码几乎模仿了软件需求中的*决策表*。我们可以很容易地检查软件需求和代码之间的一对一映射。如果将来需求发生变化，我们可以通过调整参数来相应地更新条件的行/列。

在上面的代码中，我们使用了*模式匹配*和元组( [C#元组类型](https://docs.microsoft.com/en-us/dotnet/csharp/tuples))。代码中的下划线(`_`)代表一个丢弃变量( [C#丢弃](https://docs.microsoft.com/en-us/dotnet/csharp/discards))。在`switch`代码块中，每个匹配的事例由一个元组表示。

注意，`switch`代码块中的匹配用例需要是常量值。通常，每个匹配条件可以由一个元组表示，该元组由数字、布尔、字符串、枚举、对象类型等组成。你可以在微软文档的[这篇文章](https://docs.microsoft.com/en-us/archive/msdn-magazine/2019/may/csharp-8-0-pattern-matching-in-csharp-8-0)中阅读更多关于*模式匹配*的细节。

在许多决策表中，条件是由值比较的结果决定的。例如:大于 0 的金额、非特定状态、特定时间之前的日期、可能值数组中的字符串等等。在这些情况下，我们需要借用一些函数来将值比较操作转换为原始类型的简单结果。出于演示的目的，我在下面列出了一个业务*决策表*，我们将使用一个帮助器函数来生成一个布尔值来表示比较结果。

另一个决策表例子([要点链接](https://gist.github.com/changhuixu/d2a0115b369a6f07e8b0a89fb254d3f4))

基于上面的*决策表*，我们可以通过匹配几个参数来查找差旅费账号。其中一个匹配案例(上表中的案例号 4)检查`TravelPurpose`是否在定义的字符串集合中。换句话说，如果`TravelPurpose`是`AR`、`SR`、`FR`中的一个，那么我们应该得到一组账号，否则，我们应该得到另一组账号。

该实现非常类似于上面“化学请求”案例的代码。我们模仿决策表并编写模式匹配`switch`代码块，除了我们使用`IsRecruit(string purposeCode)`函数将`TravelPurpose`列转换为布尔列。使用`IsRecruit`函数，`switch`语句能够用一系列常量元组匹配条件。下面的代码片段显示了一个示例。

更复杂的决策表([要点链接](https://gist.github.com/changhuixu/9998731455911b206dc6f059e225184d))

看起来不错。但是，每次调用`GetAccountNumber()`方法时，在`switch`语句尝试匹配元组之前，会检查`TravelPurposeCode`。换句话说，即使对于与`TravelPurposeCode`无关的情况，无论如何也要对`IsRecruit`方法进行求值。

如果“`IsRecuit`”方法很耗时，那么我们希望仅在必要时对其进行评估。在这种情况下，我们可以使用`when`表达式。下面的代码片段是上述相同实现的修改版本。

模式匹配使用“when”([要点链接](https://gist.github.com/changhuixu/b711af7d9b1002e793ea4ab5aa4c5408))

在上面的代码中，`IsRecruit`方法的求值被移到了第 15 到 17 行。只有当旅行元组匹配时，才会调用`IsRecruit`方法，从而节省一些计算资源。当*决策表*中的一列仅适用于少数条件行时，`when`表达式非常有用。

像其他`switch`语句一样，intellisense 将智能地检查数据类型，并检查元组案例是否已经建立了详尽的列表。注意，我们可以使用一个“`_`”来捕捉`switch`块末尾的所有剩余案例。

此外，智能感知将检查条件的顺序。如果一个条件已经被它上面的另一个条件覆盖，那么 intellisense 将在 IDE 中报错(在 Visual Studio 和 VS 代码中测试)。以下屏幕记录显示了一个示例。

![](img/a6bfb0f60cbfe8615b8ffffa0707f19d.png)

VS 代码中模式匹配的智能感知，Visual Studio 中也有类似的东西

在上图中，红色摇摆下划线表示顺序错误。

好吧！我希望您已经相信，通过使用决策表和模式匹配，我们可以避免大量的“如果”语句。请在评论区分享你的想法。

代码样本可以在[这个 GitHub 库](https://github.com/dotnet-labs/PatternMatchingDemos)中找到。享受编码。