# 用组合 API 构建 VueJS 应用程序

> 原文：<https://levelup.gitconnected.com/structuring-vuejs-apps-with-the-composition-api-de97107d4482>

Vue 3 向我们介绍了组合 API，它旨在解决 VueJS 应用程序中的代码重用和可维护性。这里有一个快速的概述和一些关于如何构建代码的建议。

![](img/37ff7f16f00ad617cce14998a90590e8.png)

阿迪·戈尔茨坦在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

[Vue 3](https://github.com/vuejs/vue-next/releases/tag/v3.0.0?ref=madewithvuejs.com) 来了！随之而来的是备受关注的[组合 API](https://v3.vuejs.org/guide/composition-api-introduction.html) ，它旨在解决当前 VueJS 应用程序中代码重用的困难。

我说的“代码”重用是特指，而不是“组件”重用，因为对于完全自包含的组件，组件重用总是可能的。然而，组合 API 使开发人员能够将代码(功能)与组件本身(表示)分开。

当然，我们总是能够通过使用 [Vuex](https://vuex.vuejs.org/) 在功能和表现之间建立某种程度的分离。然而，Vuex 要求我们将功能保持在定义主商店的地方，在我看来，这经常被滥用。

Vuex 主要是一个状态存储，但是开发人员使用它作为一种快速共享状态和动作的方式，只需要一两个组件，因此不需要全局共享。

React 开发人员将熟悉这个概念，因为组合 API 在它试图实现的方面类似于 React Hooks(尽管我在这一点上相信其他开发人员的话，因为我对 React Hooks 几乎没有经验)。

# 老办法

让我们看一些代码。

从一些我确信你从未见过的东西开始；这段代码用几个按钮设置了一个 count 变量，用来增加或减少值。

至此，生活简单了。快速阅读代码可以为开发人员提供使用代码所需的所有信息。但是想象一下，我们已经计算出了价值，存储了交互和到处都有的事件。

因为您需要在组件的定义(方法/计算/数据等)中分割代码。)与其功能(计数、数据检索等)相反。)，东西很快就变得乱七八糟，读起来难多了。

# 新的方式

现在让我们看一下相同的组件，但是使用的是组合 API。

首先，我们现在调用“setup”函数，而不是“data”，在这里我们使用“ref”函数创建一个名为“count”的新变量，并将其初始化为 0。

因为我们在相同的范围内初始化和使用变量(即“setup”函数的范围)，所以我们可以直接访问它，而不需要“this”(这在 setup 函数中不管用)。

然后，我们创建与之前相同的两个函数，但是现在它们是在 count 变量的旁边声明的。这意味着我们可以根据功能将代码分组，这使得维护开发人员的工作变得更加容易。

最后，我们返回我们创建的东西，以便它们在组件范围内可用。

所以我们设法在代码中逻辑地分离功能。但是现在假设另一个组件希望使用 add & take 函数；或者需要访问 count 的值。“传统上”(如果你可以这么说 VueJS 的话)，这是你引入 Vuex 的地方。

Vuex 本身没有任何问题，它是有目的的。然而，由于状态和商店的组织方式，你又一次得到了组件的关键功能，而不是组件本身。

而且，你现在已经和 Vuex 完全绑在一起了；组件离不开它。如果您想在另一个项目中重用该组件，您必须随身携带 Vuex 存储的一部分。

# 创造有用的分离

这是组合 API 的真正改变者所在的地方。

我们可以将功能分离到单独的文件中，并将它们导入到我们希望使用的任何组件中。

例如:

这是相同的代码，除了现在`count`、`add`和`take`可用于我们的整个代码库。功能很容易移植，组件也变得更容易移动(虽然仍然依赖于`counter.js`文件，但它不需要 Vuex 来提供)。

# 构建您的 API

以前，我写过关于[构建 VueJS 组件以供重用的文章](/structuring-vue-components-for-reuse-c6f2444b6167)。那篇文章关注的是我如何通过分离数据的检索和表示来创建跨整个应用程序(实际上是跨多个应用程序)可重用的组件。

组合 API 又增加了一层:我把非组件代码放在哪里？我的`.js`和`.ts`文件？

我看到过各种建议，有些人在 src 根目录下创建一个“composables”或“hooks”文件夹，并在那里存储所有的功能。

然而，我觉得这让我们处于与 Vuex 相似的情况(尽管没有那么严重)。如果您希望跨项目重用代码，您仍然需要从多个目录中获取多个文件。

对于像计数器这样高度通用的东西，这是有意义的。您可能想要没有组件的代码，反之亦然。

但是如果我们要考虑一些更复杂的东西(比如一个通用的“联系我们”表单或认证)，我发现将代码存储在组件本身旁边是一种更干净的组织文件的方式。

以联系我们表格为例。我将创建以下文件夹结构:

`src/components/contact`

在`ContactForm.vue`和`index.ts`中有两个文件(是的`.ts`，TypeScript 对于组合 API 来说非常强大)。

然后，如果我需要在应用程序的其他地方访问联系人表单中的数据(例如确认组件或其他类似组件)，我可以`import { data } from './src/components/contact'`并立即访问其中的数据。

此外，如果我想在另一个项目中使用相同的联系方式，我可以将整个文件夹复制粘贴到我的新项目中，嘿，很快，我们就可以开始了！

我将通过使用 Composition API 和 Firebase 身份验证创建一个身份验证“库”来进一步探索这一点，请继续关注！

但是现在，我希望您可以看到组合 API 如何进一步帮助创建功能，这些功能不仅更具可重用性，而且更易于维护。

单个组件可以从许多位置导入功能，并使用它们来组成自己的行为。这允许您在逻辑关注点之间创建一个清晰的分离，当其中一个关注点有 bug 时，降低维护成本。

库已经开始出现(参见 [vue-composable](https://pikax.me/vue-composable/) 和 [vue-use](https://github.com/antfu/vueuse) ),它们提供常见的实用功能，如鼠标交互、本地存储和本地 API 交互。

对于那些还没有的人，试一试吧！开始前进，未来你会感激的！