# 关于 TypeScript 中的环境变量，您只需要知道

> 原文：<https://levelup.gitconnected.com/all-you-need-to-know-about-environment-variables-in-typescript-2e7042edfac7>

环境变量是在软件项目中传递配置的一种便捷方式。我们能利用类型系统有效地使用这些变量吗？请阅读我的文章，了解这个问题的答案和更多！

![](img/394ece2ebc7bca26c5b6fe8106ebe8d8.png)

照片由[欧文·史密斯](https://unsplash.com/@mr_vero?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

# 什么是环境变量？

大多数开发人员考虑将环境变量*键值对*传递给特定的程序。

对于每一对，键和值总是字符序列。或者你可以称之为字符串。在后端项目中，您将把这些对传递给服务器应用程序。

但是，对于前端项目来说，这并不是那么简单。当浏览器执行它们的代码时，它们不支持环境变量*本身*。开发人员通常利用额外的库(插件)来用预定义的常量替换这些变量的用法。通常，这种绑定发生在项目构建期间。

使用环境变量的原因是将配置与代码分开。现代产品使用*基础设施即代码*模型来管理基础设施，并将这些变量定义为所述模型的不可分割的元素。为什么它比将配置保存在项目的 JSON 文件中要好？

首先，JSON 格式允许嵌套对象。我努力使配置尽可能简洁——我发现实际上不需要嵌套信息。其次，我不希望在项目存储库中明确保留凭证。最后，我希望可以自由地将什么配置传递给程序。

# Node.js 中的环境变量

要在 TypeScript Node.js 项目中使用环境变量，我们需要添加`@types/node`作为开发依赖项。您可以使用`process.env`对象访问变量。这个对象是一个简单的字典，有字符串键和可选的字符串值。就类型而言，它使用了`ProcessEnv`接口。

即使你可以扩展`ProcessEnv`接口，我相信你不应该这样做。编译时类型的系统不可能预测运行时变量。我们有责任验证哪些键出现在运行时。

# 建筑模式

到目前为止，我在处理环境变量时观察到了两种架构模式:

*   在一个地方提取所有这些变量，
*   需要时提取变量。

将所有的环境变量放在一个文件中可以告诉我们需要将什么传递给可执行文件。它促进了依赖注入，因为我们需要将值显式地传输给需要它们的类和函数。有些人认为将环境变量从依赖代码中分离出来是一个很大的缺点——大多数开发人员不会测试提取功能。

当您在需要时检索环境变量时，它将本地代码与特定的变量绑定在一起。与前面的模式不同，它强制执行自顶向下的服务测试。为什么？如果不传递环境变量，就无法可靠地测试代码。

# 默认值

让我们假设你期望一个特定的变量出现。如果它不存在，你该怎么办？

我认为你应该突然停止这个项目。

根据我的经验，默认值是开发中几乎所有罪恶的根源。如果你提供默认值，你对外界依赖什么信息？是*在意*还是*大意*的信息？

这意味着你不在乎提供的值，因为你可以在任何时候用别的东西来代替它。

另外，我总是将配置从代码中分离出来。

确保环境变量保存有意义的值的一种优雅的方法是使用 TypeScript 断言，如下面的代码片段所示。

断言不可空变量的代码段。

我们也可以使用提取函数，如下所示。

从特定的环境变量中提取字符串值。

你也可以访问这个[链接](https://github.com/grzpab/ts-envvar)来访问上面定义的作为我的库的一部分的函数。

# 数值

因为环境变量包含字符序列，所以我们不能显式地使用数值。我们必须将数字编码为字符串，将它们传递给可执行文件，然后在我们的应用程序中对它们进行解码。

我们可以解码实数或整数。在我的记忆中，我从来不需要使用实数。请注意，虽然这样的选择仍然可用。

以下代码片段显示了如何实现从特定环境变量中提取数值。

从特定的环境变量中提取一个数值。

你也可以访问这个[链接](https://github.com/grzpab/ts-envvar)来访问上面定义的作为我的库的一部分的函数。

# 布尔值

同样，由于环境变量保存字符串，我们不能使用布尔值。我们能做的是在两个场景中选择:

*   运行时将`true`和`false`字符串映射成布尔值，
*   在运行时将`1`和`0`映射成布尔值。

我更喜欢用个位数的字符串。它们明显比其他选项短。

下面的代码片段展示了如何实现从特定环境变量中提取布尔值。

从特定环境变量中提取布尔值。

如前所述，您可以访问这个[链接](https://github.com/grzpab/ts-envvar)来查看上面定义的作为我的库的一部分的函数。

# 解码所有变量

如果您碰巧使用了`io-ts`库来解码信息，您可能会利用它从运行时可用的环境变量中提取数据。

在此之前，我们需要安装一个名为`io-ts-types`的依赖项。如果你是`io-ts`的狂热用户，你一定以前用过它。如果没有，这个库为开发人员提供了更高级的编解码器，包括一些隐式类型转换。

我们对哪些编解码器感兴趣？这些是:

*   `BooleanFromString`，
*   `IntFromString`，
*   `NumberFromString`。

一旦安装了依赖项，我们就可以构建一个接受`process.env`对象并解码其中存储的信息的编解码器，就像我在下面的例子中所做的那样。

用于解码环境变量的示例性编解码器。

为了获得足够的错误报告，您可以使用`io-ts-reporters`库。

# 测试提取

由于`process.env`是一个对象，我们可以毫不费力地添加和删除它的属性。尽管我绝不会在产品代码中这样做，但在测试中这是可以接受的。

如果您使用 Mocha.js，您可能会在以下地方修改`process.env`对象:

*   摩卡根钩，
*   摩卡挂钩。

您可以在测试用例中直接修改该对象。然而，如果您忘记恢复环境变量的原始状态，您可能会无意中污染其他测试的程序状态。

下面是在 Mocha.js 中使用环境变量的例子:

在 Mocha.js 中管理示例性环境变量

如果您在测试中修改环境变量，您可能会失去并行运行测试的能力。要恢复它，您可能需要执行以下操作:

*   将测试分为依赖这些变量的测试和依赖这些变量的测试，
*   一个一个地运行依赖它们的程序，
*   并行运行其他程序。

根据您的设置、时间和技能，您还可以考虑使用不同的 Node.js 流程运行特定的测试用例。

# 摘要

如上面的多个例子所示，在 Node.js 中处理环境变量并不简单。我们对这个话题了解得越多，我们发现的琐事就越多。因为我们使用了 TypeScript，所以在数据提取和转换过程中，我们必须小心谨慎。最后，类型系统允许我们构建对运行时条件有弹性的代码。

欢迎你在评论区留下你的评论。这是我 2022 年的第一篇文章，在 2021 年我的写作生涯成功启动后，我希望今年能让我联系到更多的人！