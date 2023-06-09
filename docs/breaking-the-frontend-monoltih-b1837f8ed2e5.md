# 打破前端巨石

> 原文：<https://levelup.gitconnected.com/breaking-the-frontend-monoltih-b1837f8ed2e5>

![](img/ed67bd5c63640e622420050d3024d590.png)

由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) 拍摄

在本文中，您将了解在将典型的前端整体迁移到微前端时出现的挑战。你将听到领域驱动设计的常见实践，这将帮助你在你的 monolith 中绘制边界，最终允许你将你的子域划分为微前端。

# 迁移到微前端

![](img/1a7883496ad2068a459c69b2f4d5c057.png)

由[波巴·贾格利契奇](https://unsplash.com/@bobajaglicic?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

采用微前端架构的理由很少，而最常见的理由是**扩展团队**。免责声明:如果你的前端团队少于 3 个，微前端可能会矫枉过正，对你的组织没有意义。微前端的主要目标只是让独立的模块也可以独立部署。

迁移到微前端架构的另一个原因是为了迁移 JavaScript 框架。例如，在将 AngularJS 迁移到 Angular 时，实现一个微前端架构是有意义的，因为这样就可以创建一个混合应用程序，使用 Web 组件抽象出一个 JS 框架。这实际上是一件大事，因为在过去，迁移大型应用程序是一件非常痛苦的事情，因为通常您必须进行重写，这需要花费数月的时间。另一方面，使用微前端迁移策略，您可以逐渐地一个子域接一个子域地迁移，或者一页接一页地迁移，同时您仍然可以跟上功能/bug 请求。

然而，如果您必须决定使用微前端，那么您应该注意最常见的错误，它会使您的整个架构变得毫无意义。只有当你的应用程序已经在非常独立的细粒度库中构建时，微前端才会工作。否则，系统中某个部分的变化将导致所有微前端的部署，因此独立部署的好处完全消失了。

![](img/a91308807463d1dbbb9af7ac6016558b.png)

糟糕的建筑

因此，我们必须从创建一个在代码依赖方面已经非常独立的系统开始。我们需要将这个所谓的“大泥球”构造成更小的模块，彼此之间的依赖性更小。

![](img/ece5274f49d1a712b9d2b4789b3d75a1.png)

好的建筑

当它只是以图表的形式出现时，看起来真的很简单，但是在现实世界中，将一个应用程序划分为独立的子系统绝非易事。我有一个坏消息和一个好消息。不好的一点是，没有完美的一步一步的指导给你一个完美的分离。好消息是，许多人以前面临过这个问题，并提出了许多想法，支持我们找到可能有效的分离。这些想法中的许多都可以在领域驱动的设计哲学中找到，我经常把它看作是一个巨大的工具箱，用来弥合需求和软件架构之间的差距。

# 实现领域驱动的设计模型

![](img/7ffc2da199da6405b58ea56f5522941b.png)

埃里克·埃文斯的《大蓝皮书》

领域驱动设计可以分为两个主要概念:**战略设计和战术设计**。战略设计关注的是更大的图景和将大系统分割成子领域，而战术设计更多的是实现细节，比如设计模式和最佳实践。因此，当我们谈到将一个系统分解成子域时，战略设计对我们来说更为重要。

但是我们如何创建所有这些子域呢？尽管没有总是适用的直接答案，但有多种工具，来自 DDD 工具箱，它们将帮助我们识别好的域切片的可能候选者。另一个坏消息是:我们必须关注业务流程。我知道这是任何开发人员都不愿意做的事情，但是这是完全必要的，您很快就会看到它的好处。

我们来看一个具体的例子——一个酒店软件。顾客会在 Booking.com 这样的网站上在线预订几天的住宿，然后在预定入住之前会安排一个简短的客房服务。成功登记入住后，酒店酒吧会为顾客提供一杯迎宾饮品。当然，在入住之后，顾客会结账。

![](img/15058dfdcebda7bfd6c968b50aac2905.png)

子域切片的指示

在上图中，我们查看了三个区域— **、业务流程、实体、域代理—** ，这将帮助我们识别可能的子域。如您所见，业务流程本身没有主要的共性。也许，签入和签出是相关的，但最好是不同的子域。如果我们看看实体，我们肯定可以看到许多共性，因为预订是在三个不同的步骤中使用的。如果我们看看领域代理，或者换句话说，业务流程中涉及的人员，我们还可以看到签入和签出都是由接待员完成的。

现在，我们能够在纸上看到许多方面的共性和差异，因此领域切割更容易。坦率地说，这使得决策更容易，但是肯定没有告诉我们什么是理想的域切割。这只是一些真正主观的东西，没有对错，因此我们应该尝试从良好的直觉开始，然后以敏捷的方式适应领域切割。

![](img/bf816a79ad68e9849e0158a7ef744f62.png)

子域

在这个例子中，我决定用四个子域名。预订、客房服务、接待处和酒吧。这可能是一个好的也可能是一个坏的领域分割，没有人能够在不知道系统的确切需求的情况下做出判断。既然已经确定了子域，我们必须再次谈论一些重要的东西— **通信**。虽然，当子域不共享任何依赖并完全独立工作时，这将是完美的，但现实看起来是不同的。实际上，几乎所有子域都依赖于其他子域。为了可视化子域之间的依赖关系，我们创建了一个所谓的**上下文图**。

![](img/3eb477e34038361f54961b55b73c7d94.png)

上下文地图

如您所见，Booking 子域位于上下文地图的中心，因为所有其他子域都依赖于它。这并不奇怪，因为所有的子域都依赖于预订实体，预订实体触发客房服务，并激活酒吧迎宾饮料的优惠券，接待处必须能够看到所有当前的预订。这肯定是不幸的，因为预订子域的变化将触发所有子域重建，这与常规的整体相比基本上没有部署优势。

![](img/a25394d4676547bc8af457376052cff5.png)

共享内核

幸运的是，战略设计中有许多技术可以帮助最小化这些差异。其中之一是作为共享库的**共享内核**，从而消除了子域之间的直接依赖性。但是要注意，要让你的共享内核尽可能小。

还有许多其他的技术，比如**开放/主机服务**，或者**反腐败层**，我推荐你阅读一下。

# 抽象之上的复制

在进行 DDD 时，为了取得成功，只剩下一个我们必须谈论的话题。在一个子域中，我们有一种所谓的通用语言，这基本上意味着，实体的命名等同于领域专家使用的领域语言。这种无处不在的语言在有界上下文的边界中是有效的，大多数时候它相当于一个子域。无处不在的语言完全独立于其他子域是完全必要的。

![](img/2141b9d1b94727c2e9a51fbabe74e750.png)

普遍存在的语言

这意味着，我们可以在多个有界上下文中拥有一个预订实体，并且该实体的含义可以不同。例如，预订子域中的预订可以包含许多字段，而另一个子域中的预订实体可能只有几个字段。

有时候，实体可能看起来非常相似甚至相同，但是在这里你必须注意远离传统的 OOP 思维，避免抽象。通常，在 OOP 中，我们被告知复制是万恶之源，抽象是救星，但是在 DDD 的案例中，复制并不是坏事。实际上，DDD 的复制比抽象好得多，因为那样的话，子域可以更加独立，这也是它的初衷。

# 结论

当迁移到微前端架构时，必须做的最重要的事情是一个干净的域分割，这样微前端就只共享很少的依赖项。这是独立部署的基础，也是微前端架构的主要原因，因此微前端架构应该始终采用领域驱动设计。

顺便说一下，如果你对领域驱动设计感兴趣，我可以推荐两本书:

*   领域驱动设计精华(沃恩·弗农)
*   领域驱动设计(埃里克·埃文斯)

如果你喜欢这篇文章，请考虑用我的推荐链接来支持我:

[](https://medium.com/@stefan.haas.privat/membership) [## 通过我的推荐链接-斯特凡·哈斯加入媒体

### 阅读斯特凡·哈斯的每一个故事(以及媒体上成千上万的其他作家)。您的会员费直接支持…

medium.com](https://medium.com/@stefan.haas.privat/membership) 

**其他有趣的阅读:**

[](/secure-frontend-authorization-67ae11953723) [## 停止在前端进行令牌认证

### 为单页应用程序构建安全认证过程的现代方法。

levelup.gitconnected.com](/secure-frontend-authorization-67ae11953723) [](/moduliths-in-angular-with-nx-b8b0076794fb) [## 以 Nx 为单位的角度模数

### 使用 DDD 和 Monorepos 创建可持续应用

levelup.gitconnected.com](/moduliths-in-angular-with-nx-b8b0076794fb) [](/your-first-angular-microfrontend-58950768a465) [## 你的第一个角形微前端

### 这是一个关于如何创建一个简单的 angular 应用程序来使用另一个应用程序的模块的分步指南…

levelup.gitconnected.com](/your-first-angular-microfrontend-58950768a465)