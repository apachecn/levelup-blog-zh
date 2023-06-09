# 代码审查:请删除代码中的注释

> 原文：<https://levelup.gitconnected.com/code-review-please-remove-comments-from-your-code-2c4de8cf9b13>

我要求在代码审查期间删除大部分注释的原因是

![](img/ee2e428d28b637c6eacfdcf46b551b69.png)

[绝对视觉](https://unsplash.com/@freegraphictoday?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/information?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

当我还是一名大学学生时，我从许多人那里学到，我应该在我的代码中添加大量的注释，以确保其他人能够理解它。在我参加的一个外包公司的入职课程中，指南告诉我，评论平均要占三分之一行。在我职业生涯的最初几年，我遵循了这个指导方针，但是后来我发现这不是正确的选择。现在，我通常要求其他人在代码评审中删除他们的大部分评论。这篇文章将谈谈我这样做的原因。

# 评论是谎言

这一事实可能会让人们感到惊讶，但在很多情况下，这些评论是谎言。为了解释这一点，让我们从下面的一个小例子开始。该函数倾向于将多个文件下载到浏览器的内存中，压缩它们，并将输出保存到本地驱动器。当开发人员完成工作时，一切看起来都很完美。他解释了其他人可能需要的标题和函数中每一步的内容。风格也是我职业生涯早期曾经比较喜欢的。

几个月后，团队决定改变。他们想要十个文件，而不是同时下载五个文件。另一个开发者接了这个任务。他把 5 改成了 10，并更新了行内注释。但是他没有注意到他也需要更新标题评论。后来，另一个开发人员将默认文件名从`combined-<DateTime>.zip`改为`compressed-<DateTime>.zip`。而且这家伙还忽略了头部评论。在代码审查期间，因为比较工具只显示变更，所以其他开发人员也跳过了 head 注释。

这些评论的目的很好，在开始时非常有帮助。但由于合作历史，现在变成了骗子。有些人可能会认为这是其他不负责的人的问题，而不是评论本身的问题。但我们都是人。没有人能保证不犯同样的错误。虽然测试可以帮助我们避免破坏现有的特性，但是没有一个等价的系统可以对评论做同样的事情。

# 注释打消了我们编写描述性代码的积极性

回到上面的例子。虽然注释可以很好地描述代码，但它们也阻碍了开发人员以更具描述性的方式思考和编写代码。如果开发人员强迫自己删除所有注释，但仍然确保可读性，他可能会有一个更好的版本。下面的例子演示了他如何增强了`downloadAndZipFiles`函数的原始代码。

他没有对每一步进行评论，而是应用了来自 clean codes 的指导方针:

1.  使用小函数。每个功能都有一个单一的责任。
2.  对所有函数和变量使用描述性名称。

这些都是很小的改变，但是可以使他的代码更加清晰明了。我可以非常肯定，其他人可以理解这个代码，没有任何评论，在第一个样本。

# 测试是解释特性的更安全的方法

大多数情况下，我们可以使用单元测试来描述一个功能的功能。如果您仍然看到一些隐藏的逻辑，很可能您应该添加更多的测试。严格使用测试也有助于代码审查。如果一个开发人员在实现上做了改变，但是没有在测试上引入相应的更新，他更有可能需要回顾和增加更多的工作。下面是一个比较注释和单元测试的简单例子。

# 可以安全地删除注释代码

许多人习惯于注释掉代码，而不是完全删除它们。这个习惯是有历史原因的。在过去版本控制工具不够强大的时候，跟踪一个模块的变化有点困难。我记得当我还是学生的时候，一些高年级的家伙建议我这样做。“不要删除任何代码。用你的名字和明显的理由把它们注释掉。如今，当我们只需点击几下鼠标就能追踪变化时，这种指导方针已经过时了。我看到那些注释代码像乱码。我们不应该让他们犯任何错误。

# 一些例外

我们仍然应该保留一些特殊的注释。我强烈建议保留评论，甚至在那些罕见的案例上添加更多的细节。

## “为什么”注释

解释为什么代码存在或以那种方式设计的注释通常是有价值的。缺乏上下文通常会导致开发人员困惑、质疑，甚至责备过去的作品。这种类型的评论的一些候选是:

*   开发人员认为团队的决定对其他人来说可能会很奇怪
*   代码库或框架的限制
*   一个已知错误的商定解决方法
*   …

## 异常“难读”

当代码包含正则表达式或复杂算法时，我们应该添加注释。这些部分通常很难阅读，但通常会从评论中受益匪浅。

这篇文章是我关于代码评审的系列文章的一部分，它讲述了我在评审代码时的笔记。对某些人来说，它们中的每一个都可能很小或者没什么特别的。但是因为一个小小的错误会让开发人员付出很大的代价，所以其他人留意所有的可能性可能会有所帮助。

可能有人需要，上面的示例片段来自我的一篇文章:[下载文件，并使用 Javascript](/download-files-and-zip-them-in-your-browsers-using-javascript-cc2143262ea9) 在浏览器中压缩它们。

*最初发布于*[*https://huynvk . dev*](https://huynvk.dev/blog/code-review-please-remove-comments-from-your-code)*。*

# 分级编码

感谢您成为我们社区的一员！[订阅我们的 YouTube 频道](https://www.youtube.com/channel/UC3v9kBR_ab4UHXXdknz8Fbg?sub_confirmation=1)或者加入 [**Skilled.dev 编码面试课程**](https://skilled.dev/) 。

[](https://skilled.dev) [## 编写面试问题+获得开发工作

### 掌握编码面试的过程

技术开发](https://skilled.dev)