# 面向技术领导者和资深人士的 50 个软件工程最佳实践

> 原文：<https://levelup.gitconnected.com/50-software-engineering-best-practices-for-technical-leaders-and-seniors-cfcdf6a17e44>

## 最佳工程师的最佳实践。

![](img/545db6fd49c3091709229a90d1b95b38.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) 拍摄的照片

软件工程师定期从软件开发的各个领域学习最佳实践。学习最佳实践，然后找到将它们应用到项目中的正确方法，使软件工程师变得成熟，并帮助他们的项目成功。

当选择要关注的最佳实践集时，程序员的经验很重要。初级工程师通常学习编写单元测试或避免代码味道的最佳实践，而高级或技术领导应该学习影响整个项目或开发过程的最佳实践。

# 第三方库的使用

**1。**第三方库注册发布在项目空间( [Confluence](https://www.atlassian.com/software/confluence) ，Wiki)上，由技术负责人或架构师定期维护。

**2。**使用第三方库必须遵守其许可协议。

**3。**应用程序不应该直接使用库，而是通过 **facade 设计模式**。这避免了第三方库和应用程序代码之间的紧密耦合，因此可以很容易地用新的库替换该库。

**4。**应用程序功能的集成测试应涵盖第三方库的代码。这些集成测试确保新版本的库不会破坏应用程序的功能。

**5。**开发团队应该使用积极维护的库。

# 记录和监控

**6。**记录消息时，应用程序应使用最合适的记录级别(跟踪、调试、信息、警告、错误等)。).

7。应该可以通过配置文件改变日志级别，而无需重新部署代码。

8。在记录消息时使用**结构化记录技术**，这样您可以通过编写查询来分析大量日志。

9。即使主动向监控工具发送大量日志也不会显著影响应用程序的性能。记录调用应该是非阻塞的。此外，它们可以在单独的线程中进行批处理和发送。

10。使用 Application Insights、Stackdriver 等监控工具。监控工具被配置为当应用程序超过任何阈值时发送通知。

🔔 [**现在订阅**](https://esashamathews.medium.com/subscribe) **，所以大家不要错过我接下来的文章。**

# 代码审查过程

**11。为了避免长期的拉请求，代码评审比开发任务具有更高的优先级。**

**12。**代码审查过程是自动化的，而不是手动的。[使用 GitHub](https://github.com/) 、[坩埚](https://www.atlassian.com/software/crucible)、[评审板](https://www.reviewboard.org/)或其他工具。

**13。不超过**300–400**行的代码被发送给代码评审。考虑将一个大的功能分解成较小的任务，开发人员可以单独检查。**

14。评审者应该能够记录花在代码评审上的时间。

15。审查者清楚地理解他正在审查的代码的接受标准。

16。评审者根据**代码评审清单**评审代码。检查表应该存在于项目空间中，以便所有开发人员都可以访问和使用它。

17。在将代码提交到主分支之前，每个提交应该由至少一个或两个团队成员审查。

# 技术债务管理

18 岁。一旦开发人员在源代码中看到技术债务，他们应该在问题跟踪系统中创建描述良好的技术债务单。

**十九。**所有技术债务票据应以某种方式分组:1)技术债务 epic，2) *“技术债务”*标签或 3)票据标题的命名约定。

20。开发团队应该通过在每个 sprint 中包含一些技术债务票据，或者通过将整个 sprint ( **技术 sprint** )用于处理技术债务，来防止技术债务的增长。

**21。**开发团队应该在待办事项细化会议期间对技术债务单进行优先排序和评估。

**22。**每个利益相关者都需要知道如何快速找到所有的技术债单。

# 评估和流程规划

**23。**整个开发团队都参与评估，而不仅仅是技术领导或架构师。

**24。在项目空间中为故事定义并发布 Done (DoD)** 的定义。在进行评估之前，团队必须就完成的定义达成共识。

**25。**开发人员使用[三点估算](https://en.wikipedia.org/wiki/Three-point_estimation)或 [PERT 公式](https://en.wikipedia.org/wiki/Program_evaluation_and_review_technique)来估算工作，而不仅仅是单个值。

**26。评估应该包括编写单元测试、通过代码评审和测试活动所需的努力。**

**27。基于类比的估算**、**故事点**、**策划扑克**、**分解**和**重组**技术在估算过程中使用。

28。团队应该在积压工作梳理或冲刺计划会议期间定期审查现有的评估，并根据需要进行改进。

29。所有团队成员都应该参与到冲刺规划过程中。

三十岁。所有的开发人员都应该参与到设计阶段，而不仅仅是高级职员。

31。技术负责人以单独任务的形式进行工作委派。

32。每个任务都应该有一个书面的验收标准。

# 源代码管理

**33。**项目源代码和所有相关脚本(数据库脚本、构建或部署脚本)应存储在版本控制系统中。

34。分支的每个提交应该包含来自问题跟踪系统的工作项 ID 和描述。

**35。**开发人员每天几次将变更推送到特性分支**。**

**36。每个提交必须包含特定于唯一工作项的功能。**

****37。**开发人员应该在主分支机构的请求被批准后立即将请求合并到主分支机构，以避免合并冲突。**

****38。**从源代码或第三方包编译输出的二进制文件应通过配置 **gitignore** 文件从源代码控制中排除。**

****39。**特定于环境的数据，如连接字符串，应与源代码分离，并存储在配置文件或环境变量中。**

**40。开发团队应该定义满足项目需求的分支和合并策略，并在项目空间中描述它们。**

# **数据库变更管理**

**41。数据库模式和**引用数据**(运行应用程序所需的数据)应该存储在源代码控制中。**

****42。**开发团队应该根据项目需求在**基于状态的**和**基于迁移的**方法之间进行选择。**

****43。**开发人员应该始终通过源代码控制中的数据库脚本来修改数据库。如果开发人员直接更改了数据库，他应该在源代码控制中进行同样的更改。**

****44。**每个开发人员都应该有自己的本地数据库，他们可以通过运行从存储库中获取的数据库脚本来轻松创建。**

# **持续集成和交付**

****45。**持续集成工作流应该由技术经理或架构师记录，并与团队共享。**

****46。**运行静态代码分析器工具应该包含在持续集成管道中，并在代码质量度量低于指定时导致构建失败。**

****47。**持续集成管道应该运行所有单元测试，如果任何单元测试失败，就会导致构建失败。**

**48。在将代码提交到存储库之前，开发人员应该在本地运行单元测试。**

**49。构建通知已配置。构建服务器自动向所有相关方发送关于构建状态的通知。**

**50。构建工件应该使用语义版本控制进行版本控制。**

**51。每个构建都与存储库中相应的提交相关联。**

**52。为失败的部署定义和配置回滚程序。**

# **代码质量**

****53。**开发团队应该定期收集和分析代码质量指标，以尽快识别任何代码问题。**

****54。**所有团队成员都应该使用与构建服务器配置相同的静态代码分析工具。**

**可以考虑订阅我的电报频道 [**软件开发日报**](https://t.me/sd_daily) 从我这里获取更多内容。**

## **更多软件工程文章**

**[](https://esashamathews.medium.com/top-best-practices-for-writing-brilliant-unit-tests-3af3e9ddce79) [## 编写优秀单元测试的最佳实践

### 这可以最大化你的单元测试套件的好处。

esashamathews.medium.com](https://esashamathews.medium.com/top-best-practices-for-writing-brilliant-unit-tests-3af3e9ddce79) [](/how-to-fix-bugs-and-not-introduce-new-ones-9f35e625673a) [## 如何在不破坏应用程序的情况下修复 Bug

### 更改源代码时更自信的步骤。

levelup.gitconnected.com](/how-to-fix-bugs-and-not-introduce-new-ones-9f35e625673a) [](https://medium.com/geekculture/common-programmer-mistakes-that-fail-projects-57d131e755df) [## 导致项目失败的常见程序员错误

### 从别人的错误中学习。

medium.com](https://medium.com/geekculture/common-programmer-mistakes-that-fail-projects-57d131e755df) [](/develop-these-few-habits-to-become-an-outstanding-software-engineer-8117a155af77) [## 养成这几个习惯，成为一名优秀的软件工程师

### 你所需要的只是纪律。

levelup.gitconnected.com](/develop-these-few-habits-to-become-an-outstanding-software-engineer-8117a155af77)**