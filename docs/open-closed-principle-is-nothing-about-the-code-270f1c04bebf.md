# 开闭原则与代码无关

> 原文：<https://levelup.gitconnected.com/open-closed-principle-is-nothing-about-the-code-270f1c04bebf>

# 历史

1972 年大卫·帕纳斯教授提出了信息隐藏的概念。许多人将这个术语误解为简单封装。许多书将这些术语用作同义词。真正的意图是对其他模块隐藏模块设计信息。使用定义良好的接口与模块交流，尽可能少地暴露内部模块决策和设计。这使得模块松散耦合并可互换。我们有机会在模块范围内进行推理。

![](img/eca7397de58fca4b8b6545448ae12c41.png)

开闭原则这个术语是 1988 年由 Bertrand Meyer 在他的《面向对象软件构造》一书中首次使用的。他指出，模块应该是开放的和封闭的。作为封闭的，他的意思是模块已经完成，发布，并被其他人使用。模块相互依赖来完成各自的任务，因此这种变化可能会在整个系统中引发连锁反应。随着时间的推移，许多被证明行之有效的系统将再次变得不确定。他的想法是不修改现有的模块来处理任何新的特殊情况，而是引入一个封装新的 case 逻辑的新模块。Mayer 建议使用原始模块作为新版本的父模块。这种方法允许在不修改现有代码的情况下添加新功能。这也是基于使用抽象契约而不是特定的实现。

在 20 世纪 90 年代，这个原则被重新定义为使用抽象接口。这些接口的实现可能会改变。接口本身被认为是封闭的，而不是实现。接口的许多不同实现可以同时存在。我们希望重用接口，而不是实现。合同结束了。1996 年，罗伯特·c·马丁提出了这样一种方法。

1996 年，阿利斯塔尔·考克伯恩提出了受保护变异的概念。这和我们现代对 OCP 的理解是完全一样的。

# 扩展点

OCP 是软件工程的圣杯。大多数设计模式都旨在满足这一需求。作为一个设计原则，它更像是一种指导，甚至是一种思维模式，而不是某种模式。它告诉我们应该如何设计出可重用的组件，以及如何在不违反抽象边界的情况下扩展功能。这些抽象是设计的相关部分。这是我们模型中可行的一部分。新的行为应该来自新的代码。这都是关于寻找自然的扩展点。专业相机就是一个很好的例子。你可以自由轻松地更换镜片。插座代表一个接口，只要镜头生产商遵守这个标准，它就能很好地与你的相机配合工作。

重点不是提供最终的通用解决方案。这是不可能的。代码应该完全按照它的设计来做。不多也不少。OCP 说的是专注于提供好的抽象。这并没有改变任何抽象都不是完美的这一事实。每个抽象都只能在它被设计的范围内工作。因此，不可避免地要改变现有的代码，更重要的是要改变现有的抽象。抽象是这里的关键。系统的不同部分不应该相互依赖。我们的角色是以接口的形式在组件之间制作适当的契约。问题是在早期发现正确的扩展点并不容易。过度工程和紧缩之间有一个模糊的界限。仅仅通过假定的灵活性来证明任何额外的间接性是很容易的。但是这并不是伟大软件设计的良方。这里的难点是提供正确的可扩展性级别和定义正确的契约。这是直觉和经验的问题。如果不修改组件，总会有不容易实现的需求。这是一件好事。通过收集更多关于你的领域的知识，你可以得到一个更好的模型，你的抽象是模型的重要部分。目标不是避免更改现有代码。它更多的是试图发现并明确建模真实的依赖关系。这是一个寻找答案的过程，即为了有效地合作，我们需要对彼此了解多少。总的来说，我们的代码库和语言不是静止的。它不断进化，适应新的需求。违反 OCP 不是当你由于新的领域洞察力而有意重构你的代码库时，而是当你需要跨越抽象边界时。

# 限制

冬天你可以给你的车换轮胎。这是扩展功能的一个很好的例子。这一切都是基于一份完善的合同。轮辋如何适合你的车轴，轮胎如何适合轮辋等。这里有很多隐晦的地方。你的引擎并不真的关心你用的是什么类型的轮胎(在有大量电子设备的日子里，它可能看起来有点不同)。所有这些都依赖于定义良好的接口。然而，我们被允许定制我们的汽车到一个特定的程度和尺寸，它被设计成这样。这并不意味着任何概念都可以转换成其他概念。这并不意味着你应该试图把你的车变成一架直升机。做汽车和做直升机是两码事。如果你试图太开放，至少会很尴尬，没有效率，相当昂贵，而且不可靠。

假设我们需要为税收政策服务设计 API。该服务的唯一任务是确定特定商品的税率。我们知道每个项目必须属于一个特定的税收类别，不同国家或地区的分类可能会有所不同。我们是有经验的开发人员，所以我们希望依靠抽象，而不是具体的实施。我们现在需要计算税的是一个项目和分类表。

但一年后，我们的业务扩展到了墨西哥，事实证明，在墨西哥，当你满 100 岁时，你没有义务纳税。所以税率可能取决于顾客的年龄。我们的界面没有考虑到这一点。即使我们怀疑这方面的变化，我们也没有让我们的合同足够灵活。

在某种程度上还是可以解决的。我们可以在这里使用 IoC，并根据客户年龄使用一个从零开始的分类表。但这是知识泄露。我们也可能引入一些免税政策，并根据客户的属性使用工厂。这似乎也不是一个灵活的解决方案。例如，只有特定的项目可能是免税的，所以我们没有足够的信息来提前做出决定。所有这些都是伪造的，并不反映我们的知识。

我们可以有把握地假设客户与我们的合同相关，因为我们实际上是代表客户提出要求的。它还使我们能够在相同的上下文中为许多客户计算税款。就 DDD 而言，我们得到的最佳选择是坚持我们的代码库符合当前的知识。我们被迫打破 OCP，以利于调整代码来收集知识。现在我们可以很容易地建立 MexicoTaxPolicy，它概括了在墨西哥超过 100 岁的人可以免税的知识。听起来像是一个可靠的解决方案，我们已经将领域知识融入到适当的模型中。

不幸的是，在德国，税收可能不是取决于物品的价格，而是取决于数量。例如，购买烘焙咖啡时，你应该支付每公斤 2.19 欧元，而购买速溶咖啡时，你应该支付每公斤 4.78 欧元。这很麻烦。同样，这在早期很难预测，我们需要相应地调整我们的接口，并将请求的数量作为查询的一部分添加进来。

如果你是一个生产商，这甚至取决于你每年生产多少产品。对于年产量不到 200 万桶的国内酿酒商，FET 从 7 美元/桶降至 3.50 美元/桶。在这里提出一个优雅而灵活的 API 几乎是不可能的。我们最好的选择是将这个负担转移给策略构造器，而不去碰我们的 API。这种方法的缺点是服务不再是无状态的。它必须持有对某种存储库的访问权，以便为我们提供正确的结果。通常情况下，必须预先提供一些依赖关系，因为一些策略可能依赖于一组任意的属性。我们希望尽可能保持合同的相关性和通用性。

将 DateTime 参数添加到我们的查询 API 中也是合理的。特定商品的税收可能取决于季节，我相信在一些国家这真的取决于季节。我们不应该依赖当前的日期时间，因为这会使我们的 API 不纯。DateTime 还将模拟利率随时间变化的事实。

很明显，预测未来是不可能的。判断什么属于我们的自然契约，什么不属于，这是一个经验和直觉的问题。这完全取决于你的领域和你的问题空间。没有税收服务的终极设计。可能上述建议和考虑在你的系统中没有任何意义。如果某个问题是一般性的，那么总有现成的一般性解决方案。对于任何其他场景，您必须用一个恰到好处的可扩展性级别来为您自己的现实建模。

# 时间表

- 1972 年大卫·帕纳斯—信息隐藏“在将系统分解成模块时使用的标准”
- 1988 年伯特兰·迈耶—形式子类化中的开放封闭原则—“面向对象的软件构造”
- 1996 年罗伯特·c·马丁—OCP 在接口/抽象方面的重新定义—“开放封闭原则”
- 1996 年阿利斯泰尔·考克伯恩—引入受保护的变异—“软件设计中的优先力量”
- 2001 年克雷格·拉曼“受保护的变异:被封闭的重要性”