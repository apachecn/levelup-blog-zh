# 粗略代码草案的案例

> 原文：<https://levelup.gitconnected.com/a-case-for-rough-draft-code-3094fc281e92>

为什么你的项目初稿会有点乱

![](img/24c9a633f70539868b5cbd5eb2953f67.png)

格伦·卡斯滕斯-彼得斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## 干净的代码

我在我的其他文章中提到过，我最近开始了一个软件开发人员学徒期。作为实习的一部分，我们在编写项目代码和学习新语言的同时阅读了几本书。

当我认为自己对一个主题有了大致的了解时，我经常会感到谦卑，但是经过进一步的探索，我意识到我仅仅触及了所有知识的表面。这是我在阅读**清洁代码:敏捷软件工艺手册**时发现自己激动人心的地方。

今天我想写的是“粗略的代码草案”我在这里分享的大部分内容都是从这本书中学到的。

## 至善论

作为一个天生的完美主义者，我曾经认为我第一次编码一个项目时，我必须把它做好。甚至在写一行代码之前，我就对所有等待我的工作感到害怕。我认为无论我写了什么，我基本上是永久地写它——无论我马上想到什么，它都会保持原样。就好像我看不到树，因为我被森林的想法淹没了。由于这种心态，我会经常受阻。我没有简单地从小处着手，让代码进化，而是努力构建完美的实现。

我从这本书(和我的学徒生涯)中学到的是一种不同的策略。我们可以使用 TDD(测试驱动开发)来驱动我们的项目，并从小的、“不完美的”代码开始。TDD 允许我们成功地进行这种实践，因为您可以简单地分离出您当前试图完成的事情。当然，这通常会随着项目的进展而改变。这种编写代码的方式非常适合 TDD——测试覆盖了所有“杂乱”的、粗糙的代码草稿。

您的代码在第一次迭代中永远不会完美。很可能需要几次重构、走查和评审，才能将项目进行到您想要的地方。如果你有测试，你不必害怕修改你的代码！

现在，当我编码时，我的目标是编写最小的失败测试——使其通过，然后根据需要进行重构(红色、绿色、重构)。有点像形，随着我的进展，这个项目开始向我展示自己。这种编码方式在短期内需要更多的努力和思考，因为你开始养成良好的习惯，但随着时间的推移，它将成为第二天性。

## 像写故事一样写代码

你的代码最好读起来像一个故事。你的函数应该被恰当地命名——表明它们正在执行的单个动作。你的变量应该清晰，明确，有意图。你的函数或方法就是你的动词。你的类和变量就是你的名词。

> "编程大师认为系统是要讲的故事，而不是要写的程序."

你不会期望在第一次尝试的时候就把笔放到纸上(或者手指放到键盘上)写出一部杰作。(除非你可能是下一个莎士比亚，但我猜即使是他也写了草稿)。

> “当你写一篇论文或一篇文章时，你首先把你的想法写下来，然后你按摩它，直到它读起来很好。第一稿可能很笨拙，也没有条理，所以你要对它进行文字加工、重组和提炼，直到它达到你想要的阅读效果。”⁴

如果我们像想讲故事或写博客一样想写我们的代码，这种心态给了我们一点自由。在最终发表一篇文章之前，我会写几份草稿。我会经历几次迭代才会开心。那么为什么我们的代码应该有所不同呢？

## 粗略代码草案

我们可以像写一篇文章一样来编写我们的项目。Bob 叔叔告诉我们，从长函数、糟糕的变量名或一个大类开始是完全可以接受的。然后，随着时间的推移和重构，你会看到你的代码以一种适合被精炼的方式。它会向你展现自己。

> "编程的艺术是，并且一直是，语言设计的艺术."⁵

我可以自由地一次编写项目的一小部分，由测试覆盖，重构的安全网遍布每一个角落，而不是在代码中缩手缩脚。有了这种新的自由，我可以创建一个命名不当的变量，一个丑陋的嵌套方法，或者一个大类。然后，随着我一个接一个地进行重构，我可以开始提取、拆分功能、更改名称和消除重复。随着时间的推移，最终的分解结构往往会变得更加明显。

创造任何东西的最终产品都需要努力和专注。所以，我再一次问(我自己，或者任何一个与这个潜在的障碍作斗争的人)，为什么编码应该有所不同？

## 前进并编码

有了这种新的心态，注意你是否以不同的方式对待你的项目。用肯特·贝克的话说，“让它工作，让它正确，让它快。”换句话说，**首先，**我们让它工作，**然后**我们让它正确。编码快乐！

[1]干净的代码:由 Robert c . Martin(“Bob 叔叔”)编写的敏捷软件工艺手册

[2]干净代码通道。9

[3]，[4]，[5]干净代码通道。3