# 我从零开始构建 SaaS 产品中学到的 5 个教训

> 原文：<https://levelup.gitconnected.com/5-lessons-i-learned-from-building-a-saas-product-from-scratch-627a101d5381>

## 一个开发者的视角

![](img/376c6b2223d00d7da978dda7bb6dba8a.png)

图片由 [Arian Darvishi](https://unsplash.com/@arianismmm) 提供

几个月前，我在度假时想到了一个 SaaS 产品的创意。一回来，我就列了一张待办事项清单，并开始仔细查看，以实现我的愿景。这篇文章概述了我面临的一些问题和我学到的教训。

## 1.从一开始就想好你的赚钱策略

不用说，开发人员喜欢写代码——作为一名典型的开发人员，我直接跳到了这一点。一两天之内，我就有了一个超级基础的 MVP。但有一个问题，我用来支持我的核心服务的 API 以小数美元跟踪使用成本，我的支付后端使用美分(可以说是更符合人体工程学的处理金钱的方式，更好地避免舍入误差)。

由于这种差异，我无法安全地将我的产品货币化。这个问题由于系统需要能够处理低至几分之一美分的成本问题而变得更加复杂。

就在这时，我从代码中后退了一步。我查阅了各个服务的 API 文档，并意识到有一些有用的端点可以解决我的问题。我最终阅读了该死的手册，并通过一些即时的成本/使用比较解决了我的问题。

如果我以一种更细致、更有条理的方式计划我的攻击过程，我会因为间接性而节省几天的时间。

## 2.总是测试与第三方 API 的集成，即使他们不可能这样做

我想确保我有一个可靠的 CI/CD 管道，向我的客户交付高质量、经过良好测试的代码。我愿意忍受的代码库的最小测试覆盖率是 90%,我不想简单地手工测试第三方 API 集成，并希望最好的结果。

我使用的支付后端鼓励用全面的嘲讽库和沙盒环境进行测试。我的集成测试能够向沙箱发出实时请求，并无缝地断言应用程序行为。

我希望我能对驱动我的核心服务的 API 说同样的话。在我的人工测试中，他们最终以“可疑活动”为由封锁了我的账户(在他们的辩护中，他们确实在给他们发邮件的一天内恢复了我的账户)。我最终创建了一个不同的测试帐户，并在我的集成测试中使用它。这仍然没有达到我的期望，因为我不能对某些应用程序特性进行自动化测试，因为 API 会为此向我收费。将来，我计划创建一个模拟服务器，它将返回预定义的响应，就像它是实际的 API 一样。

## 3.拥有一个无缝且完美的用户入职流程

对于我的应用程序，我必须温和地引导用户通过一个过程，确保他们:同意条款，输入他们的支付细节，并支付注册费。

我的第一反应是像过去一样推出自己的认证逻辑，但我决定通过使用“使用 Google 登录”来拥抱 OAuth 2.0。我相信这个决定从长远来看会更好，因为它使注册/登录过程更快。

但是我不得不经历几次迭代，直到我觉得它对生产使用来说足够清晰和符合人体工程学。

## 4.从一开始就考虑安全性和加密

MVP 很少关心高安全性，但是我决定从一开始就利用加密的数据库字段、仅支持 HTTP 的 cookies、SSL 和经过验证的第三方 API 请求。

我使用隧道服务来设置子域、测试纯 HTTP cookie 和开发中的 HTTPS 请求。我在这背后的想法是，如果这个 SaaS 起飞，它受到审计甚至攻击只是时间问题。从一开始就推出这些功能比以后再添加要容易得多。

## 5.考虑使用平台即服务来托管/开发运营

这可能是特定于我的情况，因为我是这个项目中唯一的开发人员。我想最大化我的生产力，所以我选择了 PaaS 托管。

尽管走这条路要昂贵得多(与 AWS 等 IaaS 相比),但我相信它会让我将开发精力集中在构建应用程序功能上，而不是建立托管基础架构，从而带来回报。这也让我不用担心基础设施的安全，这是一件好事。

就这样，如果你对产品的结果感到好奇，你可以点击[这里](https://www.lenny.mobi)查看

[沙施克](https://www.linkedin.com/in/shashike-jayatunge/)是一名来自多伦多的软件工程师，也是 [Restarone Inc](https://www.restarone.com) 的创始人。当他不开发软件时，他在 Medium 和 YouTube 上创作内容，帮助人们过渡到技术领域。