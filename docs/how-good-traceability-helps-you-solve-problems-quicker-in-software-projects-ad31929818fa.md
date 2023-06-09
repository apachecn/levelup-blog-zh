# 良好的可追溯性如何帮助你更快地解决软件项目中的问题

> 原文：<https://levelup.gitconnected.com/how-good-traceability-helps-you-solve-problems-quicker-in-software-projects-ad31929818fa>

## 用你的工具！

## 这是一个真实的例子，展示了我如何通过使用不同的工具快速解决一个错误报告，以及它们如何帮助你。

![](img/fdbc79e8910044179a8c2836799d658f.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Carlos Muza](https://unsplash.com/@kmuza?utm_source=medium&utm_medium=referral) 拍摄的照片

## 介绍

我们的开发团队为一个管理公司大部分流程的软件大客户工作。该软件最初创建于 2015 年左右，现已发展成为员工记录其内部流程的最重要工具。这些年来，有许多开发人员、产品负责人和项目经理。没有人知道所有的事情，很多人知道很多，加上一些书面文档，我们可以很好地处理系统的增强和改进。在过去的两年中，软件开发过程和软件本身的质量都得到了极大的提高。我们引入了 Scrum 过程，增加了管理工作任务和会议的工具，并改变了一些开发规则，以获得更多的洞察力和实现指标。我将在接下来的段落中谈到细节。

## 错误报告

有一天，我们在早上收到一个**的 bug 报告**被标记为*阻塞*，意思是工人无法完成工作，因为软件不允许。为了管理我们的工作任务，我们使用一个支持我们的 Scrum 过程的系统，这个 bug 是由那个系统中的一个工人创建的。因此，我们立即通过电子邮件得到了**的通知，并可以很快对此进行调查。然而，当错误消息出现时，报告仅包含应用程序的标题和屏幕截图。**

💡**提示**

✅意味深长的标题
✅重现错误的步骤
✅预期的系统行为
✅实际的系统行为
✅截图甚至一段视频
✅版本信息(软件、数据库、操作系统等。)

许多系统允许在创建项目时定义模板。这可以大大提高报告质量，因为有些人不知道什么信息与解决问题相关。

## 查找代码行

虽然我只有截图，没有重现错误的实际步骤，但我有足够的信息开始调查。图像显示了用户已经打开的页面，所以我有这些信息。然后有两个选择条目的表，这给了我更多的提示。最后，该消息是关于保存过程中的一个错误，因此用户必须单击该页面上的 save 按钮。所以我开始在代码库中寻找错误信息。连同页面和操作的信息(用户保存了他的更改)，我找到了代码行，它引发了一个异常，并显示了上面提到的错误消息。我使用了我的 **IDE** 的许多特性，比如全文搜索，在方法的定义和实现之间跳转，以及调试器，它允许一步一步地检查你的代码。

💡**提示**

✅学习使用调试器(这是一个强大的工具)
✅学习 IDE 的快捷方式(打字比点击快)
✅检查 IDE 扩展以获得更多有用的功能

## 寻找相应的用户故事

在我找到那条线之后，我可以立即判断出问题出在哪里。但我对代码的上下文一无所知。所以我检查了我们的**版本控制系统**中对这行代码的最后一次修改。结果包含开发人员的名字和变更提交的唯一 ID。通过提交 ID，我设法找到了相应的**拉请求**。拉请求中链接的是**用户故事**。这个用户故事告诉了我很多关于上下文的信息，但是我不能自己决定它是否真的是一个 bug。

💡**提示**

✅结合或链接不同的工具
✅写出好的用户故事([例子](https://stormotion.io/blog/how-to-write-a-good-user-story-with-examples-templates/))

## Bug 还是特性？

在与我的同事交谈并阅读了找到的用户故事后，有可能这个 bug 实际上并不是一个 bug，而是之前开发的功能的副作用。有了这些信息，产品所有者、利益相关者和工人找到了纠正过程的方法。
总的来说，我花了大约两个小时收集相关信息。澄清之后，实施并测试了一个修补程序。当天下午经过新的部署，生产问题得到了解决。我不想猜测，如果没有我们良好的工具支持，要花多长时间。

💡**提示**

✅在有疑问的时候总是问别人

## 用过的工具

下面是我用来澄清错误报告的所有工具的列表。我不会提到任何公司，因为有很多好的产品，每个人都必须自己决定应该使用什么工具。

*   带通知的工作项跟踪工具
*   具有拉请求策略的版本控制
*   持续集成/持续部署(CI/CD)
*   具有搜索、导航和调试功能的 IDE

## 结论

工具在几乎每个软件项目中都很重要。正如你在这个例子中看到的，它们可以帮助你很快地澄清问题。所以我给你们所有人的建议是使用工具。有许多关于如何将工具集成到开发过程中的例子，根据经验，我可以告诉你这是值得努力的。

如果你喜欢这篇文章，我会很高兴得到掌声👏(你知道可以拍几次吗？😎)另外，如果你还没有跟上我，我也很感激。

🌲 [linktr.ee](https://linktr.ee/xeladu) |☕ [咖啡](https://www.buymeacoffee.com/xeladu) |🎁[捐赠](https://www.paypal.com/donate/?hosted_button_id=JPWK39GGPAAFQ) |💻GitHub |🔔[订阅](https://xeladu.medium.com/subscribe)

顺便说一句:如果你还没有 Medium 会员，我推荐你使用[│我的推荐链接◀](https://medium.com/@xeladu/membership) ，因为它会让你访问 Medium 上的所有内容，并以一小部分费用支持我，而不会为你带来任何额外费用。谢谢大家！✨

## **相关故事**

这是另一篇文章，你可能会感兴趣。

[](https://xeladu.medium.com/some-important-things-i-learnt-in-my-first-years-as-a-software-developer-638918f60b2c) [## 作为软件开发人员的头几年，我学到了一些重要的东西

### 以下是我作为软件开发人员第一年学到的一些东西。这是关于文档，写作…

xeladu.medium.com](https://xeladu.medium.com/some-important-things-i-learnt-in-my-first-years-as-a-software-developer-638918f60b2c)