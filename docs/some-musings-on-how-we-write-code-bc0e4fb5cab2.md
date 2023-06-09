# 关于我们如何写代码的一些思考

> 原文：<https://levelup.gitconnected.com/some-musings-on-how-we-write-code-bc0e4fb5cab2>

![](img/b60b181babec125b2395a67ff04949f0.png)

罗布·施莱克希斯在 [Unsplash](https://unsplash.com/search/photos/computer-thinking?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

每个代码库都是不同的。同样，每个团队(队列…骄傲？工程师的统称是什么？一个字节？)对什么构成质量有不同的标准。

![](img/888a6e66436ad1d347d1090436f1a9f2.png)

开发商，开发商，开发商！

通常，对一群开发人员来说被认为是异端邪说的代码味道，被他们对面的同行认为是理所当然的“做事的方式”。

我指的不仅仅是分号、制表符、空格或格式之类的东西。这些事情不会改变程序的执行方式(至少在 JavaScript 中！) .我说的是范式(函数式 vs .声明式 vs .命令式)，如何分离关注点，或者甚至使用嵌套的范式是否被认为是不道德的。我认为这些怪癖、偏好和理想受你的环境、同事(pod 成员)和你采用的技术的影响。

让我们来看几个。

## 环境影响

不管你怎么说，你的优先事项将取决于你的公司/团队的规模(当然，还有其他因素)。

以两个同样大小的 dev 聚会为例。一个是中高层管理人员和企业发布周期的官僚作风，另一个是争取在资金耗尽之前尽快发布产品。

![](img/0cf1046cb71461e2880954f3cb848345.png)

这里起作用的核心因素是紧迫性。如果你的日常生活没有受到软件出货速度的影响，那么就没有紧迫性。你也不会尽快把东西拿出去。但是——你*可能*写更多的测试或者更少的未来遗留代码。下面的列表总结了我对团队规模如何影响你编写代码的方式的看法。

**大公司:**

*   你不着急。你的产量会减少。你的工作没有危险，因为在成熟的、盈利的公司里，钱不是问题。
*   您可能必须处理遗留代码。不幸的是，这意味着您可能会编写更多的*遗留代码。您也可能正在处理没有很好记录或不容易使用的技术。或者更糟……颤抖……这可能是定制的。闭源。滚自己的！这将增加你的工作时间。这会让你更慢。*
*   如果某个更资深或更投入的人恰当地完成了他们的工作，你将会看到事情发展的一面。CI/CD 将“正常工作”**【TM】**，您可以轻松启动任意数量的环境/管道。你不必花时间去摆弄基础设施。这将使你更快更有可能写出好的测试。
*   大公司很少有横向的组织结构。这意味着你的团队中可能会有人只在代码满足他们对“好代码”的定义时才合并代码。这可能是好事也可能是坏事。

**相比之下，在小公司:**

*   你必须把事情做完。这可能意味着你正在编写更少的单元测试。在你的代码发布之前，看它的人可能会少一些。在用户使用它之前，你甚至可能没有一轮人工问答。编写不那么脆弱的代码，或者找到一种高效、有效的编写自动化的方法，以“保证”您的代码做包装上所说的事情。
*   您仍然需要处理遗留代码。您可能仍然会编写最终应该丢弃并重写的代码。理想情况下，你要记住，每一段代码都有一个时间线，你应该相应地编写它。
*   为自己相信的标准而战更容易。希望这更像是精英管理。

## 同事/技术选择影响

我很幸运能和一些聪明的程序员一起工作。难以捉摸的 10xs。完全有动力的人类。但是我也和一些开发人员一起工作过，他们写狗屎代码，不关心产品，只想做好他们的朝九晚五，很差，和 gtfo。

它来了。这是一个疯狂、陈腐、令人不寒而栗的论题。

> 没有一个程序员是孤岛。

那里。我说了。现在，外面的麻烦制造者可能会沾沾自喜地笑着问自己，“那我呢？”“我是一个团队的一员/我在永恒的月光下每天 20 小时写代码/我把我的创业公司变成了一只独角兽，没有一个人被雇佣，”你仍然使用开源框架。你仍然会遇到问题。你仍然依赖其他人！

但是更严重的是，你和谁一起工作会强烈地影响你的代码结果。如果你能增加的最大价值是指导、代码审查或“架构”，那可能你甚至不用写代码。

> 生产力是我个人的产出。Generativity 是团队有我和没有我的产出之差。来源:[https://the-composition . com/the-origins-of-opera-and-the-future-of-programming-bcdaf 8 FBE 960](https://the-composition.com/the-origins-of-opera-and-the-future-of-programming-bcdaf8fbe960)

你对团队最大的价值主张可能是成为一个“推动者”，帮助其他人写出伟大的代码。

继续，某些开发人员，就像人类习惯做的那样，有自己的观点。偏好，如果你愿意的话。无论是谁开始构建您正在开发的产品，他都可能热爱 jQuery 并拒绝让它消亡。(不好意思。)

或者他们可能讨厌在他们的 React 项目中看到`style.css`文件，所以你的整个应用程序都是用内联样式构建的。

但是意见的范围更广。甚至程序员对产品其他部分的选择和行为也会强烈影响你如何编写代码。如果您是前端开发人员，您可能需要获取一些数据。您可能认为您可以从后端获得它，但是后端工程师会告诉您如何以及何时可以获得它。(理想情况下，你们可以找到一种方法，很好地合作。)这将影响你如何编写你的“数据层”和你与 API 的交互。

你的队友也会对你的个人能力和成长产生强烈的影响。花一年时间和一个比你更聪明、更有经验的开发人员在一起，他会真正关心你的进步，你会明白我的意思。我保证——你会写出越来越好的代码。

## 回首

最近，我一直在思考，在过去的几年里，我做编程的方式是如何经历了彻底的转变的。写这篇文章让我探索了如何和为什么，而没有太多的技术细节。在以后的文章中，我可能会探索我正在编写的 React 代码中的变化。