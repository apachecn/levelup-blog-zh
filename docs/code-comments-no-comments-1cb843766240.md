# 代码注释？没有评论

> 原文：<https://levelup.gitconnected.com/code-comments-no-comments-1cb843766240>

## 关于评论的很多评论

![](img/eded8711baf5e6ab4a4b44f49ea74c0f.png)

与 pic 无关:向爱德华大喊！

## 序文

说到写代码注释，大家都有注释(包括[本人过去的](https://medium.com/p/133647f2a869)；以后再读！)

评论应该**而不是**成为常态。如果需要的话，尽量少用。我相信添加过多评论的文化是从学校开始的。当我们学习代码时，我们看到代码中散布着注释；profs 在代码提交中征求意见。因此，当我们转向更大的项目，开始编写复杂的逻辑时，这个习惯会一直伴随着我们；我们认为评论是默认的。但事实上，编码文学在**年**一直提倡反对注释(我最喜欢的参考是 2008 年写的！)为什么“评论一切”这个概念会一直存在？我的三个理论:

1.  这个习惯一直延续着
2.  一些在评论盛行的时候还是编码员的人，现在领导着团队，并且更喜欢这种方法
3.  最佳实践会发生变化，但是团队约定仍然存在，因为遵循它更容易

我们可以开始了，不用写下一行评论。

## 为什么不是评论？

烂片的一个标志就是大量的暴露，如果我们能通过观看故事发生来了解故事，不是很好吗？代码也是一样。代码是内容，评论是，只是评论。当我们添加注释时，我们已经放弃了让代码讲述故事。

过多的注释会损害代码质量的三个实际原因:

1.  它们是另一个维护点，随着代码的发展，它们可能会过时
2.  依靠评论来解释故事将延续使用评论来讲述故事的习惯，而不是花费时间来编写代码(还记得那些论述吗？)
3.  强制执行过多的注释约定(例如，Javadoc everything，comment every property)会抑制使用适当的代码结构来避免额外的工作(例如，工程师可能会发现 Javadoc 很麻烦，并在同一个函数中编写所有的逻辑，而不是分解成小的、描述性的函数)

如果不清楚，编写过多注释的替代方法不是简单地丢弃注释，而是编写自我记录、自我解释的代码，这样注释就变得多余了。(继续类比:从一部电影中去掉解说并不能让它变好；改进内容，使阐述变得不必要，使其变得更好)

## 当评论？

那么什么时候加评论呢？以下是一些使用案例:

1.  为面向公众的接口或 API 编写 Javadoc 时
2.  对于复杂的逻辑(例如:性能高度优化的代码)
3.  对于非常规逻辑或陷阱(例如，调用一个应该返回错误状态但实际上总是抛出的方法)
4.  当你的短绒(或“权力”)需要的时候。既然这样，也许给他们看看这篇文章，希望能改过来？
5.  这是你自己的项目(而且是你一个人的)，在这种情况下..规则是你定的！

**后记**

如果你忘记了上面的一切，只要记住这一点:

> 秀，不要说

默认情况下避免注释，只有当你能证明它是正确的时候才添加。这里有一些来自其他文章的片段。

来自 https://blog.codinghorror.com/coding-without-comments/(我最喜欢的参考，来自 2008 年):

> 当你已经重写、重构和重新架构了你的代码十几次，以使你的开发伙伴更容易阅读和理解的时候——当你不可能想象出任何可以想象的方法来改变你的代码，使之变得更简单明了的时候——然后，只有在*之后*，你应该感到有必要添加一个注释来解释你的代码是做什么的。

来自鲍勃叔叔的《干净代码》一书:

> 用代码解释你自己

来自[https://visual studio magazine . com/articles/2013/07/26/why-commenting-code-is-still-bad . aspx](https://visualstudiomagazine.com/articles/2013/07/26/why-commenting-code-is-still-bad.aspx)

> …代码的编写和重写应该尽可能显而易见。留给注释去做的是解释编译器不能访问的东西:为什么代码在那里。

摘自 https://www.martinfowler.com/bliki/CodeAsDocumentation.html(2005 年):

> 如果没有意愿让代码变得清晰，那么它自己变得清晰的可能性就很小。因此，清理代码的第一步是接受代码是文档，然后努力使它变得清晰。

**您可能喜欢的其他文章**

*   [用 Kotlin 写流畅的代码](/write-fluent-code-in-kotlin-133647f2a869)
*   [房间报道:网络服务](https://medium.com/dont-code-me-on-that/tryhackme-network-services-room-writeup-e00f88b7b599)
*   [CTF 日志:机器人先生](https://medium.com/dont-code-me-on-that/tryhackme-mr-robot-ctf-log-c64fc17069c1)