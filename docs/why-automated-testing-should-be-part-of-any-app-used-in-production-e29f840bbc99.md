# 为什么自动化测试应该成为生产中使用的任何应用的一部分

> 原文：<https://levelup.gitconnected.com/why-automated-testing-should-be-part-of-any-app-used-in-production-e29f840bbc99>

![](img/a99edc9eef472f3a67b627d2b5bb311a.png)

deanna alys 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

编写软件并交付给用户是很难的。它包括与潜在用户交谈以获得反馈。

然后，我们必须通过计划、设计和实施我们的用户反馈解决方案来对它们采取行动。此外，我们必须确保在这个过程中没有任何东西被破坏。

在本文中，我们将了解为什么自动化测试对于用户在生产环境中使用的任何应用程序都很重要。

# 软件质量的重要性

软件质量很重要。人们会注意到我们在生产过程中损坏了东西。他们会抱怨坏掉的东西。

因此，在将它们部署到生产环境中之前，我们必须尽最大努力确保它们没有损坏。

# 生产软件不同于学生项目

在我们有在工作中开发软件的经验之前，我们只有通过开发学生项目来开发软件的经验。

生产软件不同于学生项目。即使他们可能做相似的事情，生产软件被用户使用，而学生项目不是。

我们不需要检查学生项目中的回归，因为在我们完成它们之后，任何人都不会再看它们。

但是，生产软件就不一样了。它们被很多人使用。所以我们必须确保在投入生产前一切正常。

# 高质量的软件比低质量的更快更便宜

高质量的软件构建起来更快更便宜。bug 让人们付出了代价，因为它们让用户感到沮丧，导致计算错误，以及其他许多让企业付出了处理成本的事情。

如果一切都运行良好，那么我们就不必花费时间和金钱来处理这些事情。

测试、调试和重建都要花钱。低质量的项目有蹩脚的代码，很难理解和改变，所以如果他们可以改变的话，需要更长的时间来改变。

因此，缺陷预防是我们在投入生产之前都应该努力的事情。

更少的缺陷意味着要修复的东西更少，这意味着花在修复东西上的时间更少，因此节省了人力成本。

# 如何防止缺陷

如果我们有自动化测试，防止缺陷是容易的。我们可以通过单独测试应用程序的小部分，用单元测试来自动检查回归。

每个函数、类或模块都可以有自己的测试集。确保我们测试了所有的案例。

然后我们有集成测试来测试应用系统的小部分。我们用这些测试做一些事情，比如操纵文件和数据库。

为了测试更广泛的系统，我们有端到端的测试来测试涉及系统更大部分的所有事情，这几乎是真实用户会做的任何动作。

端到端测试测试整个系统，就像用户必须通过多个应用程序才能完成某件事情一样。

唯一的区别是，我们在每次测试后都清理数据，这样我们就可以像用户那样从头开始。

一旦我们有了一个大的测试套件，那么当我们改变我们的系统时，我们就可以高枕无忧了。

当我们改变系统时，我们只是增加和更新测试，然后我们就万事大吉了。

如果我们没有测试，那么我们每次都必须从零开始手工测试所有东西，这很无聊而且重复。

电脑擅长做无聊和重复的事情，所以我们应该让它们做，而不是自己做。

![](img/34c01b0e173c10a1b90bfcbbf41ccc1d.png)

由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 [hue12 摄影](https://unsplash.com/@hue12_photography?utm_source=medium&utm_medium=referral)拍摄

# 改进开发过程

我们肯定可以通过将这些测试合并到一个持续集成系统中来改进我们的开发过程，该系统在让我们将变更集成到将要投入生产的代码中之前运行这些测试。

那我们就不用自己跑了。

如今大多数框架都包含一些测试框架。所以，我们可以用它来测试我们的东西。

任何测试都比没有好，所以我们应该尽可能将它们添加到我们的代码中。

它会永远帮助我们。

# 结论

在生产环境中使用的任何项目中，自动化测试都不会出错。

这正是我们应该有的安心。我们不想一直自己测试所有的东西，也不想等到用户发现后才修复我们的代码。