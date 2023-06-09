# 您不需要缺陷积压！

> 原文：<https://levelup.gitconnected.com/you-dont-need-a-defects-backlog-dcd6b33bff64>

## 如果你有，这里有一些策略来摆脱它

![](img/63a739b1015e4a5c0b8d202af0b41b8b.png)

图片来自[皮克斯拜](https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1562205)

[根据 Scrum 指南](https://scrumguides.org/scrum-guide.html#product-backlog)，没有提到术语“缺陷积压”，它仅仅描述了产品积压或者冲刺积压。我们仍然不断听到这样的消息，尤其是那些拥有大量遗留产品的公司。在大多数公司中，由于客户承诺或竞争，不断有压力要求更快地推出新功能。这导致了持续的斗争，以充分利用可用的资源，许多团队最终积累了大量的技术债务和缺陷。随着时间的推移，缺陷列表变得如此之大，以至于它自己变成了一个积压。在一些公司中，有支持团队处理缺陷积压工作，而其他人只是努力寻找时间来解决它们。

很久以前，我在一家大型软件产品公司担任技术主管。由于一些不幸的事件，公司决定关闭几个部门并裁员。幸运的是，我挺过了裁员，但被调到了另一个产品团队。团队中的每一个新人都被放在支持团队中，该团队只致力于修复缺陷积压中的缺陷。现在，我一直喜欢从事新的开发工作，所以我不顾一切地想要摆脱这个修复缺陷的任务。我能想到的唯一方法是摆脱缺陷积压本身。这是我从那次努力中学到的一些东西的总结，结合了多年来的其他经验。

要摆脱缺陷积压，您必须从两个方向着手——目标是关闭现有的缺陷，同时专注于减少引入的缺陷。

![](img/78e44d118fc05df2597dc9243d23f531.png)

图片来自 [Pixabay](https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2349444) 的 [PIRO](https://pixabay.com/users/piro4d-2707530/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2349444)

# 1.最大化缺陷闭合

## **1.1 排毒积压**

很多团队鼓励大家一看到缺陷就打开。他们可能有也可能没有适当的过程来分类所有的缺陷或者确认它们的有效性。你最终会有大量的缺陷，这些缺陷可能是也可能不是真正的问题。第一件事是通过关闭以下无关的缺陷来清理您的缺陷积压，这些缺陷只是增加了数字:

*   任何不能在稳定/受控的测试环境中重现的缺陷。
*   任何特定于配置/环境的缺陷。
*   任何在缺陷伪装下打开的增强请求。
*   特定用户的任何工作流程查询/建议/意见。
*   任何很少发生的低频率、低优先级缺陷(包括外观缺陷)。
*   超过 365 天未更新/报告的任何缺陷。

> 用户超过一年没有报告的任何缺陷要么不再是缺陷，要么不值得修复。

在练习的最后，您应该会得到一个可以重现的有效缺陷列表，修复它们将会直接帮助用户/消费者。有些人可能会反对其中的一些建议，但实际上，仅仅保留一个你不打算修复并且与用户无关的已知问题列表是没有价值的。

## 1.2 了解积压

现在你有了一个真正的目标待办事项，团队理解待办事项和所有的缺陷是很重要的。不是团队中的每个人都需要知道所有的缺陷。然而，应该有一两个人知道重要的缺陷和受它们影响的功能区域。这更像是通过回顾和理解缺陷，同时确定它们的优先级和严重性，再次训练细化的 backlog。它可以由团队领导、高级工程师、产品负责人或 scrum master 这样的角色来完成。这将是弥补这些缺陷的计划中的关键信息。

## 1.3 缺陷分组

一旦您知道了 backlog 中的缺陷，尝试通过按功能区域对它们进行分组来组织它们。有两件事应该完成。您可能希望通过缺陷的严重性级别(例如，关键、高、中或低)来区分缺陷的优先级，但是也有办法识别相同功能区域或相关代码库中的缺陷。分组可以是基于模块的，也可以是基于工作流的，或者是你的产品或应用的任何组织方式。例如，您可能想知道银行应用程序的开户模块中的所有缺陷，或者订单管理系统的账单生成中的所有缺陷，或者类似的事情。

## 1.4 创造机会

既然您已经有了有效缺陷的积压，并且理解了受影响的区域，那么是时候寻找机会来关闭它们了。从产品管理中获得专门的时间来修复缺陷总是很难，所以让我们创造一些选择:

*   如果在计划增强的同一个工作流中有任何缺陷，那么在讨论中包括这些缺陷。如果有人已经在改进代码，并且知道现有的缺陷，可能需要 1/4 的时间来修复它。甚至测试时间也可以减少，因为广泛的回归测试可以和新的开发一起覆盖。
*   冲刺计划是按照团队的速度来完成的，但是通常个人可以更早地完成他们的工作。使用优先化的缺陷列表来填补 sprint 之间的空白，而不是挑选下一个 sprint 的目标工作。这将保持 sprint 报告的质量(通过避免结转)，并且不需要太多的计划。
*   推动缺陷关闭成为团队的目标或目的，并给予少量激励。一个例子可以是每个团队成员在每个 sprint 中的一个缺陷关闭，或者是在计划的开发工作之上关闭缺陷的个人奖励。我过去的一个工作场所有一个减少 25%缺陷的季度目标，这个目标与高管奖金挂钩。在我看来有点太多了，但有时这些质量改进举措增加了大量的客户满意度，并增加了业务。
*   如果目标是结束缺陷，那么要有创造性和灵活性。一些团队只关注高优先级的缺陷，他们的缺陷积压从来没有减少。上面给出的分组方法建议，即使您选择了一个高优先级的缺陷，也要关闭相同代码库中存在的任何其他低/中级别的缺陷。由于某些活动如测试、构建和/或部署被组合在一起，一起修复三个缺陷而不是一次修复一个缺陷的总时间和工作量大大减少了。

> 总的来说，这是关于改变团队的心态，缺陷是不可接受的，修复它们是团队的集体所有权。

![](img/4ab93d9ef2ced90e1428e8dc3fca3a67.png)

图片由 [5238941](https://pixabay.com/users/5238941-5238941/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2271442) 来自 [Pixabay](https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2271442)

# 2.尽量减少缺陷的流入

当团队致力于减少现有的缺陷时，包含引入的缺陷也同样重要。如果缺陷关闭的比率不大于缺陷打开的比率，那么摆脱缺陷积压将成为一个运行目标。

## 2.1 缺陷根本原因分析(RCA)

应该分析所有的缺陷，尤其是逃逸的缺陷，以确定缺陷的根本原因。理解缺陷为什么会被遗漏是很重要的。

*   每一个逃脱的缺陷至少会导致一个额外的测试用例
*   缺失的实现可能需要几个测试用例来覆盖不同的场景
*   一个缺失的需求或者设计考虑可能会有更大的影响，并且需要更多的测试和分析来避免引入缺陷。
*   RCA 也可以帮助你识别你最近的缺陷是否有规律可循。如果它们都指向代码中的特定区域，那么可能值得评估是否值得修复大量缺陷，或者是否最好重写或重构与该工作流相关的代码。

> 每个缺陷本质上至少是一个缺失的测试用例。

## 2.2 目标回归

当一个缺陷被修复或者一个增强被添加时，测试被编写来覆盖代码的变化。很多时候，一个地方的代码更改会影响其他几个方面。应该努力确定影响半径，并运行有针对性的回归测试，以确保不会引入新的缺陷。

## 2.3 纳入发展最佳做法

*   在您的构建中包含测试覆盖/代码覆盖工具(例如 JoCoo、Cobertura ),并确保有健康的代码覆盖，不会随着新的工作而下降。
*   确保团队已经建立了多重代码审查和测试的过程。随着对测试自动化的更多关注，我看到一些团队并不关注同行评审或者同行验证。即使你的测试是自动化的，确保所有的测试场景都被第二双眼睛所覆盖也是有价值的。
*   尽快解决你的技术债务，或者更确切地说，从一开始就避免积累它。无论是过时的技术货币还是你一直想要重构的糟糕的代码，这些都是隐藏缺陷的潜在领域，这些缺陷稍后会显现出来。
*   确保每个版本的回归测试套件都有一致的细化，以删除不相关的测试用例，并添加缺失的测试用例。这将导致有意义和有效的回归测试。

# 最后的想法

当你写大量复杂的代码时，总会有缺陷。目标应该是将最佳实践落实到位，以便在到达客户之前发现大多数缺陷。应该尽快解决逃脱的问题。将缺陷列表永远保存为已知列表的旧思维过程对任何人都没有帮助。客户不在乎你是否知道这个缺陷。如果它影响了最终用户，那么它是值得修复的，并且应该立即有一个计划来修复它。请随意分享你的想法，无论你是否同意我的想法。欢迎所有反馈！

如果你喜欢这篇文章，你可以在你的邮箱里订阅这里的文章。如果你正在考虑加入 Medium，请使用我的[推荐链接](https://praveshbhargav.medium.com/membership)来支持我。

[](/5-things-i-wish-i-knew-as-a-new-manager-ee104d318844) [## 作为新经理，我希望知道的 5 件事

### 可以帮助你在新角色中更快成功的知识

levelup.gitconnected.com](/5-things-i-wish-i-knew-as-a-new-manager-ee104d318844) [](https://medium.datadriveninvestor.com/6-things-stopping-you-from-improving-your-work-culture-e4c1b82d3ca3) [## 阻止你改善工作文化的 6 件事

### 解决这些关键影响因素将有助于你创造更好的工作环境

medium.datadriveninvestor.com](https://medium.datadriveninvestor.com/6-things-stopping-you-from-improving-your-work-culture-e4c1b82d3ca3)