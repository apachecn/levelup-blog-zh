# 捍卫干净的代码

> 原文：<https://levelup.gitconnected.com/in-defense-of-clean-code-2592165487d4>

## 来自鲍勃叔叔的 100 多条永恒的建议

![](img/ff3a3b8d2628093acb306d991dd83a03.png)

*干净码*书的封面

罗伯特·c·马丁的《干净的代码》是有史以来最值得推荐的编程书籍。搜索任何“软件工程师的顶级书籍”列表，你几乎可以保证在列表中找到这本书。

然而，有些人对*干净代码*又爱又恨，甚至说[可能是时候停止推荐*干净代码*](https://qntm.org/clean) 了。我认为这种观点被严重误导了。

是的，书中的一些建议是有问题的。是的，有些内容感觉过时了，或者没有随着时间的推移而变得陈旧。是的，有些例子令人困惑。所有这些都是真的。但是我们不要这么快就对这本书提供的所有好建议打折扣！

仅仅因为几个糟糕的想法而完全忽略一本书，是几种认知扭曲的完美例子:心理过滤、放大和忽视积极的东西，等等。

事实上，鲍勃大叔和其他撰稿人已经在本书的第一章中小心翼翼地处理了这一问题:

> 这本书里的许多建议都是有争议的。你可能不会同意他们所有人的观点。你可能会强烈反对其中一些。那很好。我们不能宣称最终的权威。另一方面，这本书里的建议是我们深思熟虑过的。我们通过几十年的经验和反复的试验和错误学会了它们。所以不管你同意还是不同意，如果你不理解和尊重我们的观点，那将是一种耻辱。

所以，事不宜迟，让我们考虑一下*干净代码*提供的所有永恒的建议！我们将一章一章地浏览这本书，总结鲍勃叔叔提出的许多观点。

# 第 1 章:干净的代码

1.  拥有一家餐厅的总成本会随着时间的推移而增加。
2.  从头开始重建一个遗留系统是非常困难的。重构和渐进式改进通常是更好的途径。
3.  在混乱的代码库中，完成原本只需要几个小时的任务可能需要几天或几周的时间。
4.  抓紧时间快速前进。
5.  干净的代码做好了一件事。糟糕的代码试图做太多事情。
6.  干净的代码是久经考验的。
7.  当阅读编写良好的代码时，每个函数都做了您所期望的事情。
8.  如果你不同意一个有着几十年经验的人正在教导的原则，你最好在忽视它之前至少考虑一下他们的观点。
9.  代码被阅读的次数远远多于它被编写的次数。
10.  易读的代码更容易修改。
11.  留下比你发现时更好的代码库(童子军规则)。

# 第 2 章:有意义的名称

1.  仔细选择变量名。
2.  选择好名字很难。
3.  变量或函数的名字应该告诉你它是什么以及如何使用它。
4.  避免使用单字符变量名，除了循环中计数器变量的常用名`i`。
5.  避免在变量名中使用缩写。
6.  变量名应该是可发音的，这样你就可以谈论它们并大声说出来。
7.  使用易于搜索的变量名。
8.  类和对象的名字应该是名词。
9.  方法和函数的名称应该是动词或动词-名词对。

# 第三章:功能

1.  功能应该很小。
2.  函数应该做一件事。
3.  函数应该有描述性的名字。(重复自第 2 章)
4.  提取 if/else 主体中的代码，或者将语句切换到命名清晰的函数中。
5.  限制函数接受的参数数量。
6.  如果一个函数需要很多配置参数，可以考虑将它们合并到一个配置选项变量中。
7.  函数应该是纯的，这意味着它们没有副作用，并且不修改它们的输入参数。
8.  函数应该是命令或查询，但不能同时是命令和查询(命令查询分离)。
9.  抛出错误和异常，而不是返回错误代码。
10.  将重复的代码提取到明确命名的函数中(不要重复)。
11.  单元测试使重构更容易。

# 第 4 章:注释

1.  评论可以骗人。它们可能一开始就是错误的，或者它们可能最初是准确的，但随着时间的推移，随着相关代码的变化，它们就变得过时了。
2.  用评论来描述*为什么*某件事被写成这样，而不是解释*T4 正在发生什么。*
3.  通过使用明确命名的变量和将代码段提取到明确命名的函数中，通常可以避免注释。
4.  以一致的方式为您的 TODO 注释添加前缀，以便于搜索。定期回顾和清理你的待办事项。
5.  不要为了使用 Javadocs 而使用它们。描述一个方法做什么、它采用什么参数以及它返回什么的注释，往好里说是多余的，往坏里说是误导的。
6.  评论应该包括阅读评论的人需要的所有相关信息和背景。写评论的时候不要偷懒，不要含糊。
7.  由于版本控制和 git 的原因，日志注释和文件作者注释是不必要的。
8.  不要注释掉死代码。删了就好。如果您认为将来会需要这些代码，这就是版本控制的作用。

# 第 5 章:格式

1.  作为一个团队，选择一套规则来格式化您的代码，然后一致地应用这些规则。你同意什么规则并不重要，但你确实需要达成一致。
2.  使用自动代码格式化程序和代码 linter。不要依靠人工来捕捉和纠正每个格式错误。这是低效的，非生产性的，并且在代码审查期间浪费时间。
3.  在代码中添加垂直空格，以直观地分隔相关的代码块。您只需要在组之间添加一个新的行。
4.  小文件比大文件更容易阅读、理解和浏览。
5.  变量应该在靠近使用它们的地方声明。对于小函数，这通常在函数的顶部。
6.  即使是短函数或 if 语句，也要正确格式化，而不是写在一行上。

# 第 6 章:对象和数据结构

1.  对象中的实现细节应该隐藏在对象的接口后面。通过提供一个接口供对象的消费者使用，您可以更容易地在以后重构实现细节，而不会导致破坏性的更改。抽象使得重构更加容易。
2.  任何给定的代码都不应该知道它正在处理的对象的内部。
3.  当处理一个对象时，你应该让它执行命令或查询，而不是询问它的内部结构。

# 第 7 章:错误处理

1.  错误处理不应该掩盖模块中的其他代码。
2.  抛出错误和异常，而不是返回错误代码。(重复自第 3 章)
3.  编写强制错误的测试，以确保您的代码处理的不仅仅是快乐路径。
4.  错误消息应该是信息性的，提供得到错误消息的人为了有效地进行故障诊断所需要的所有上下文。
5.  将第三方 API 封装在一个抽象薄层中，使得将来用一个库替换另一个库变得更加容易。
6.  将第三方 API 封装在一个抽象薄层中，使得在测试过程中模仿库变得更加容易。
7.  使用特例模式或空对象模式来处理异常行为，比如当某些数据不存在时。

# 第八章:界限

1.  第三方库允许您外包各种问题，从而帮助您更快地交付产品。
2.  编写测试以确保您对任何给定第三方库的使用都正常工作。
3.  使用适配器模式在第三方库的 API 和您希望它拥有的 API 之间架起一座桥梁。
4.  将第三方 API 封装在一个抽象薄层中，使得将来用一个库替换另一个库变得更加容易。(重复自第 7 章)
5.  将第三方 API 封装在一个抽象薄层中，使得在测试过程中模仿库变得更加容易。(重复自第 7 章)
6.  避免让你的应用程序知道太多任何给定的第三方库的细节。
7.  依赖你能控制的东西比依赖你不能控制的东西要好。

# 第 9 章:单元测试

1.  测试代码应该像生产代码一样保持整洁(除了一些例外，通常涉及内存或效率)。
2.  随着产品代码的变化，测试代码也在变化。
3.  测试有助于保持产品代码的灵活性和可维护性。
4.  测试通过允许您自信地重构而不用担心不知不觉地破坏东西，从而支持变更。
5.  使用 Arrange-Act-Assert 模式(也称为 Build-Operate-Check、Setup-Exercise-Verify 或 Given-When-Then)构建您的测试。
6.  使用特定领域的函数使测试更容易编写和阅读。
7.  每次测试评估一个概念。
8.  测试应该很快。
9.  测试应该是独立的。
10.  测试应该是可重复的。
11.  测试应该是自我验证的。
12.  测试应该及时地编写，可以在产品代码编写之前或之后不久，而不是几个月后。
13.  如果你让你的测试腐烂，你的代码也会腐烂。

# 第 10 章:类

1.  班级应该很小。
2.  类应该只对一件事负责，并且应该只有一个改变的理由(单一责任原则)。
3.  如果你不能为一个类想出一个清晰的名字，它可能太大了。
4.  一旦你让一段代码开始工作，你的工作就没有完成。下一步是重构和清理代码。
5.  在你的应用中使用许多小类而不是几个大类，可以减少开发者在处理任何给定任务时需要理解的信息量。
6.  有了一个好的测试套件，当您将大型类分解成较小的类时，您就可以放心地进行重构。
7.  类应该对扩展开放，但对修改关闭(开闭原则)。
8.  接口和抽象类提供了使测试更容易的接口。

# 第十一章:系统

1.  使用依赖注入使开发人员能够灵活地将任何具有匹配接口的对象传递给另一个类。
2.  使用依赖注入在应用程序中创建对象接缝，使测试更容易。
3.  软件系统不像一个必须预先设计好的建筑。它们更像是随着时间的推移而成长和扩张的城市，适应当前的需求。
4.  将决策推迟到最后负责任的时刻。
5.  使用特定于领域的语言，以便领域专家和开发人员使用相同的术语。
6.  不要让你的系统过于复杂。使用最简单有效的方法。

# 第十二章:紧急情况

1.  不可测试的系统不可验证，不可验证的系统永远不应该被部署。
2.  编写测试会带来更好的设计，因为易于测试的代码通常使用依赖注入、接口和抽象。
3.  一个好的测试套件可以消除你在重构过程中破坏应用程序的恐惧。
4.  代码中的重复会产生更多的风险，因为代码中有更多的地方需要修改，也有更多的地方需要隐藏 bug。
5.  理解你正在编写的代码是很容易的，因为你已经深入地参与了对它的理解。对于其他人来说，很快获得相同程度的理解并不容易。
6.  软件项目的大部分成本是长期维护。
7.  测试就像是你的应用应该(和确实)如何运行的活文档。
8.  不要一让代码工作起来就继续前进。花点时间让它更清晰，更容易理解。
9.  在不久的将来，下一个阅读你的代码的人很可能就是你。通过编写易于理解的代码，善待未来的自己。
10.  抵制教条。拥抱实用主义。
11.  真正精通软件工程需要几十年的时间。通过向周围的专家学习和学习常用的设计模式，可以加快学习过程。

# 第十三章:并发

1.  编写并发代码很难。
2.  随机错误和难以重现的问题通常是并发问题。
3.  测试并不能保证您的应用程序中没有错误，但是它确实可以将风险降到最低。
4.  了解常见的并发问题及其可能的解决方案。

# 第 14 章:连续细化

1.  干净的代码通常不会一开始就很干净。你先写一个脏的解决方案，然后重构它使它更干净。
2.  一旦代码“工作”了，就停止工作是错误的在你让它工作之后，花些时间让它变得更好。
3.  混乱是逐渐形成的。
4.  如果你发现自己陷入了添加特性太困难或花费太长时间的困境，停止编写特性并开始重构。
5.  与从头开始重建相比，进行渐进式更改通常是更好的选择。
6.  使用测试驱动开发(TDD)进行大量非常小的更改。
7.  好的软件设计包括分离代码中的关注点，并将代码分割成更小的模块、类和文件。
8.  在你制造了一个烂摊子后马上清理它比事后清理要容易得多。

# 第 15 章:JUnit 内部

1.  负变量名或条件比正变量名或条件稍微难理解。
2.  重构是一个充满试错的迭代过程。
3.  让代码比你发现的更好一点(童子军规则)。(重复自第 1 章)

# 第十六章:重构序列日期

1.  代码评审和对代码的批评是我们变得更好的方式，我们应该欢迎它们。
2.  首先让它工作，然后让它正确。
3.  不是每一行代码都值得测试。

# 第十七章:气味和启发

1.  干净的代码不是一套规则，而是一个驱动你工作质量的价值体系。

在这一章中，Bob 叔叔列举了他的 66 种代码气味和启发法，其中许多在本书的其余部分都有涉及。在这里复制它们实质上就是复制和粘贴每一个条目的标题，所以我没有这样做。相反，我会鼓励你去读这本书！]

# 结论

让我们从开始的地方结束:*Robert c . Martin 的《干净的代码》*是有史以来最值得推荐的编程书籍。

有一个很好的理由。