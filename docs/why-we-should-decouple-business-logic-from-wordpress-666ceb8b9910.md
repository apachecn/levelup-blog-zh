# 为什么我们应该将业务逻辑从 WordPress 中分离出来

> 原文：<https://levelup.gitconnected.com/why-we-should-decouple-business-logic-from-wordpress-666ceb8b9910>

## 将你的业务逻辑和 WordPress 紧密结合起来似乎没有坏处，但是确实如此，我会解释为什么。

![](img/2149709a6bb59c954a610a73da3b065f.png)

安妮·尼加德在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

WordPress 成为最广泛使用的 CMS，因为它是一个无需修改的好系统，但是当需要改变时，添加它们很简单。plugins 文件夹中只有一个基本的 PHP 文件，你可以拥有一个全新的 WordPress。

虽然这很适合采用，但作为一名专业的开发人员，我的目标不是扩展 WordPress 并让它做我想做的事情。我的目标是[解决企业存在的问题](/what-is-your-job-as-a-software-developer-and-why-youre-probably-wrong-1e7c60e6b255)。WordPress 只是工具。

我们经常将我们使用的工具与我们正在构建的项目混为一谈。我们允许便利性和时间约束影响我们的架构，并创建跨越太多架构边界的代码。

我们的项目架构中的问题在我们编写一行代码之前就开始了。它们始于项目的规划阶段。WordPress 有两种主要的方式将自定义代码放到你的网站上:插件和主题。我们使用的所有东西要么是插件，要么是主题。当规划你的项目时，我们首先要问自己什么？

# 这是插件，还是主题？

这个问题听起来耳熟吗？如果是这样，那么你已经成为围绕 WordPress 建立业务的陷阱的受害者。这是什么陷阱？围绕 WordPress 建立你的业务。

你的生意不是 WordPress。你的业务是向你的观众提供本地新闻。或者卖杂志。也许你的业务是为在线游戏产品提供一个数字市场。我见过所有这些，甚至更多，都是用 WordPress 运行的。

他们共有的问题？他们将核心业务与 WordPress 结合起来。

# MV…按？

[模型-视图-控制器](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)是一个众所周知的设计模式，我在这里就不再赘述了。我提到它是因为我认为当谈到 WordPress 时，我们需要从中获得灵感。MVC 背后的目的是关注点的分离，允许我们在不影响项目整体流程的情况下交换单独的部分。

用 WordPress 开发时，我们的关注点是什么？我们有我们的业务逻辑——我们的模型——和我们的网站模板——我们的视图。我们的控制器是什么？WordPress。

在现代 MVC 框架中，控制器管理请求生命周期。这正是我们希望从 WordPress 中得到的功能。好的，WordPress 就像是模型、视图和控制器的混合体。但是当涉及到我们编写的代码时，它就充当了控制器的角色。

当我们讨论为什么我们的代码与 WordPress 紧密耦合时，请记住这一点。

喜欢这篇文章吗？ [*成为会员*](https://travisweston.com/membership)*[*订阅*](https://travisweston.com/subscribe) *获取更多类似这样的精彩内容！**

# *WordPress 对我们有吸引力*

*紧耦合是什么意思？紧密耦合的代码需要另一段特定的代码才能运行。或者，换句话说:如果它“知道”WordPress，那么你的代码就耦合到了 WordPress。你不能孤立地运行你的代码。*

*这在 WordPress 中钩子的广泛使用和通过全局范围的变量和函数的渗入中表现得最为明显。如果我们允许我们的代码直接调用 WordPress，我们所做的就是允许 WordPress 与我们的代码结合。*

*而离婚码是很难的。*

# *代码，有好处*

*我喜欢把我写的代码想象成一个*模块。*模块是一个独立的特性，只关心它自己和它的任务。模块是混杂的。任何人都可以要求他们做他们的事情，他们会这样做。他们不需要任何特定的平台或框架来完成工作。所有模块需要的是它们的输入。根据输入，它们将输出返回给平台。他们不关心输出会发生什么。*

*我对所有代码的期望是创建离散的模块，并在模块中包含所有的业务逻辑。这是可能的，尽管我知道你在问自己怎么做。*

# *作为控制器的插件*

*所以你对着屏幕大喊，“要让你的愚蠢模块工作，你还得写 WordPress 代码，白痴！”可能有很多脏话。*

*当然，你是对的。*

*像其他事情一样，这里的目标不是*不写任何 WordPress 代码*，而是*将业务逻辑从平台逻辑中分离出来。**

*假设我正在构建一个基于故事的游戏。也许我决定使用 WordPress 来使更新故事更加简单，让我把注意力集中在游戏机制上，而不是建立一个内容管理系统和一个游戏。*

*WordPress 需要知道我有一个想要激活的游戏插件。当我的游戏插件运行时，它需要知道两件事:*

1.  *它需要 WordPress 之外的哪些数据；和*
2.  *它是如何将这些信息从 WordPress 中取出并放回 WordPress 的呢？*

*就是这样。*

*因为我们在构建插件时已经考虑到了模块，所以我们可以编写插件代码，通过创建一个微插件来执行我们的业务逻辑，从而调用该模块。*

# *由此得出合理的结论*

*如果我们把这个扩展到它的逻辑结论，我们得到两个独立的项目:我们小小的 WordPress 插件和我们在 WordPress 插件中需要的 Composer 包。我们的业务逻辑从来不需要了解 WordPress，因为我们的业务逻辑不应该关心 WordPress。*

*我们的业务逻辑关心它的业务。*

*WordPress 需要了解我们的商业逻辑，而不是反过来。如果我们的业务逻辑因为任何原因需要访问 WordPress，它会通过一个接口发生。假设一年后，我们决定最好将游戏转移到 Laravel。*

*我们可以做到这一点，而无需完全重写我们的游戏。*

*我们需要编写一个新的实现层，就这样。美妙之处在于，我们可以同时运行两个版本，同时更新我们的业务逻辑，因为这是三个完全独立的项目。*

# *模块的优势*

*不过，让我们面对现实吧。我们多久移动一次平台？不经常，特别是如果我们的业务逻辑依赖于 CMS。*

*这样做还有其他好处吗？*

*当然，否则，我也不会建议。*

# *测试*

*我一直直言不讳地说我有多讨厌在 WordPress 中测试代码。我喜欢测试代码，但是在 WordPress 中这样做总是很痛苦。通过将我们的代码分离成一个模块模式，我们得到了两个世界的最好的东西——使用 WordPress 的便利性和独立测试我们代码的能力。*

# *技能转移*

*关于在 WordPress 中编码的事情是，如果你花太多时间去做，你就不再是一个 PHP 开发者，而开始成为一个 WordPress 开发者。这在短期内没问题，但从长远来看，这会损害你的工作前景。将你的职业与 WordPress 紧密结合比将你的代码与它紧密结合更糟糕。*

*通过以模块化模式构建东西，您可以专注于创建干净的 PHP 代码，而不是使用正确的钩子在正确的时间启动某些东西。根据项目的大小，你可能永远不需要编写 WordPress 核心函数。在较大的项目中，你可能关注业务逻辑，而另一个开发人员可能只关注 WordPress 界面。*

# *企业成长*

*我将选择 Yoast SEO 一分钟，因为他们是普遍的，可以接受。*

*尽管价值不菲，但如果 WordPress 消失了，Yoast SEO 也会关门大吉。没有 WordPress 就没有 Yoast SEO。*

*但这是为什么呢？*

*Yoast SEO 的核心并不是 WordPress 特有的。不使用 WordPress 的网站可以从 Yoast 这样的 SEO 工具中获益。但是 Yoast 与 WordPress 是如此紧密地结合在一起，在这一点上几乎不可能分开。*

*如果他们今天重新开始，他们可以将他们的业务逻辑创建为一个模块，并构建一个基于 WordPress 的加载器。一旦 Yoast 控制了 WordPress SEO 世界，他们可以投资一个月来构建 Joomla loader。然后是 Magento。德鲁巴。*

*看不到尽头，因为随着开发人员创建新的 CMS 平台，Yoast 可以制作一个控制器层来与新平台接口。相反，它们局限于 WordPress 所占据的公认的巨大市场。*

# *结论*

*总会有与 WordPress 紧密耦合的代码。如果你的工具是一个修改核心函数的 5 行插件，那么你可能不用担心这个。*

*但是如果你是更广泛的“作为平台的 WordPress”社区的一员，并且你的组织依赖 WordPress 作为你业务的核心部分，你应该担心。你的生意取决于整个 WordPress 社区的意愿。这个项目太大了，无法由一家公司控制。*

*因此，最好将您与平台的交互限制在一个层，同时您的业务逻辑不会受到平台变化的影响。*

*你喜欢这篇文章吗？ [*成为会员*](https://travisweston.com/membership) *准备好 Travis Weston 写的所有东西——以及媒体上所有其他可用的东西。**

**已经是会员了？* [*订阅得到通知*](https://travisweston.com/subscribe) *特拉维斯·韦斯顿写的每一篇文章。**