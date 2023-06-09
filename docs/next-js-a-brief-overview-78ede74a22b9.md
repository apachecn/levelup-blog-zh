# Next.js 简要概述

> 原文：<https://levelup.gitconnected.com/next-js-a-brief-overview-78ede74a22b9>

js 是一个灵活的 React 框架，它为我们提供了创建快速 web 应用程序的构件。

![](img/0bab5fa2d5c5750a75295e7932093c8d.png)

Next.js 是一个构建在 Node.js 之上的开源框架，以 React 为基础。

本文假设您熟悉 [React](https://reactjs.org/) ，并且已经使用了一段时间，现在想要将 [Next.js](https://nextjs.org/learn/foundations/about-nextjs) 添加到您的工具集中。

Next.js 旨在提供一流的开发人员体验和许多内置功能，例如:

*   自动代码分割加快页面加载速度
*   具有优化预取的客户端路由
*   直观的基于页面的路由系统(支持动态路由)
*   预渲染，静态生成(SSG)和服务器端渲染(SSR)都是基于每页支持的。
*   内置的 CSS 和 Sass 支持以及对任何 CSS-in-JS 库的支持。
*   支持快速刷新的开发环境
*   使用无服务器功能构建 API 端点的 API 路由
*   完全可扩展。

如果您还不熟悉 Next.js，您可能会想知道所有这些东西是什么意思。让我们对其中一些进行详细阐述。

# **代码拆分**

Next.js 自动执行**代码拆分**，因此每个页面只加载该页面所必需的内容。这意味着，当加载主页时，最初不会提供其他页面的代码。这确保了即使我们有数百个页面，主页也能快速加载。

只为我们请求的页面加载代码也意味着页面变得孤立。如果某个页面抛出错误，应用程序的其余部分仍将按预期工作。

# 客户端导航

在 Next.js 中，我们在`pages`下创建路径作为文件，并使用内置的`Link`组件链接到它们。不需要路由库。

# 预取

在 Next.js 的生产版本中，每当一个`Link`组件(Next.js 版本的< a >标签)出现在浏览器的视窗中，Next.js 就会自动在后台预取链接页面的代码。因此，当用户点击链接时，目标页面的代码已经在后台加载，页面转换几乎是即时的。

> 因此，Next.js 通过代码分割、客户端导航和预取自动优化我们的应用程序以获得最佳性能。

# 预渲染

默认情况下，Next.js 会预先呈现每个页面。也就是说，Next.js 预先为每个页面生成 HTML，而不是由客户端 JavaScript 来完成。预渲染可以带来**更好的性能**和 **SEO** 。

每个生成的 HTML 都与该页面所需的最少 JavaScript 代码相关联。当浏览器加载一个页面时，它的 JavaScript 代码运行并使页面完全交互。这个过程叫做**水合**。

Next.js 有两种形式的预渲染:**静态生成**和**服务器端渲染**。区别在于它何时为页面生成 HTML。

*   **静态生成**是在*构建时*生成 HTML 的预渲染方法。然后在每个请求中重用预先呈现的 HTML。
*   **服务器端呈现**是在每个请求上生成 HTML 的预呈现方法。

Next.js 让我们选择每个页面使用哪种预渲染方法。我们可以创建一个“ ***混合***”next . js 应用程序，对大多数页面使用**静态生成**，对其他页面使用**服务器端呈现**。

建议尽可能使用静态生成(有数据和无数据),因为我们的页面可以构建一次并由 CDN 提供服务，这比让服务器在每次请求时呈现页面要快得多。

然而，如果我们不能在用户请求之前预先呈现页面，静态生成就不是一个好主意。也许我们的页面显示频繁更新的数据，并且页面内容在每次请求时都会改变。

在这种情况下，我们可以使用**服务器端渲染**。它会慢一些，但是预渲染的页面将总是最新的。或者我们可以完全跳过预渲染，使用**客户端 JavaScript** 来填充频繁更新的数据。

# 客户端渲染

如果我们不需要预渲染数据，我们也可以使用一种叫做**客户端渲染**的策略，它:

*   静态生成(预呈现)不需要外部数据的页面部分。
*   当页面加载时，使用 JavaScript 从客户端获取外部数据，并填充其余部分。

# API 路线

Next.js 支持 API 路由，这让我们可以轻松地创建一个 API 端点作为 Node.js 的无服务器函数。我们可以通过在`pages/api`目录中创建一个函数来做到这一点。

# 结论

在本文中，我试图用非常简单的术语来解释 Next.js 的一些主要构建块。对于一直在使用 Next.js 但尚未真正掌握这些构建块的人来说，本文也可以作为一个复习工具。

如果你喜欢这篇文章，请留下几个或很多的掌声。谢了。