# 代码评审期间要检查的 50 件重要事情

> 原文：<https://levelup.gitconnected.com/50-critical-things-to-check-during-a-code-review-221e03b69f42>

## 对于后端 web 开发人员来说。

![](img/389fa666bacb17a8a8bdc9fefece0af4.png)

克里斯汀·休姆在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

代码审查过程应该尽可能自动化。创建一个拉请求应该至少触发功能分支上的单元测试和静态代码分析。自动化工具可以提供很多关于代码质量的信息:度量、单元测试覆盖率、检测重复行等等。

然而，至少有 50 种东西无法自动检查，需要有经验的审查者的仔细观察(这让我们看到了机器人不会在不久的将来取代开发人员的希望)。

# 要求

1.代码是否实现了用户故事中描述的所有功能需求？

2.代码是否满足非功能性需求，如性能或安全性？[故事中根本没有提到非功能需求](/why-missing-non-functional-requirements-can-be-a-disaster-b0b8028acca1)？在这种情况下，他们是否与架构师或客户进行了澄清？

# 可维护性

3.根据 **Onion/Clean** 架构，每个接口、类或其他类型是否都放在适当的应用层？

4.代码是不是重新实现了轮子？它是否应该被某个第三方库提供的现有逻辑所取代？

5.实现的逻辑或它的某些部分是否已经存在于代码库中？

6.依赖注入容器中的接口和实现的生存期范围选择是否正确？

7.实现的函数的行为是确定的吗(总是为相同的输入返回相同的输出)？

8.所有的依赖都是通过类型构造函数显式注入的吗？

9.类之间的紧密耦合会使代码更难重用吗？

10.是否使用**值对象**代替原始数据类型来避免原始困扰问题？

11.每个实现的组件如函数、类、接口或模块是否遵循**单一责任原则**？

12.现有功能是用 decorators、面向方面的编程技术(开闭原则)扩展的，还是就地修改的？

13.在 web 应用中访问单例对象是否正确实现了线程同步机制？

14.为了避免副作用，是否尽可能使用不可变数据类型**而不是可变数据类型**？

15.具有正确的**日志记录级别**的日志记录是否被添加到代码中应该被跟踪的重要位置？

# 表演

![](img/8a95627dd33a090355c2e55959d67c6b.png)

照片由 [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

16.**数据结构**选择正确吗？例如，当需要频繁查找值而不是对象数组以避免线性搜索时，是否使用`Hashtable`结构？

17.长时间运行的操作是否跨所有可用的内核并行化，以有效利用机器的资源？

18.代码是否在堆上执行了许多对象的**分配**，给垃圾收集器带来了压力？

19.从数据库**中读取的数据是缓存在本地内存还是远程缓存中？**

20.当前代码进行了多少次数据库调用？也许只需一次或几次通话就能获得所有数据，而不是多次通话，这是值得的？

21.代码是否以异步方式执行所有数据库、I/O 或其他阻塞调用？

22.代码是否充分利用了**线程池**而不是创建新线程？

23.在实现额外的数据库表时，是否在**规范化**和**反规范化**之间选择了正确的平衡？

24.如果 pull 请求包含新的 SQL 查询，索引是否被适当地添加或修改？

25.当使用 ORM 框架从数据库获取数据时，会有 N+1 问题吗？

26.存储过程中是否设置了适当的事务隔离级别？

27.SQL 查询会从数据库中返回应用程序代码不需要的冗余数据吗？像`SELECT *`之类的东西有没有用？

# 单元和集成测试

28.单元测试是否完全覆盖了添加的逻辑？

29.当逻辑中存在修复时，相应的单元测试是否有变化？

30.所有实现的单元或者其他类型的测试总是表现出确定性吗？例如，在断言之前，它们是否暂停线程执行一段时间(这是一种反模式)？

31.每个单元测试都是根据 **F.I.R.S.T.** 原则实施的吗？

32.有没有单元测试闻起来像*条件测试逻辑、断言轮盘、重复断言*或其他？

33.是否添加了集成测试，至少是针对已实现特性的快乐路径场景？

34.是否所有的 SUT 对象(**s**system**u**under**t**est)依赖关系都被模拟，以便单元测试不会意外地变成集成测试并快速运行？

35.单元测试或集成测试是相互隔离的吗？

# API 端点

36.诸如 *GET、POST、PUT、DELETE* 等 HTTP 动词是根据端点实际在做什么来选择的吗？

37.是不是每个 API 端点只负责执行一个业务操作，而不是多个？

38.API 端点是否返回正确的状态代码？例如，对于未经授权的请求，它是否返回 401 而不是 500？

39.大型响应在返回给调用者之前是否经过压缩？

40.每个 API 端点都受到身份验证和授权策略的保护吗？

41.一个返回大量对象列表的 API 允许过滤和分页吗？

42.GET API 端点幂等吗？

43.API 端点名称中是否用名词代替动词？

# 重大变化

44.API 端点是否有重大更改，比如重命名 API、删除或重命名其参数？

45.消息负载中是否有重大变化(在使用消息代理的情况下)，比如删除或重命名其属性？

46.对数据库模式的更改(如删除列或表)会影响系统的其他服务吗？

# 环境

47.拉请求中的代码在执行时消耗了多少 CPU 和 RAM？将部署代码的环境(QA、UAT、生产)是否有足够的 CPU 和 RAM 来高效地运行代码？

48.实现的逻辑、算法、数据结构等。，在一个**生产环境**可能拥有的大型数据集上运行得足够快？

# 证明文件

49.文档是否已更新以反映新的代码变更(API 文档、架构或设计文档等)。)?

50.如果拉请求包含由于时间限制而无法重构的低效或肮脏的代码，是否会产生一张**技术债务**罚单？

# 结论

评审者应该关注的项目数量取决于具体的项目，甚至取决于每个具体的拉取请求。使用上面的技巧，你的经验和与同事的头脑风暴将极大地减少在代码审查期间一些关键的东西被忽略的风险。

感谢阅读。如果你喜欢你所读到的，看看下面这个故事:

[](/20-code-design-tips-for-developers-for-everyday-use-ed7c4413b544) [## 开发者日常使用的 20 个代码设计技巧

### 从实际的拉取请求中收集。

levelup.gitconnected.com](/20-code-design-tips-for-developers-for-everyday-use-ed7c4413b544) 

还有，考虑成为[中等成员](https://esashamathews.medium.com/membership)。

# 分级编码

感谢您成为我们社区的一员！在你离开之前:

*   👏为故事鼓掌，跟着作者走👉
*   📰查看[升级编码出版物](https://levelup.gitconnected.com/?utm_source=pub&utm_medium=post)中的更多内容
*   🔔关注我们:[Twitter](https://twitter.com/gitconnected)|[LinkedIn](https://www.linkedin.com/company/gitconnected)|[时事通讯](https://newsletter.levelup.dev)

🚀👉 [**加入升级达人集体，找到一份惊艳的工作**](https://jobs.levelup.dev/talent/welcome?referral=true)