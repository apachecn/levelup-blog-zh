# Angular —动态语言(i18n 和 l10n)

> 原文：<https://levelup.gitconnected.com/angular-dynamic-language-i18n-l10n-300d76c31b17>

## 了解如何使用多种语言运行您的应用程序，并带来无国界的可扩展性！

![](img/2c0a43ee924956fcea66c1537bdabc5d.png)

照片由[西德·瓦克斯](https://unsplash.com/@videmusart?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 摘要

*   国际化(i18n)；
*   它是如何工作的？
*   IP API
*   如何实施？
*   奖金
*   参考

# 国际化(i18n)

那么这个巨大的单词是什么呢？什么是国际化？国际化是准备相关软件或系统以支持不同语言和文化的过程，在这一点上几乎没有投入时间和资源。

不经过 i18n 过程的软件发布会带来几个问题，首先是市场接受度。然而，推迟这个问题会导致额外的成本、时间、资源、努力，并且相对于已经实施了它的竞争对手来说会有损失，因此被认为是一种市场优势。

从一开始就实现这个过程会带来一些好处，比如消除了硬编码代码，独立于与代码相关的日期和动态。

最后，值得注意的是，与国际化进程密切相关的另一个概念是本地化进程(L10n)，它与产品的翻译和改编相关，以满足语言、文化和其他要求。一个特定的位置。

因此，考虑到这些概念和过程，本文旨在展示如何使用 Angular 框架为页面/web 系统以实用的方式实现这些概念。

# 它是如何工作的？

这整个想法始于思考如何给我的个人页面(【https://lucasbrito.vercel.app/home】)带来更多的可扩展性，没有什么比让它对更多语言可用更清楚的了，但我仍然面临着为访问它的人带来便利的挑战。因此，为了使语言的选择更加自动化，我想到利用一些服务，这些服务知道访问页面的人的位置，以便它自动适应该位置的语言。

下图总结了对所执行的实施的解释。

![](img/4d01e0916a4e12d1e6da01305e463b38.png)

解释应用程序如何工作的图表。

值得注意的是，起初只使用两种语言。

# IP API

关于前面提到的知道每个请求位置的资源，我选择使用 IP-API，主页面将其中的请求转发给该服务的 API。这个 API 提供了一个端点，它在 JSON 中返回以下数据:

*   地位；
*   消息；
*   国家；
*   国家代码；
*   地区；
*   regionName
*   城市；
*   zip
*   lat
*   lon
*   时区；
*   isp
*   org
*   as；
*   查询。

有关该服务的更多信息，请随时访问以下链接:

[](https://ip-api.com/docs/api:json) [## IP-API.com-地理定位 API 文档 JSON

### API 基本路径是 http://ip-api.com/json/{query} { query }可以是单个 IPv4/IPv6 地址或域名。如果你…

ip-api.com](https://ip-api.com/docs/api:json) 

# 如何实施？

为了实现这个环境，有必要使用一个包来帮助翻译页面，这就是[@ ngx](http://twitter.com/ngx)-translate/core([https://www.npmjs.com/package/@ngx-translate/core](https://www.npmjs.com/package/@ngx-translate/core))，但是值得一提的是，还有其他选项可以执行相同的任务，例如 angular-l10n([https://www.npmjs.com/package/angular-l10n](https://www.npmjs.com/package/angular-l10n))。

因此，要采取的第一个措施是通过以下命令创建项目:

```
ng new angular-tour-of-heroes
```

创建项目后，有必要添加将在开发中使用的包，在这种情况下，我将放置上述包。

```
npm i @ngx-translate/core @ngx-translate/http-loader
```

添加这个包后，需要将它导入到我们的应用程序中，放在`app.module.ts`中，如下例所示:

带翻译服务的模块。

将包添加到项目模块后，需要定义项目中会用到哪些语言，项目中要用到的句子都要写在那里。需要强调的三点是:

*   这些文件必须在`/assets/i18n/`文件夹中。例如，`/assets/i18n/en.json`。
*   要定义的文件格式是 JSON
*   对于所有语言，JSON 键必须是相同的，只需改变值。

下面是这两种语言的示例文件。

带葡萄牙语翻译的文件。

带英文翻译的文件。

有了定义的语言以及翻译的短语，我们将执行用户位置的搜索。对于我们将使用的 API，用户只需要向 JSON 端点发出一个请求，因此我们已经有了前一个会话中提到的所有数据的答案。因此，我们将通过以下命令生成一个连接到 API 的服务:

```
ng g service api
```

创建服务后，我们将执行在 API 中发出请求的函数的构造。下面是提到的服务，函数`getIPInfo()`负责发出请求。

服务来连接提供用户 IP 的 API。

通常，在此步骤中，系统默认语言的定义被执行，然而，由于我们将动态地执行此操作，因此在此步骤中，我们将启动相关页面上的翻译服务，以及捕获与用户 IP 相关的信息的请求。我将在页面`app.component.ts`上执行这样的实现，如下面的代码所示。

这是用翻译资源创建主页的代码。

从第 6 行到第 15 行，可以看到正在构建的组件，以便强调在第 10 行、第 11 行和第 12 行中，我们可以看到 JSON 中文件的关键字，并伴有单词“translate ”,因此关键字在哪里，将是 JSON 中根据语言定义的值。

该文件中的另一个亮点是由`OnInit`生命周期调用的函数`setLanguage()`，因为通过该函数，请求被发送到 IP-API API(第 29 行)，不久之后，我们将英语设置为默认语言(第 32 行)，但是如果用户的国家代码与`BR`相同，这将被更改，将语言更改为葡萄牙语。

如果使用`ng serve`命令执行代码，就有可能观察到代码被转换成访问语言。如果你想执行访问模拟另一个位置，我建议使用 VPN，这就是你的应用程序如何进行 l10n 和 i18n 开始的概念。

# 奖金

当执行代码时，我们可能看不到语言的变化，但是在文件`app.component.ts`(第 12 行)中，我们看到有一个没有动作的按钮，通过点击，可以执行语言的变化。所以让我们来实现这个功能。

这是用翻译资源创建主页的代码。

这里可以观察到，在第 18 行中添加了一个变量来加载当前语言，该变量在`changeLanguage()`函数中被更改，其中，如果语言是葡萄牙语，则当调用该函数时，它会变成英语，反之亦然。-反之亦然。这个函数是通过单击按钮来调用的，这可以在前面脚本的第 12 行中观察到，随着按钮功能的改变(单击)。

最后，值得一提的是，完整的实现可以在下面的存储库中找到。请随意投稿，我希望这份文档能对你的职业生涯有所帮助！

[](https://github.com/Lucs1590/angular-dynamic-language) [## GitHub-lucs 1590/angular-dynamic-language:一个使用第三方软件展示角度平移的项目…

### 这个项目展示了使用第三方 API 来获取用户位置角度转换。这个项目是由 Angular…

github.com](https://github.com/Lucs1590/angular-dynamic-language) 

# 参考

[](https://ip-api.com/) [## IP-API.com—地理定位 API

### 免费的 IP 地理定位 API 查找任何 IP 地址

ip-api.com](https://ip-api.com/) [](https://blog.mozilla.org/l10n/2011/12/14/i18n-vs-l10n-whats-the-diff/) [## i18n 与 l10n —有什么区别？

### 国际化(i18n)。本地化(l10n)。全球化(g11n)。本地化能力(l12y)。这一切意味着什么…

blog.mozilla.org](https://blog.mozilla.org/l10n/2011/12/14/i18n-vs-l10n-whats-the-diff/)  [## i18n 是什么？|什么是国际化？Lingoport

### 国际化(i18n)是准备软件的过程，以便它可以支持本地语言和文化…

lingoport.com](https://lingoport.com/what-is-i18n/) [](https://github.com/ngx-translate/core) [## GitHub—ngx-translate/core:Angular 的国际化(i18n)库

### Angular 的国际化(i18n)库。使用 ngx-translate 的简单示例…

github.com](https://github.com/ngx-translate/core) 

# 分级编码

感谢您成为我们社区的一员！在你离开之前:

*   👏为故事鼓掌，跟着作者走👉
*   📰查看[级编码出版物](https://levelup.gitconnected.com/?utm_source=pub&utm_medium=post)中的更多内容
*   🔔关注我们:[推特](https://twitter.com/gitconnected) | [LinkedIn](https://www.linkedin.com/company/gitconnected) | [时事通讯](https://newsletter.levelup.dev)
*   🚀👉 [**软件工程师的顶级工作**](https://jobs.levelup.dev/jobs?utm_source=pub&utm_medium=post)