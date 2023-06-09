# React 的模块联合示例

> 原文：<https://levelup.gitconnected.com/a-module-federation-example-for-react-1fa29d6ac07b>

## 具有模块联合的微前端

查看通过模块联合实现的 React 微前端解决方案

![](img/169b4700506e68b244fad8b7e3536098.png)

# 前情提要…

这个例子的基础是我不久前写的另一篇[文章](/a-micro-frontend-solution-for-react-1914b19663b)，展示了带有 React 的微前端。简言之，该应用程序是一个法国牛头犬配件网店，其中的主机应用程序是一个简单的 React 应用程序，带有产品列表和购物车页面。这两条路线是渲染一个产品和一个购物车微前端。查看[故事](/a-micro-frontend-solution-for-react-1914b19663b)了解更多详情。在这篇文章中，我想介绍一种使用模块联合的微前端的可能实现，并从几个角度比较这两种解决方案。如果你想详细了解这个例子，下面是一份报告:

[](https://github.com/burzaszsolt/react-module-federation) [## burzaszsolt/react-模块-联邦

### 这是一个使用 javascript 方法将微前端与 react 结合使用的例子。如果你有 docker，那就是…

github.com](https://github.com/burzaszsolt/react-module-federation) 

# 模块联盟

您可能从未听说过这个 Javascript 架构，因为它是 Webpack 5 中引入的一个非常新的特性。最好的描述来自发明者[本人](https://medium.com/@ScriptedAlchemy):

> 模块联合允许 JavaScript 应用程序从另一个应用程序动态加载代码—在此过程中，共享依赖关系，如果使用联合模块的应用程序没有联合代码所需的依赖关系— Webpack 将从该联合构建源下载缺少的依赖关系。

听起来很酷，对吧？如果你想了解更多关于这个话题的信息，请先阅读这个故事，然后再回来。现在让我们来看看，为了使用模块联合作为我的应用程序的微前端架构的基础，我必须做哪些更改。

# **解决方案**

## 遥控器

为了将我的微前端变成远程应用，我所要做的就是将`ModuleFederationPlugin`添加到我的 webpack 配置文件中。

产品微前端的 webpack 配置

在插件配置中，我将`ProductService`定义为一个我想从这个应用程序中公开的组件，这样它就可以在其他应用程序中使用。配置的另一个重要部分是`shared`对象，在这里我可以列出主机和远程之间共享的所有依赖项。

## 主持

有了这些改变，我就有了一个可以使用的遥控器。我所要做的就是在三个小步骤中改变主机，这样它就可以渲染微前端。第一步是更改 webpack 配置:

在`ModuleFederationPlugin`配置中，我将产品和购物车微前端定义为`remotes`。这允许我在我的组件中访问它们。

第二步是在我的`index.html`中添加所有遥控器的`remoteEntry.js`。这些包很小(几 kB ),包含关于模块的最少信息。

第三步(我最喜欢的)是在主机中渲染遥控器:

主机应用程序中的产品组件

我可以从`mfProducts`遥控器惰性导入`ProductService`，并在我的`Products`组件中渲染它，就这样。就是这么简单。🎉🙌

## **双向主机**

正如你可能注意到的，我还在微前端中公开并添加了远程主机应用程序。这意味着我所有的应用都是消费者和远程用户，这使得它们被称为双向主机。这样做允许我在我的微前端渲染主机应用程序，这样我就可以轻松地开发它们，就像它们是一个应用程序一样。我的微前端的入口点是呈现下面组件的`index.js`:

产品微前端中的 App.js

我可以像处理遥控器一样处理暴露的主机应用程序。结果是，不管我在看哪个应用程序，它们看起来都一样。

# 结论

在这一章中，我想观察一下我的同一个应用程序的两个实现的一些方面，看看它们之间有什么不同。

## 暴露应用程序

在前面的例子中，我从每个微前端创建了一个库，可以通过 window 对象在其他应用程序中访问这个库。这个库包含了一些方法，我实现了这些方法来渲染或卸载微前端。这并不是一个复杂的解决方案，但有了`ModuleFederationPlugin`就更简单了。

## 使用应用程序

我很惊讶我可以如此轻松地使用主机上的遥控器。之前我创建了一个定制的`useMicrofrontend` React 钩子来动态地将微前端包加载到应用程序中。对于模块联合，默认情况下是支持的。

## 表演

这是模块联合的最大优势之一。通过共享依赖项，包的大小减少了很多。在前面的实现中，导航到 cart 页面会产生大约 2.3MB 的下载数据，这是 cart 微前端(开发构建)的包大小。对于同一个页面，通过模块联合传输的总数据量只有大约 700kB。即使在如此小的应用程序中，这也是一个巨大的差异。

## 发展

在我的第一个例子中，我可以将每个微前端作为一个独立的应用程序运行，但要将它们集成到主机应用程序中，我必须在每次更改时重新构建它们。使用双向主机实现，我可以立即检查我在任何应用程序中所做的每个更改，并测试它如何集成到整个应用程序中。这使得开发更加舒适和高效，同时保持了微前端的优势。

总而言之，我喜欢模块联盟的工作方式，很高兴看到它解决了使用微前端的一些缺点。我相信这是前进的方向，它将改变我们开发 web 应用程序的方式。