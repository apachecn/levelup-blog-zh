# 我如何让我的垃圾 Python 代码快了 20 倍

> 原文：<https://levelup.gitconnected.com/how-i-made-my-shitty-python-code-20-times-faster-c768308c6cc0>

## 不，这可能不是你应该遵循的建议。

![](img/d81c0a00691b7248031deb0bc4d6f116.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上[泰沛](https://unsplash.com/@agforl24?utm_source=medium&utm_medium=referral)拍摄的照片

我想我们今天可以做一些有趣的事情:谈论我认为每个程序员都有的“那个程序”。这是出于好奇，当第一个小测试成功时，我最终采取了额外的步骤，找到了解决最奇怪问题的最古怪的方法。

我的这个脚本版本是一个 Python 程序，它自动化了一系列微博、Twitter 和 Instagram 账户——结果它出奇地复杂，而且就我通常在日常工作甚至个人项目中应用的干净代码或适当的编码规则而言，令人惊讶地可怕。

这一切都令人惊讶地工作得很好，它工作的事实本身就令人惊讶——考虑到它是文本文件、selenium 脚本的大杂烩，我意识到与其搞清楚 API 访问，我还不如通过自动化 chrome 来自动化登录和发布。这是一个可爱的烂摊子，我最喜欢的项目，我曾经建立了自己的条款。

现在的速度比过去快了 20 倍，这也是今天这篇文章的主题。

# 让它慢下来会让它快很多

我的剧本的第一个版本不断地在某一步或另一步出现问题，而且经常不是我的错。这些网站的加载速度非常慢，当我的脚本试图点击它们或输入文本时，重要的元素还没有加载——这是使用任何类型的网站自动化时常见的问题。

由于我*实在懒得*去弄清楚 Selenium 的“检查元素是否被加载”是如何工作的，我只是在正确错误的地方添加了 time.sleep(3)。

突然间，我的成功率从 30%上升到 80%，这让我很快忘记了我的解决方案实际上有多糟糕。是的，每个任务的执行持续时间大概是 20 秒，但是谁会在乎整个过程在后台运行呢？

# 允许它优雅地失败可以省去我实际编码这么多代码的痛苦

接下来，我面临着我的自动装置的随机问题，有时相同的东西工作，而其他时候不工作。由于我操作了一长串精选的链接，并点击了重新博客按钮，我意识到我真的不关心为什么这些东西有时会失败——下次我们尝试时可能会成功。

因此，我将整个事情放入一个 try-catch 中，当控制台中的错误代码开始让我烦恼时，我删除了 print 语句。现在，整个脚本运行没有明显的问题(lol)，我永远不必调试我无法控制的东西。

# 重新运行错误的链接让我避免了很多额外的代码

我的脚本在启动时做的第一件事是将一个整数加 1，然后在执行结束后调用自己，只要这个整数小于 2。

这导致了两次连续的执行，这“修复了”第一次运行的所有错误，或者差不多。

一旦第二次迭代完成，脚本继续从博客中提取所有统计数据，并给我一个所有关注者计数和队列编号的列表。我还会收到一个简短的报告，关于那些队列中帖子太少的博客。

这最后一步确保我对我的博客状态有一个非常坚实的概述，并且可以看到一些事情看起来是否真的不对劲——这在一段时间内还没有。

# 同时运行同样的东西会让慢代码变快

有一天，我意识到我的博客太多，时间太少，单线程执行开始受到限制。

因此，很自然地，我做了想到的第一件事:编写一个外部 PowerShell 脚本，用单独的参数调用我的脚本八次。我真的不喜欢在适当的多核上浪费时间，尤其是在 Python 中这总是让我困惑。

实际上，我最终正确地完成了这一部分，因为我意识到以这种方式调试任何问题都是一件痛苦的事情，现在它有了正确的多线程。突然间，20 秒的执行时间不再是问题，因为它已经执行了 8 次。

然后，我为我的 3D 渲染机器买了一个新的 CPU，现在我的脚本在十六核上运行，我甚至没有足够的博客。这个脚本每月运行 20 分钟左右，实际上我不得不设置每月提醒，这样我就不会忘记运行它。我*真的不想*弄清楚如何设置一个运行 Python 脚本的预定 Windows 任务。

再一次，我最终在某个时候做得很好，但是我花了令人尴尬的时间鼓起勇气去谷歌一下，并且花了五分钟的实际工作。

# 外卖:有时候，我们都需要脱离专业。

我不能夸大我从这个脚本中得到的乐趣，它几乎做错了所有的事情。我绝不会在工作项目中这样工作，甚至是私人项目——除非是你自己写的，否则你不会想要维护它。

如果有人强迫我处理这团意大利面，我会在他们头上掀翻桌子——但因为这是我自己要处理的，我觉得很好吃。

里面有一些很棒的技巧，我最喜欢的是它写图片标题然后添加链接的方式。它通过键入文本，然后以编程方式按下 Shift-left-arrow 足够的次数来标记单词，然后按下 Control-K，然后添加一些帖子的网站链接。可能有更好的方法，但是我在改变 HTML 标签时遇到了问题，这样做效果更好。

纯粹的，未经过滤的乐趣。

[](https://keypressingmonkey.medium.com/membership) [## 通过我的推荐链接加入媒体-按键按键

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

keypressingmonkey.medium.com](https://keypressingmonkey.medium.com/membership)