# 为什么 Leetcode 不能解决你的数据工程问题

> 原文：<https://levelup.gitconnected.com/why-leetcode-will-not-solve-your-data-engineering-problem-c52ac7c3ba6e>

接受数据工程和软件工程之间的差异，以便更好地面试数据工程师

![](img/c7a7af4c52a4531cf890fe089298ee8e.png)

照片由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 [Sunder Muthukumaran](https://unsplash.com/@sunder_2k25?utm_source=medium&utm_medium=referral) 拍摄

软件工程师通常会接受 leetcode、hackerrank 等编码系统的面试。软件工程师的典型定义是“设计和创建计算机系统和应用程序来解决现实世界的问题”，他们的一些主要任务包括编写和测试代码，优化软件的速度和可伸缩性。

另一方面，数据工程师的主要目标是“建立系统，收集、管理原始数据，并将其转换成可供数据科学家和业务分析师解读的有用信息。他们的最终目标是使数据可访问，以便组织可以使用它来评估和优化他们的绩效。”更具体地说，数据工程师并不专门致力于创建可优化的代码。是的，有时他们确实需要了解是否有更优化的解决方案，但这通常是与软件工程师一起进行的。因此，数据工程师倾向于关注已经创建的应用程序。

那么，为什么数据工程师的测试方式与软件工程师相似呢？应该怎么考数据工程师？这就是我今天想在文章中回答的问题。

我们将创建的数据量只会继续增加。据《福布斯》的吉尔出版社称，从 2010 年到 2020 年，我们已经将数据量从 1.2 万亿千兆字节增加到 59 万亿千兆字节，增幅约为 5000%。这些数据只会越来越大，因此了解如何管理这些数据对企业来说至关重要，因此我们需要塑造并教会人们如何从这些数据中创造洞察力。

其中一个很棒的工具是 Apache Spark。这是软件工程师和数据工程师之间差异的一个很好的例子。为了找出如何分析如此庞大的数据集，软件工程师设计、开发并提出了现在称为“Apache Spark”的平台，并不断扩展其功能。与此同时，数据工程师正在使用，有时滥用(或者在这种情况下，也许挑战是合适的词)创造系统。

你现在可能在想，“那么，莎拉，为什么这些差异很重要？”“我为什么要在乎？”这些都是很好的问题。许多软件工程师不喜欢创建数据管道，也不喜欢弄清楚为什么或哪里有数据质量问题。反之亦然。很多数据工程师不喜欢创建平台，也不喜欢把代码优化成碎片。他们想知道自己的数据处于何种状态，以及如何可靠、一致地将其置于干净的状态。那么为什么数据工程师和软件工程师的工作不一样，我们对他们的面试期望却是一样的呢？

问类似 leetcode 的问题也是一把双刃剑。第一方面是你将设定对面试的期望，因此也是对工作的期望。作为一名候选人，我看到了他们问的问题类型与我在工作中会遇到的问题类型之间的相关性。问我一堆像 Leetcode 这样的算法问题，我会认为这项工作需要大量的算法分析。作为一名数据工程师，我一点也不觉得这有什么吸引力。如果我真的喜欢算法分析，当我意识到这份工作实际上不需要任何算法分析时，我会感到惊讶。

应该怎么考一个数据工程师？不幸的是，我不能告诉你具体怎么做。但这里是我的建议。

首先，确定你想要的是数据工程师还是软件工程师。一种方法是列出他们需要做的事情。他们将使用什么平台(如果有)？什么语言？等等。现在，将这些与软件工程或数据工程联系起来。

如果你意识到你实际上需要一个软件工程师，你可以跳过这篇文章的其余部分，因为它只与数据工程师面试有关。

我可以告诉你，数据工程师至少应该熟悉这些技能:

1.  计算机编程语言
2.  结构化查询语言
3.  数据仓库或湖的想法
4.  NoSQL 与 SQL 数据库
5.  ETL 与 ELT

我会掩护 1 号。第二。我会用一些实际的(想一些你在日常生活中会发现的)问题。例如，如果你需要一个网页抓取器，问他们关于如何通过 URL 分页的问题。

对于后三个问题，我会使用系统设计类型的问题，例如，如果您正在构建一个像[insert awesome system]这样的系统，您会使用数据仓库还是湖？如果您有 10gb/小时和 1000 GB/小时的数据，您会改变主意吗？

希望这些面试建议能对你接下来的求职有所帮助。数据工程师与软件工程师完全不同，应该有不同的标准和期望。

感谢您的阅读！

```
**Resources**1\. [https://www.coursera.org/articles/software-engineer](https://www.coursera.org/articles/software-engineer)
2.[https://www.coursera.org/articles/what-does-a-data-engineer-do-and-how-do-i-become-one](https://www.coursera.org/articles/what-does-a-data-engineer-do-and-how-do-i-become-one)
3\. [https://www.forbes.com/sites/gilpress/2021/12/30/54-predictions-about-the-state-of-data-in-2021/?sh=2b94800d397d](https://www.forbes.com/sites/gilpress/2021/12/30/54-predictions-about-the-state-of-data-in-2021/?sh=2b94800d397d)
```