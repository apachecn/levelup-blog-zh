# 伟大的拉动式请求的 11 个部分

> 原文：<https://levelup.gitconnected.com/11-parts-of-a-great-pull-request-cc513a947dbe>

现在是周四下午，你已经完成了前两天写的特写。您希望在周末之前将这个特性合并到主分支中，但是您知道您必须提交一个 pull 请求并等待代码审查。然后，你必须根据提供的反馈进行协商或做出改变。团队中的高级开发人员和首席架构师在进行代码审查时会非常仔细，所以你知道他们可能会有所发现。你已经有几个月没有进行 LGTM 审查了，所以你知道即使今天审查了代码，你是否能够在周末之前进行修改并得到最终的代码是值得怀疑的。

最重要的是，你真的想得到领导的评价。在你开始工作之前，你已经和她一起检查了设计，所以她已经签署了你是如何建造它的。但是你知道她非常忙于处理会议和项目的其他方面，从管理客户的技术期望到为下一个 sprint 计划工作，她总是很忙，很少有机会自己编写代码。你怀疑她今天或明天早上会有时间审查你的代码。不幸的是，代码审查似乎总是被降低优先级。但是你认为如果我友好地请求她，也许她可以花些时间快速浏览我的代码，所以你给她发了一条关于 slack 的消息。

![](img/c90d03337f1354079874c3309278eef4.png)

弗洛里安·奥利佛在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

她回答说，她会努力，但首先她希望你自己预先审核你的拉动式请求，她正准备向团队发送一些关于如何创建一个出色的拉动式请求的指南，以加快审核过程。

几分钟后，您的收件箱中会收到该主管发来的以下电子邮件。

有了这些新发现的知识，你现在知道如何准备你的公关，以确保它能尽快得到审查

*战队，*

代码审查非常重要。我们都应该审查所有未完成的拉动式请求。我知道它们需要时间，但它们是我们分享知识和保持团队发展一致性的不可或缺的一部分。由于要求高级开发人员签准所有 pr，因此我们已经在每个 sprint 中为他们每个人分配了一些时间。然而，虽然团队中的高级开发人员试图及时进行代码审查，但我们也有自己的开发承诺，所以审查有时并不总是像您希望的那样快。然而，您可以帮助团队中的所有开发人员更快地审查您的拉取请求。我整理了以下列表，您可以通过这些方式准备您的拉动式请求，这样我们可以加快每个人的审核过程。下次提交拉取请求时，请仔细阅读此列表。

*谢谢，
首席高级开发*

*   ***让你的拉取请求与主分支*** 保持同步。检查一下，一天同步几次。至少在早上和下午的某个时候。没有什么比在做评审之前同步一个拉请求更令人讨厌的了，希望不会有冲突。(这导致……)
*   ***化解你们的矛盾。确保你尽快解决你的分支机构与总分支机构之间的任何冲突。如果我看到冲突，我可能会花时间去解决它，或者如果我没有时间，我会把它踢回给你。***
*   ***确保 PR 管道是绿色的。如果你在公关过程中有自动化测试或静态分析，确保它们都通过。这通常意味着在你提交了 PR 后，你需要在几分钟后检查它，以确保所有的灯都是绿色的。我不能告诉你有多少次我遇到了我准备好回顾的 PRs，但是我因为测试或静态分析是红色或黄色而停止。***
*   ***编写伟大的单元测试。无论如何你都应该这样做，但是如果我在一个 PR 中看到单元测试，并且管道通过了所有的单元测试，这是一个好的迹象。这些测试将是我在公关中关注的第一件事。它们看起来正确吗？他们在测试正确的东西吗？正反两种情况都涵盖了吗？顺利通过测试让我对你的代码充满信心。***
*   不要让你的 PRs 原子化。 这违背了传统智慧，但整个过程也是如此。大多数开发人员都被告知一个问题- >一个分支- >一个公关。然而，你需要知道有时候打破这种状态是个好主意。如果我审查 PR，我宁愿审查 1 个中等大小的 PR，而不是 5 或 6 个小 PR，它们都在代码的相同区域中运行。特别是，如果它们触及相同的代码，作为一个评审者，我开始关注这些变更之间的相互作用。我经常把这些踢回给一个或多个开发人员，让他们把变更合并到一个分支中，形成一个合并的 PR。这就不止一次地抓住了否则可能看不到的冲突或问题。*记住开发者没有自己的分支，你可以分享它们。*
*   ***留个赞拉请求评论。*** 介绍一下变化，说说你做了什么，为什么。不要只告诉我门票或门票这是相关的，给我一个链接到他们。在公关评论中包括门票的重要部分。告诉我这个 PR 的重要性和依赖关系。仅仅告诉我它应该在冲刺阶段或周五之前完成是没有帮助的。我知道这个。一切都在星期五到期。如果是 UI 改动，包括一些截图。
*   ***在你的代码中留下很棒的注释。*** 代码中的注释不仅有助于当前的 PR，也有助于所有未来的开发者。当你写代码的时候，所有的代码都是“自文档化”的，因为你已经把它们都记在脑子里了。想象一下，你是一个新的开发人员，一年后看到这段代码，却对它一无所知。总是用注释来解释原因。
*   ***反馈自己的 PR。*** 没有什么能阻止你回顾自己的 PR，留下评论。如果你认为有什么东西我可能会更仔细地看，那么你可以先发制人地评论那一行。如果我看到你对此发表了评论，也许我就不用问你了。这里需要注意的是，如果你觉得有必要这样做，首先问问自己是否应该把注释放在代码中。(参见*在您的代码中留下精彩的注释*。)
*   ***吸取以往的教训。如果我以前检查过你的代码，并对需要修改的地方留下了评论。不要再次提交做同样事情的代码。充其量，我会错过它，我们会有代码不匹配的代码库的其余部分。更糟的是，我会再次标记它并拖延你的公关。此外，现在我将开始更仔细地查看您的代码。***
*   ***不要自作聪明。*** “聪明”的代码写起来很有趣，但审查起来却很麻烦。使用您的语言和代码库通用的结构和约定编写简单明了的代码。不要在你的拉动请求中提交脑筋急转弯。我可能会浪费时间试图弄清楚它是如何工作的，或者我可能只是把它送回给你。即使我真的理解了，我也可能会把它退回给你以简化它。
*   ***做一个伟大的评论者自己。假设整个团队都可以审查代码，那么你就可以根据每个人的拉取请求来帮助完成上述所有工作。如果我投入到一份公关工作中，看到其他人都花了很大力气去审核它(而不仅仅是一堆“LGTM”的评论)，那么我会对这个过程更有信心，我需要花更少的时间去审核它。如果你看到两个 PRs 可以合并成一个，和另一个 dev 谈谈，合并它们。如果您看到其他 PRs 有未解决的冲突或破裂的管道，请修复它们或让最初的开发人员修复它们。如果你看到一个公关缺乏良好的评论，标记它，并与开发人员交谈。如果你看到一个 PR 的代码与之前被拒绝的代码相似，请对其进行评论。***

这最后一点我怎么强调都不为过。这有几个好处。首先，我会开始更信任你的代码，这意味着对你的 PRs 的审查会更少。第二，如果你想要达到这样一种状态，团队作为一个团队而不是一个看门人进行代码评审，那么团队需要证明它能够进行有效的 PR 评审。所有这些都是实现这一目标的必要条件。最后，当把关者能够主要留下“LGTM”评论时，你将有证据表明团队准备好改变流程，因为团队已经发现了所有可能的问题。