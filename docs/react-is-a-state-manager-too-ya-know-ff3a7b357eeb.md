# 反应也是一个国家经理，你知道！

> 原文：<https://levelup.gitconnected.com/react-is-a-state-manager-too-ya-know-ff3a7b357eeb>

## 你可能不需要 Redux…或者上下文。使用 React 的内部组件状态，而不是复杂的第三方解决方案。

![](img/4dd72d258143b1591c530349ff813f57.png)[](https://gitconnected.com/portfolio-api) [## 组合 API -轻松发展您的编码事业| gitconnected

### 消除在每个单独位置手动更新您的详细信息的痛苦。只需在您的中更改一次数据…

gitconnected.com](https://gitconnected.com/portfolio-api) 

**向 React 内部状态的简单致敬**

我写 React 已经快两年了，毫无疑问，它是我在 web 开发领域最喜欢使用的工具。就像整个软件行业一样，React 也在不断发展，特别是在它管理状态的方式上。从 16.8 版本开始，React 推出了一个[的新 hooks API](https://reactjs.org/docs/hooks-intro.html) ，它实际上颠覆了生态系统。

我目前的目标不是专门关注这些 API 的变化，而是它们对我们在 React 应用程序中管理状态的方式的影响。React 最大的优点之一是它在配置、工具和实现方面是多么的独立。然而，当谈到应用程序范围的状态管理时，第三方库通常是事实上的选择，React 本身被认为不如处理大规模不可变状态对象。

我希望从使用 React 应用程序的第一步开始，就反对将这种思维模式作为默认选择。当然，我承认肯定会有一些场景，通常与规模相关，这些外部工具使我们作为开发人员的生活变得更容易。

这不是一篇劝阻你不要使用 Redux 的博客文章——我个人真的很喜欢使用它，并发现在适当的情况下它非常强大。然而，你的 Todo 应用或个人网站绝对不需要 [Redux](https://redux.js.org/) 或最近更流行的状态管理变体 [React Context](https://reactjs.org/docs/context.html#contextprovider) 。在这篇文章的结尾，希望我至少能让你在下一个 React 项目中使用这些工具之前三思。

所以让我们开始吧。

*免责声明:React 的所有实现，无论状态管理方法如何，都将包括纯粹的钩子实现。如果你不熟悉钩子，我建议你在继续之前先看看上面的链接。*

# 道具钻井…唉

我看到 React 开发人员使用像 Redux 这样的第三方库或者定制的上下文实现的最常见原因是为了避免[道具训练](https://kentcdodds.com/blog/prop-drilling)。当子组件需要某个特定的状态，但包含该状态的父组件在组件树中比它高几个级别时，就会发生适当的钻取。当然，中间组件不关心这种状态，所以像 Redux 和 Context 这样的解决方案旨在从本质上省去中间人。

这里有一个基本的 Redux 设置的常见例子，以避免道具钻孔(记住，这是一个很小的例子，所以*钻孔*将相当浅):

Redux store 由一个`search`字符串、一个`episodes`数组(感谢可爱的 [Rick 和 Morty API](https://rickandmortyapi.com/) )和一个`error`对象组成。我敦促你们思考的第一个问题是，为什么这些东西需要在商店里，或者换句话说，全球状态。尤其是像搜索字符串这样短暂的东西。

这里有一个使用 React 上下文的类似版本:

这两种方法都解决了道具钻探的问题，但是我强烈建议你考虑一下它们可能会在应用程序的生命周期中引入的问题或错误。我承认这不是一个真正的*应用*，考虑到它获取一个端点并呈现一些字符串，但我认为这是大多数应用的开始，尤其是我们的副业项目。我们没有预料到我们想要做的所有事情，我们想要添加的功能，以及这些功能是否会从这样一个僵化的系统中受益。

更进一步，我们的应用程序如何从全球状态的`episodes`中获益？作为前端工程师，通过以这种方式存储剧集，我们基本上创建了一个客户端数据库，我们必须不断地与我们的实际数据库进行比较(当然，假设有一个数据库)。

我们失去了唯一的真理来源，仅仅是为了避免一个(或两个)额外的请求。这是为了什么？有些人可能会说，它允许更容易地过滤或查询客户端数据，以避免“不必要的”后端请求，但我认为，与应用程序前端和后端之间可能发生的数据停滞相关的潜在错误相比，你在前端感受到的便利性优势毫无意义。

顺便说一下，有些人可能认为如果他们没有后端，这可能不适合他们，但我想让这些人更进一步，并问为什么，如果他们那么小，甚至有一个外部状态管理器。

# 错误处理

与使用 Redux 或 Context 这样的状态管理工具相关的一个常见思维模式是要么全有，要么全无。换句话说，如果你要用它，就用它来做所有的事情。我曾经这样想。然而，我已经改变了我的论调，现在以相反的心态接近 Redux。现在，我坚信你应该只在绝对必要的时候给你的商店添加一些东西。我可以自信地说，这种情况比您想象的要少得多，尤其是在处理应用程序中的错误时。

请注意，在上述每种方法中，我都在全局存储中加入了一个错误状态。这是我在 Redux 和其他状态管理系统中看到的常见做法。目标大概是以某种方式裁剪给定的错误消息，在特定的视图中给出它的上下文(当然与 React 上下文无关)。

这引入了一个相当麻烦的范例，因为每次我们设置错误状态时，我们都必须清除它。我在大规模 Redux 代码库中一次又一次地遇到这个令人头痛的问题，作为开发人员，几乎你创建的每个动作都必须有一个相反的，或者“清理”的动作来清除产生的状态——因为它是**短暂的**。

> 对短暂的状态使用 React，这种状态对应用程序没有全局影响，并且不会以复杂的方式变异。—丹·阿布拉莫夫在一期 [Redux Github](https://github.com/reduxjs/redux/issues/1287#issuecomment-175351978) 中

我几乎可以向您保证，您的应用程序中包含的短暂状态比您想象的要多。

# 生态系统压力

作为 React 开发人员，有大量说教的观点不断掩盖我们所做的工作和我们如何构建应用程序，有很多次我加入 Redux 只是因为它是一个受欢迎的工具，我可以把它添加到我的简历中。但是，它真的有益于我们的应用程序吗？

现在，如果你谷歌“反应状态管理”，你的结果将是全面的。“上下文让 Redux 过时了！！!"、“MobX 为状态管理提供了突破性的新观察者范式”、“新的 Redux hooks API 带来了对 React 状态管理的全面改进！”(以上均为杜撰标题)。当我早些时候提到 React 的一个我最喜欢的部分是它的非个人化，这当然不适用于 React 生态系统，这是 2019 年末 React 开发人员更令人沮丧的痛点之一。

如果有任何一点我可以理解的话，那就是如果学习反应是一个线性的路径，它应该采取*大致*这种形式:

1.  **学习 JavaScript**
2.  不，真的，我的意思是学习 JavaScript
3.  **学习反应**
4.  **在 React 中构建项目**(没有外部状态管理器)
5.  **一旦你经历了没有全局状态的痛点**，学习 Redux 或另一个第三方状态管理器

更多的时候，恐怕路径是 1 的 25%，然后 3，然后 5。

![](img/cfb373fd079a87cbb6568f1b1fa3401d.png)

花了 5 分钟/ JS 和 30 分钟/ React 尝试学习 Redux 的开发人员

重申一下，我不是说你不应该学习 Redux，或者你的应用程序不需要 Redux。Redux 在需要它的环境中非常出色。我只是鼓励你去思考你正在构建的是什么，如果引入像 Redux 这样的外部工具或者使用你自己的定制状态管理器(danger ⚠️)来增强它，它是否真的会更好。

具体来说，Context 是管理 React 状态的一个当前流行的解决方案，我曾经是宣传列车上的[乘客。但是后来我把这个系统整合到了几个生产应用程序中。在讨论有争议的 *Redux vs Context* 辩论时，我认为有一个类比是合适的，那就是将 Redux 比作豪华奔驰，将 Context 比作 1975 年的福特 Pinto](/implementing-redux-style-state-management-with-reacts-usecontext-usereducer-hooks-c1c5596d9619) 。这两种方法都会把你带到你需要去的地方，这只是你想要或需要多安全才能到达那里的问题。

似乎有赞成(或反对)的论点？)上下文围绕 Redux 在幕后使用`React.Context`这一事实。然而，上下文 API 本身并没有考虑状态管理。相反，它只是一个解决方案，使数据在组件树中从一个组件到另一个更深的组件可用。不管这种立场的意图是什么，Redux 有许多 Context 没有的内置性能增强器、渲染救助等。以上面的汽车为例，将一个代码库从 Redux 转换成纯粹的上下文实际上是从你的汽车中取出安全气囊和安全带。是的，它还能开，但是不太安全了。

# 哦嘿，反应过来

让我们用一个使用 React 的类似例子来回顾一下前面两个使用 Redux 和 Context 的设置:

您应该注意到这里有一些不同之处。首先，代码一般来说更轻，我们也放弃了我们的`reducer`。`Search`组件不再管理自己的状态——它从其父`Content`组件接收自己的状态和状态设置器。这就是通常所说的“[提升状态上升](https://reactjs.org/docs/lifting-state-up.html)”。

此外，由于这种父子重组，我们可以免费获得实时搜索过滤的额外好处。我的意思是，如果你搜索一集，你可以立即看到基于你的搜索结果，而不是基于你点击搜索按钮。

看起来不错，对吧？我们到底要换多少才能到这里？我们所做的就是删除任何与之前的 Redux 或上下文示例相关的样板文件，并将一些道具从父母传递给孩子。请注意，在这个场景中，父子道具关系是如何以一种非常令人满意的方式发生的。我们的父组件`Content`管理我们应用程序的所有必要状态。

同样，我将说明这是一个非常简单的应用程序，并不真正类似于我们在围绕状态管理做出这些架构决策时通常要处理的内容，但我恳请您考虑将这种方法扩展到您可能遇到的任何问题。详细地说，我的意思是仅仅因为有几个组件可能关心一个特定的状态块**并不意味着**那个状态块需要是*全局的*。您组合组件的方式可以很容易地治疗您可能归因于正确的训练的这种疾病。

我甚至更进一步，认为 Redux 会让我们这些 React 开发人员变得懒惰。当任何状态可以与任何组件连接时，不管它在组件树中的位置如何，内聚的组件组合通常是事后才想到的。

[迈克尔杰克逊](https://medium.com/u/7f9567e0d71c?source=post_page-----ff3a7b357eeb--------------------------------)、 [React 培训](https://reacttraining.com/)的联合创始人、 [React-Router](https://egghead.io/podcasts/react-router-with-michael-jackson) 的联合创始人最近发表了一个关于组件合成的力量的优秀的[、**短视频**、](https://www.youtube.com/watch?v=3XaXKiXtNjw&feature=youtu.be)在这里我就不尝试复制了。然而，我鼓励你去看看，因为这是一个特殊的补救措施，可以解决我们作为 React devs 在传递道具和试图管理全局状态时所经历的大部分困难。

# 向前迈进，用开放的心态去创造！

在我的开发生涯中，我尝试过几种不同的技术，但是很少有像 React 这样让我兴奋的。现在比以往任何时候都更是一个成为 React 开发人员的绝佳时机，因为前端和完整堆栈之间的界限越来越模糊，老实说，这可以保证一篇属于自己的博客文章。

React [悬念](https://reactjs.org/docs/concurrent-mode-suspense.html)和[并发](https://reactjs.org/docs/concurrent-mode-reference.html)模式是另外两个突破性的 API，该团队可能会在明年年初发布，增加代码分割和非阻塞渲染等核心功能，这将从根本上改变 React 的工作方式，并显著增强开发人员和用户的体验。

仅仅因为开源项目在 Reddit 上得到了很多支持，并不意味着你必须使用 TypeScript、Redux、GraphQL、Apollo Client 等等。**预优化是万恶之源**。从简单开始，根据复杂性需要添加工具。React 的内部状态完全有能力处理你的大多数普通应用，尤其是刚刚起步的宠物项目(往往最终会在你的回购收集中落灰)。

Redux 和其他内部状态管理器可以成为添加到 React 工具包中的不可思议的工具，我只是鼓励您更加注意何时以及如何使用它们。

感谢您的倾听👋🏻

与我联系[这里](https://www.tuckerblackwell.com/)