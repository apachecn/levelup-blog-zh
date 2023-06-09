# 我们兜了一圈。Java 现在又酷了。

> 原文：<https://levelup.gitconnected.com/weve-come-full-circle-java-is-now-cool-again-3996da973c48>

![](img/40df680febed71777c7531e80df321e8.png)

这张照片曾经让全世界的开发者兴奋不已。现在，他们在呻吟，因为他们不知道自己在做什么。

如果你对编程有热情，你可能经历过这样一个阶段:每一个闪亮的新玩具都是做事情的新方式。如果你没有使用<在这里插入 JS 框架>你就是守旧派——你应该给年轻人让路。你在阻碍进化，老家伙。

当然，我知道这是一个谬论:但是附和“不要被每个新的框架所吸引，旧的框架仍然有效”是一回事对你的同龄人来说，其实另一件事是*对*的感受。那么什么时候，我，一个年轻时还是工程师的我，终于不再沉迷于每一个新的框架了呢？我给你讲个故事吧。一个微服务，通宵，回归安全的故事。

## 使用<framework>否则你就是瘸子</framework>

众所周知，有时我写文章是为了赚钱——我认为这是一笔公平的交易:你可以阅读我无用的观点，要么觉得你同意我的观点，要么对我如此愚蠢感到愤怒。我受雇在你的大脑中释放化学物质——我想我们都从这笔交易中受益。

我所做的部分工作包括研究新的框架和技术。人们，尤其是新程序员，不喜欢费力地阅读文档并提出自己的观点——他们怎么能这样做呢？每天都有新技术问世。没有人总结是不可能跟上的。

我把燃料放在油箱里的秘密是，我实际上对所有这些东西都超级兴奋；从 Flutter 到 Cloudflare Workers，再到 Pulumi 和 ha sura……我想强调这不是浪费时间:我学到了很多很酷的方法来做事情，如果我没有花时间研究新的范例和框架，我甚至不会考虑这些事情。

我构建的每个新项目都有相同的味道:闪亮的新组件——新的 NoSQL 后端，新的查询语言，新的测试框架。我是为了学习而建造，而不是为了建造而建造。我的 github 是一片半成品项目的荒地，每个项目都使用了全新的技术堆栈。刚好够我形成自己喜不喜欢的看法。

你可以在你的空闲时间这样做:也许有人会说我疯了，从学校/工作回家，在一个`docker-compose.yaml`里摆弄模板。但我觉得这很酷也很有趣。很酷。很有趣。

有成效吗？

绝对不行。我完成了我开始的大约 10%的项目——学习闪亮的新框架很有趣，但是在某些时候，有人必须做不那么有趣的部分:编写单元测试，设置 CI/CD，实际部署……我学习了许多范例，但是什么也没有构建。

## 举着一面镜子

被安排在一个全新的项目中非常有趣:你可以置身于我空闲时的情况。所有我们可以选择的新技术；罗马的景象充满了我们明亮的绿色眼睛。该项目是一个半基本的 CRUD 应用程序，供一所大学的一个系使用。

后端团队目光敏锐，选择了基于 Scala 的框架。我负责前端——幸运的是，我没有上钩，选择了我以前有经验的东西。React.js with Typescript(当然，如果我说我尝试了一个新的测试框架和 CI/CD 管道，那就太不负责任了！)

框架选择？检查。截止日期？6 个月，兼职。很简单。

Scala 以其快速的启动时间和对初学者的友好性而闻名，结合了一个没有成熟模式或初学者友好教程的新框架，证明对我们的后端团队是一个福音——已经是初级程序员了，开始进入生产级项目。

可以说后端失败了。离截止日期还有一个月，后端已经着火了；团队的速度接近于 0，对于这些糟糕的初学者来说，这种功能性的范例太多了。

这个特殊的例子比我们许多人所能理解的要极端得多。在一个并不适合的领域选择如此难懂的语言，看起来几乎是蓄意破坏者。但是请保持你的判断力:这只是我们可能都做过的事情的一个极端例子。是的，也许我应该给予更多的指导——但我对失败者的故事很感兴趣，并且只在热情的背后开了绿灯。

这一经历虽然令人沮丧，但让我看到了自己的错误以及陷阱是多么常见。编写和部署服务是很难的，而添加新的、困难的语言就更难了。我什么都没做不是因为时间不够，而是因为每次我找到一个新的框架，我都会被踢回一个档次，不得不重新学习同样的切面包的方法。

## 跳起来救援

我决定的一个框架是一个老人游戏？跳羚队。我第一次实习是在 springboot 工作；这不是一个遗留项目，但它确实感觉像一个。一大块——标准的 Java 东西，比如 Flyway、Hibernate、Spring Security 等等。事后诸葛亮？它感觉老了，因为它是*一贯的。它做了我们要求它做的事情——虽然有点慢，但还是完成了。*

这个项目需要一些良好的一致性。这种一致性就像在 Youtube 上搜索这个框架的名字并获得 20000 次点击一样。复制和粘贴 Github 动作 CI/CD 管道提供的一致性。这种一致性使得所有的测试看起来完全一样，因为这个过程是如此的严谨，以至于所有的测试都被压缩到了最低限度。

我面对的是一堆热气腾腾的垃圾(这看起来很残酷，但却是现实)，大量代码几乎什么都不做。测试是分散的，即使有也是写得很差的。是的，本来是可以修复的。但是如果只是…从头开始重写，那将会事倍功半。

所以我重新使用了旧的 Spring Initalizr 并开始了黑客攻击。

我们及时完成了项目，客户(大学化学系)很高兴——他们并没有欣喜若狂(这只是化学实验室的一些糟糕的注册表格)，但它完成了工作。

我的同龄人对不得不回到无聊的老春天感到高兴吗？一点也不。他们抱怨说他们所有的努力都没了；他们帮助开发后端，编写 REST 端点，就像这是他们的中间名一样，但这并不*令人兴奋。*代码非常容易学习——它完全按照罐头上说的去做，没有魔法隐藏在这里(也许`@autowired`除外)。

另一个开发人员对后端团队说了什么？[“说得好，”坎迪德回答，“但是我们必须耕种我们的花园。”](https://www.goodreads.com/quotes/9807663-as-candide-went-back-to-his-farm-he-reflected-deeply)

现在是 2022 年。给我任何项目。我要评价的第一件事是什么？

Java 适合吗？我们能部署一个好的旧的 JVM 应用程序吗？我们能把完美的整体范式应用到这个问题上吗？

我仍然不喜欢 Java 本身的某些地方——尽管安全性为零。但是任何可以运行`jar`的地方都可以运行应用程序，所以我很高兴。(有时，部署二进制文件更有意义——类似于 CLI，我可能会对一键二进制文件使用 Rust。)

# 分级编码

感谢您成为我们社区的一员！在你离开之前:

*   👏为故事鼓掌，跟着作者走👉
*   📰查看[升级编码出版物](https://levelup.gitconnected.com/?utm_source=pub&utm_medium=post)中的更多内容
*   🔔关注我们:[Twitter](https://twitter.com/gitconnected)|[LinkedIn](https://www.linkedin.com/company/gitconnected)|[时事通讯](https://newsletter.levelup.dev)

🚀👉 [**加入升级人才集体，找到一份神奇的工作**](https://jobs.levelup.dev/talent/welcome?referral=true)