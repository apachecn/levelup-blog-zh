# 30 个软件工程最佳实践和改变你思维模式的技巧

> 原文：<https://levelup.gitconnected.com/30-software-development-best-practices-and-tips-to-change-your-mindset-fbf34725a685>

## 19.…尽可能晚地向您的客户或经理提供评估。

![](img/300b18c180579a2b830c286fce5668b1.png)

本·怀特在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

从有经验的开发人员那里学习软件工程最佳实践和阅读技巧可以帮助你把工作做得更好，甚至从明天开始。

下面列出的最佳实践和技巧将使大多数希望今天比昨天更好的软件开发人员受益。

# 应用程序性能

**1。**对于本地环境中没有的大型数据集，您的代码可能会运行得非常慢，但这可能会出现在生产环境中。问自己这样一个问题:“随着数据的增长，我使用的算法和数据结构能很好地扩展吗？”。

**2。不要浪费时间去实现高效的数据结构算法，这些数据结构包含的元素不会超过几个。**

**3。根据您将经常对其执行的操作类型来选择数据结构。例如，考虑基于散列的数据结构用于频繁的搜索和罕见的插入。但是考虑快速插入和罕见搜索的链表。**

**4。**不要从数据库中提取最少量的数据，以避免频繁的数据库调用。不要通过一次数据库调用获取所有数据，因为这会花费很长时间。在两者之间找到一个平衡点。

**5。**了解性能模式，如延迟加载、Flyweight、对象池、缓存等等。还要学习常见的性能反模式，如 N+1 问题以及如何避免它们。

**6。**如果迭代相互独立，考虑并行化长“for”循环的可能性。

**7。**好的业绩不是免费的。提高性能需要开发人员花费时间。可能需要牺牲安全性或其他质量属性来提高性能。在积极投资绩效之前，与客户明确绩效目标。

# 重构

**8。不要在代码中留下类似“TODO: Refactor later”的注释，因为它们会永远留在那里。相反，在问题跟踪系统中注册一个技术债务项目，标记为技术债务。**

9。在重构代码之前，确保它被一套全面的单元测试所覆盖。逐一查看每个测试用例，以便更好地理解要重构的代码。

10。如果你想重构的代码没有单元测试，首先实现它们。这将允许您捕捉回归问题，并增加整体单元测试覆盖率。

**11。**如果你要重构遗留代码，并且不知道它的确切行为，你就不能编写单元测试。相反，编写[特性测试](https://michaelfeathers.silvrback.com/characterization-testing)来捕捉要重构的代码的现有行为。

12。想出一个由小的增量变化组成的重构计划(1。将方法移到另一个类别，请按 2。拆分方法，3。重命名类等。).每次更改后运行单元测试。如果出现故障，很容易后退一步来确定故障的根本原因。

**13。尽可能多地使用 IDE 提供的自动化重构工具，而不是手动重构。**

# 代码审查

**14。**您的代码评审请求应该比您的开发任务具有更高的优先级，以避免长期的拉请求和合并冲突。

**15。**在拉取请求中仅包含与您正在处理的吉拉机票相关的代码。

**16。**确保您理解您正在审查的功能的验收标准。不要只从技术角度审查代码，还要从需求角度检查(是否所有需求都实现了)。

**17。**始终在吉拉记录单上记录你花在代码评审上的时间，就像记录你花在编码上的时间一样。

**18。**当审查一个包含业务逻辑变更的 bug 修复时，确保相应的单元测试也有变更。如果逻辑已经改变，但是单元测试没有改变，那么您就错过了测试覆盖。

[](/how-to-professionally-to-do-a-code-review-of-a-bug-fix-f17de72d42e0) [## 如何专业地对 Bug 修复进行代码审查

### 审查 bug 修复时要问的几个重要问题。

levelup.gitconnected.com](/how-to-professionally-to-do-a-code-review-of-a-bug-fix-f17de72d42e0) 

# 任务评估

19。当被问到时，不要试图对你的任务做一个粗略的估计。尽可能晚地向你的客户或经理提供评估。

20。提供一个范围内的估计值，较低的数字是乐观值，最高的数字是悲观值。例如，乐观— 3 天，悲观— 7 天。

21。评估复杂任务时，使用分解/重组和基于类比的评估技术。根据需要将任务分解成多个部分，直到可以通过类比来估计复杂任务的各个部分。

**22。** **随着你发现更多以前不知道的细节，调整你的估计。尽快与你的团队成员、经理、客户沟通评估的变化，这样就不会在预期完成工作的最后一刻说“我需要额外的 3 天”而让他们感到惊讶。**

**23。**总是请更有经验的队友来帮你估算你从未实现过类似东西的功能。

[](https://medium.datadriveninvestor.com/estimation-hell-or-what-can-developers-do-better-with-their-estimates-614f9e71f43d) [## 评估地狱，或者开发人员如何利用他们的评估做得更好？

### 估计过程很难，但没那么难。

medium.datadriveninvestor.com](https://medium.datadriveninvestor.com/estimation-hell-or-what-can-developers-do-better-with-their-estimates-614f9e71f43d) 

# 错误修复

24。在解决这个问题之前，实现一个单元测试来覆盖你未来的代码变更。

**25。找到您要修改以解决问题的方法或类的所有输入依赖项。这将允许您看到应用程序的哪些部分由于您的更改而面临风险。**

**26。** **始终确保您正在修复问题的原始根本原因，而不是其症状之一。如果你没有时间解决问题的根源，向吉拉提交一张科技债务票据。**

**27。**在将修复合并到主分支之前，在本地测试它。运行所有可用的测试，通过 UI 手动检查行为，检查几条快乐的路径。

[](/how-to-fix-bugs-and-not-introduce-new-ones-9f35e625673a) [## 如何在不破坏应用程序的情况下修复 Bug

### 更改源代码时更自信的步骤。

levelup.gitconnected.com](/how-to-fix-bugs-and-not-introduce-new-ones-9f35e625673a) 

# 要求

**28。**在开始实施之前检查需求。确保需求至少是完整的、必要的、可行的，并且对于你将要从事的用户故事来说是明确的。

**29。**阐明非功能性需求，例如用户故事的性能或可伸缩性，如果没有指定的话。这可以避免您在未来进行返工，因为例如，100 毫秒和 1 秒的代码执行可能需要完全不同的编码技术、设计模式或整个架构。

# 参加会议

三十岁。如果你被邀请参加一个会议，请事先确保你了解会议的目的和你在会议中的角色。尽可能仔细地为会议做准备。

## 我的其他文章

[](/developers-shouldnt-be-afraid-of-deadlocks-in-sql-server-8f8f4578675f) [## 开发人员不应该害怕 SQL Server 中的死锁

### 后端开发人员处理死锁的策略。

levelup.gitconnected.com](/developers-shouldnt-be-afraid-of-deadlocks-in-sql-server-8f8f4578675f) [](/7-tricky-questions-to-ask-net-developer-in-a-job-interview-9cdb3789db54) [## 要问的 7 个棘手问题。NET 开发人员在工作面试

### 带着答案。

levelup.gitconnected.com](/7-tricky-questions-to-ask-net-developer-in-a-job-interview-9cdb3789db54) [](/how-many-repositories-do-you-need-for-a-microservices-project-b5c991aa440) [## 一个微服务项目需要多少个存储库？

### 在多存储库和单存储库之间找到平衡点。

levelup.gitconnected.com](/how-many-repositories-do-you-need-for-a-microservices-project-b5c991aa440)