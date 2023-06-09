# 2019 年前 30 名 React 面试问题

> 原文：<https://levelup.gitconnected.com/everything-about-react-10512639a01e>

这篇文章将作为你准备 React 面试的指南。但是在开始 React 面试问题之前，我们先来快速了解一下 React 的需求和在市场上的地位。截至今天，Github 上大约有 1000 名贡献者。像虚拟 DOM 和可重用组件这样的独特特性使得这个库被广泛采用。看看下面的图表，它显示了流行的 JS 框架的趋势:

![](img/9c758a5fba0bb1cfd886ebce835bed71.png)

Q1:什么是反应？

*   React 是脸书在 2011 年开发的前端 JavaScript 库。
*   它遵循基于组件的方法，这有助于构建可重用的 UI 组件。
*   它用于开发复杂的交互式 web 和移动 UI。
*   它在 2015 年才开源，并有一个最大的社区支持它。

**Q2:React 的特点是什么？**

*   它使用**虚拟 dom** 而不是真实 dom 来管理 UI。
*   它能够使用**服务器端渲染**。
*   它遵循**单向数据流**。
*   你的用户界面被分成模块化和可重用的组件。
*   它是纯 JavaScript——它没有创建任何特定于领域的功能。
*   它提供了钩子和组件生命周期方法来管理副作用和状态。
*   它使用组件层次结构，数据从父级传递到子级。

**Q3:列出 React 的一些主要优势。**

*   它提高了应用程序的性能。
*   这是一个轻量级的库。
*   它可以很容易地用于客户端和服务器端渲染。
*   JSX 提供了有效的代码可读性。
*   它可以与其他框架集成，如 Meteor 等。
*   使用 React，编写 UI 测试用例极其容易。
*   它只是关注应用程序的视图层，而不是一个笨重臃肿的框架。

**Q4:React 的局限性是什么？**

*   React 只是一个库，不是一个成熟的框架。你必须定义你自己的依赖关系。
*   编码变得复杂，因为它使用内联模板和 JSX。

什么是 JSX？

JSX 是一种类似 HTML 的语法，用于声明 React 元素和用户界面。这是 React 使用的一种文件类型，它利用了 JavaScript 的表现力和 HTML 模板语法。这使得 HTML 文件非常容易理解。这个文件使应用程序更加健壮，可读性更好。

**Q6:为什么浏览器不能读取 JSX？**

浏览器只能读取 JavaScript 对象，但是 JSX 不是一个普通的 JavaScript 对象。因此，要使浏览器能够读取 JSX，我们首先需要使用像巴别塔这样的 JSX 转换器将 JSX 文件转换成 JavaScript 对象，然后将它传递给浏览器。

**问题 7:什么是 React 组件？**

React 组件是一些小的、可重用的代码片段，它们返回要呈现到页面上的 React 元素。React 组件的最简单版本是返回 React 元素的普通 JavaScript 函数。

组件也可以是 ES6 类。

**Q8:解释 React 中 render()的用途。**

每个 React 组件都需要有一个`render()`方法。它返回一个 React 元素，这个元素是原生 DOM 组件的表示。如果需要呈现一个以上的 HTML 元素，那么必须将它们组合在一个封闭标签中，如`<form>`、`<group>`、`<div>`等。这个函数必须保持纯净，也就是说，每次根据当前状态调用它时，它必须返回相同的结果。

**Q9:什么是道具？**

**Props** 是 React 组件的输入。它们是从父组件传递到子组件的数据。

**Q10:什么是状态？**

状态是存储在单个组件中的数据。这和道具一起决定了组件的渲染和行为。当与组件相关的一些数据随时间变化时，组件需要状态。

*例如，一个复选框组件可能需要在其状态中被选中。*

状态也可以使用像 Redux 这样的库进行全局分离和存储。

**Q11:状态和道具的区别。**

状态和道具之间最重要的区别是道具是从父组件传递的，但是状态是由组件本身管理的。

一个组件不能改变它的属性，但是可以改变它的状态。虽然父组件可以改变属性，但不能改变子组件的状态。

**Q12:React 中如何使用箭头函数？**

箭头函数是用于编写函数表达式的精简语法。它们也被称为‘胖箭’(`=>`)函数。这些函数允许我们正确地绑定组件的上下文，因为在 ES6 中，自动绑定在默认情况下是不可用的。

**问题 13:React 中的事件是什么？**

在 React 中，事件是对鼠标悬停、鼠标点击、按键等特定动作的触发反应。处理这些事件类似于处理 DOM 元素中的事件。

**Q14:React 中的合成事件是什么？**

合成事件是围绕浏览器本地事件的跨浏览器包装器。它与浏览器的本地事件具有相同的接口，包括`stopPropagation()`和`preventDefault()`，除了这些事件在所有浏览器中的工作方式相同。它通过自动使用事件委托来实现高性能。

简单地说——它是 React 对本地事件的包装。

**Q15:React 中的裁判是什么？**

它是一个属性，用于存储对特定 React 元素或组件的引用，该引用将由组件呈现配置函数返回。它用于返回对 r `ender()`返回的特定元素或组件的引用。当我们需要访问 React 呈现的原生 DOM 节点时，它们就派上了用场。

**问题 16:列举一些你应该使用参考文献的例子。**

*   当您需要管理焦点时，选择文本或媒体播放
*   要触发命令式动画
*   与第三方 DOM 库集成

**Q17:你对受控和非受控组件了解多少？**

受控组件:

*   他们没有保持自己的状态
*   数据由状态或父组件控制
*   它们通过接收当前值，然后通过回调通知更改

非受控组件:

*   他们保持自己的状态
*   数据由 DOM 控制

**Q18:什么是高阶元件？**

高阶组件是重用组件逻辑的一种高级方式。基本上，这是一种源自 React 的组合性质的模式。HOC 是在其中包装另一个组件的定制组件。它们可以接受任何动态提供的子组件，但不会修改或复制输入组件的任何行为。你可以说 HOC 是“纯”组件。

**Q19:列出 HOC 的用途。**

HOC 可用于许多任务:

*   代码重用、逻辑和引导抽象
*   渲染装饰
*   状态抽象和操作
*   道具操作

**Q20:什么是纯成分？**

纯组件为您管理`shouldComponentUpdate`函数，只有在状态改变时才会重新呈现。

**Q21:React 中如何模块化代码？**

我们可以通过使用导出和导入属性来模块化代码。它们有助于在不同的文件中分别编写组件。

**Q22:React 组件生命周期的不同阶段是什么？**

*   **挂载**:这是组件即将开始其生命之旅并被添加到 DOM 的阶段。React 有四种内置的挂载方法:

1.  构造函数()
2.  getDerivedStateFromProps()
3.  渲染()
4.  componentDidMount()

*   **更新**:一旦组件被添加到 DOM 中，只有当属性或状态发生变化时，它才可能更新和重新呈现。那只发生在这个阶段。React 有五种内置的更新方法:

1.  getDerivedStateFromProps()
2.  shouldComponentUpdate()
3.  渲染()
4.  getSnapshotBeforeUpdate()
5.  componentDidUpdate()

*   **卸载:**这是组件生命周期的最后一个阶段，在这个阶段，组件被销毁并从 DOM 中删除。React 只有一个被调用的内置方法:

1.  componentWillUnmount()

[*了解更多关于生命周期的信息*](https://medium.com/@__jay__singh__/react-lifecycle-2c63aee11c09)

**Q23:React 中按键的意义是什么？**

键用于标识唯一的虚拟 DOM 元素，以及驱动 UI 的相应数据。它们通过回收 DOM 中的所有现有元素来帮助优化呈现。这些键必须是唯一的数字或字符串，React 只是对元素重新排序，而不是重新呈现它们。这导致了应用程序性能的提高。

**Q24:解释通量。**

Flux 是一种实施单向数据流的架构模式。它控制派生数据，并使用对所有数据拥有权限的中央存储来实现多个组件之间的通信。整个应用程序中的任何数据更新都只能在这里进行。Flux 为应用程序提供了稳定性，并减少了运行时错误。

**Q25:Redux 是什么？**

Redux 是一个用于管理应用程序状态的开源 JavaScript 库。它通常与 React 或 Angular 等库一起用于构建用户界面。这是通量概念的一种实现。

**Q26:Redux 遵循的三大原则是什么？**

*   ***单一事实来源:*** 整个应用程序的状态存储在一个单一存储内的对象/状态树中。单一状态树使得跟踪随时间的变化以及调试或检查应用程序变得更加容易。
*   ***状态只读:*** 改变状态的唯一方法是触发一个动作。动作是描述变更的普通 JS 对象。就像状态是数据的最小表示一样，动作是数据变化的最小表示。
*   ***用纯函数做改变:*** 为了指定状态树如何被动作转化，你需要纯函数。纯函数是那些返回值仅依赖于参数值的函数。

**Q27:列出 Redux 的组件。**

Redux 有以下组件:

*   **动作:**是描述所发生事情的宾语。
*   **减速器:**是决定状态会如何变化的地方。
*   **存储:**整个应用的状态/对象树。

**Q28:Redux 中的动作是如何定义的？**

React 中的动作必须有一个`type`属性来指示正在执行的动作的类型。它们必须被定义为一个字符串常量，你可以添加更多的属性和有效载荷。在 Redux 中，动作是使用称为动作创建器的函数创建的。

**Q29:解释减速器的作用。**

Reducers 是纯函数，它指定应用程序的状态如何响应一个动作而改变。Reducers 通过接受先前的状态和动作来工作，然后返回一个新的状态。它根据动作的类型确定需要进行哪种更新，然后返回新值。如果不需要做任何工作，它就返回原来的状态。

**Q30:商店在 Redux 的意义是什么？**

store 是一个 JavaScript 对象，它可以保存应用程序的状态，并提供一些助手方法来访问状态、调度操作和注册侦听器。应用程序的整个状态/对象树保存在单个存储中。因此，Redux 非常简单且可预测。我们可以将中间件传递给商店来处理数据，并记录改变商店状态的各种操作。所有的动作通过 reducers 返回一个新的状态。

我希望这一套 React 面试问答能帮助你准备面试。万事如意！