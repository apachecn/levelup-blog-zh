# 提高整体性能

> 原文：<https://levelup.gitconnected.com/monolith-performance-f2d7b1b28493>

![](img/ece4b7ed67af996891e859ff7dcffc92.png)

提高整体系统的性能不亚于试图将一座山从一个地方移到另一个地方。事物之间的联系如此紧密，以至于很难做出任何改变。不像微服务，事情完全在少数人的控制之下，这里每个人都分享一切。

最近，我花了很多时间来提高 monolith 应用程序中某个组件的性能。到目前为止，我逐渐能够将性能提高超过 **40%** 。因此，我想从**的性能角度**分享我的经验，因为如果您的系统正在向整体式发展，或者如果您试图提高现有整体式系统的性能，这可能会有所帮助。

首先，让我列出 monolith 系统所面临的问题，与我之前使用基于**SOA/微服务**系统的经验相比。

# 问题

## 缺乏所有权

随着时间的推移，事情会发生变化，人们会从一个团队跳槽到另一个团队或另一家公司。现在在 monolith 中，代码库是共享的，随着时间的推移，可能会发生特定部分的代码成为孤儿的情况。没有人会拥有那段代码。因此，如果任何人对该组件有问题，他必须了解并改进它。这不是最佳选择，因为解决问题的人不具备这方面的专业知识，他可能没有考虑解决这个问题的时间。修复后，他们也将继续前进。在使用 confluence、commit history、slack channels 等搜索拥有任何模块的团队时，我多次遇到这种情况。

## 没有定义 SLA

很多时候，可能会有一个团队致力于代码的某个部分，但是由于没有明确的服务分离，所以没有遵守任何契约或 SLA。大多数情况下，您会为其他服务绘制图表，以得出它们的响应时间，但它们并不一定要遵守这些图表，因为它们没有定义或监控 SLA。

## 很难找到回归

因为没有分离服务，所以当组件的性能开始下降时，很难找出根本原因。您将看到下面的代码，因为没有边界的划分，您不能轻易地隔离有问题的区域。甚至基础设施也是共享的，所以你不能说是谁降低了它的性能。你将不得不做大量的调查，以找出谁在最近几天改变了什么，这可能导致了这一点。你可能要看看你的申请中的其他多个问题，看看你们是否有共同点，然后加入他们。

## 对基础设施没有控制权

因为每个人都共享相同的底层基础设施，所以很容易有人开始消耗更多的资源，如线程、数据库连接、CPU 周期、内存等，而您对此没有太多的信息和控制。同样的事情，你也可以对别人做。因此，在您的性能任务中识别或优化基础设施角色变得非常困难。

# 改进领域

正如我们在上面所看到的，在管理和改善一个整体的性能方面有很多困难，但是我们仍然必须让它继续下去，改善或保持性能。将整体拆分成服务是你可以采取的主要架构步骤之一，但是这需要时间和多人的协作。在这篇博客中，我想更多地关注你应该研究的代码和实践，我认为它们是关键的原则，在 monoliths 中非常普遍，对你有益。

## 不包括的项目:如接受服务项目是由投保以前已患有的疾病或伤害引致的

通常，API 会根据新的需求不断堆积越来越多的数据。随着时间的推移，这些请求中的一些可能会变得过时，所以如果不需要，应该清理它们，因为它们可能很昂贵，但仍然会被使用。当我们重新审视我们的 API 时，我们发现很大一部分信息没有被前端利用，排除这些信息给我们带来了大约 10–15%的收益。

## 平行

如果任务在性质和性能上是相似的，那么并行执行它们会有所帮助。你必须小心，如果任务划分得太小，可能不会有效。因为这是一个普通的基础设施，所以很难推导出来。在我们的例子中，当我们并行化稍微长一点的任务时，我们获得了收益，但是对于太多较小的任务，它没有影响。

## 确定主要瓶颈

在我们的例子中，尽管 API 做了太多的事情，但是通过一些深入的分析，我们发现了一个主要的瓶颈。如果你解决了一个大的瓶颈，它会给你带来比解决零零碎碎更多的收获。是的，不要解决你发现的所有问题，而是与正确的团队合作。他们可能会以更好更快的方式解决问题，因为他们在这方面有更多的专业知识。

## 移除多余的呼叫

如果在一个 API 的执行过程中，同一件事情在多个地方反复发生，这在 monolith 中是非常正常的情况，取决于它如何被使用的上下文，它可以被提取到一个平凡的地方，并且只能被执行一次。例如，对于任何资源，如果需要进行任何权限检查，可以只进行一次，然后您应该选择在后续处理过程中跳过权限检查的版本。

## 使用请求级缓存

在 monolith 中，由于在一个请求中有如此多的调用，并且 id 被传递给公共实体，所以它们通常会被调用多次。如上所述，在执行流程中，每个方法最好只调用一次。但是，有时候可能做不到。如果在一个请求中多次调用同一个方法，并且显著增加了总延迟，那么您应该使用一个**请求范围缓存**进行评估，该缓存在执行期间缓存第一次调用的结果，在后续调用中使用存储的结果，并在请求结束时使其无效。

# 结论

管理和改善整体性能是困难和具有挑战性的。然而，为了更好地管理它“**定期测量一切**”。看似简单的事情，有时却是最费时间的。在你的代码中使用一些像**剖析器**或**定时器**的工具作为检查点，这样你不仅可以测量它们的时间，还可以在出现倒退时找出原因。最重要的是不断地检查架构，以保持系统处于可管理的状态。