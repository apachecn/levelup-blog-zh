# 颤振发展的五大局部数据库解决方案

> 原文：<https://levelup.gitconnected.com/top-5-local-database-solutions-for-flutter-development-6351cd494070>

## 这里列出了最流行的数据库解决方案，以及代码示例。

![](img/5f22744ea13c201c4d37a3f82e5c6b85.png)

选择正确的数据管理系统对于提高**效率**和**可扩展性**，以及影响**可用性**和**用户体验**至关重要。尽管 flutter 仍处于早期阶段，但有各种各样的数据管理解决方案可供使用，其中一些已经可以投入生产。我将向您概述用于本地维护数据的最常见的数据库管理系统。

## [Sqflite](https://pub.dev/packages/sqflite)

Sqflite 是一个众所周知的 **SQLite** flutter 插件。它是一个关系数据库，具有优秀的**事务**和**批处理**支持。当数据库打开时，它自动管理**版本**。它还包括常见的 **CRUD** 操作的助手。后台线程处理所有的数据库操作。它符合 ACID 标准，因此支持几乎所有的 SQL 标准。如果您喜欢将自己的 SQL 查询写成字符串，这个简单的插件将满足您的数据管理需求。

从例子中可以看出，我觉得阅读这段代码并不容易。随着应用程序的增长，维护这些代码将变得单调乏味。因为 *sqflite* 是一个基本的**数据库管理系统(DBMS)** 插件，我相信你应该构建自己的结构，并围绕 *sqflite* 包装它，就像大多数用于 flutter 的**关系 DBMS** 包一样。

SQLite 一般是一个**自包含**、**无服务器**、**轻量级**解决方案。它的性能是有争议的，但是它允许你使用一个快得惊人的内存数据库。基础包包括移动平台支持。**没有 web 支持**，但是 *sqflite_common_ffi* 可以用来支持桌面平台。

## [地板](https://pub.dev/packages/floor)

Floor 是一个非常有用的 **SQLite** 抽象，包括一个**对象映射器**。它依赖于 *sqflite* ，并在此基础上增加了类似**类型安全**的特性。它支持 *sqflite* 支持的一切，包括**内存**数据库。

虽然它充当了 *sqflite* 的包装器，但它引入了更高级的概念，如 **DAOs** 和**实体**。实体可以用来将内存中的对象映射到数据记录，并且 DAOs 允许你访问数据。拥有清晰的分离总是一个好主意，比如**实体、DAO 和数据库**。您还可以为您的 Dao 编写良好的**测试**，并确保您的查询以这种方式得到验证。

前面的代码示例演示了**如何创建实体**。使用**注释**引导楼层创建合适的数据库表。这是一种非常用户友好的数据库设计方法。我们来看看一把**刀**是怎么造出来的。

您所要做的就是提供一个带有适当注释的抽象类。不幸的是，没有查询 API，所以您仍然必须提供一个字符串形式的 SQL 查询。这种方法对我来说特别没有吸引力，因为这些查询没有可用的语法检查。您仍然可以测试和验证这些查询。

Floor 正在一个**构建器**的帮助下生成必要的代码。因此，所有的 Dao 都存储在数据库中。要插入一个人，调用**database . person Dao . insertperson(person)**。老实说，我不认为通过数据库对象访问所有的 Dao 是一个好主意。然而，这种丑陋可以通过使用依赖注入容器来避免。

总的来说，Floor 是一个有前途的 *sqflite* 包装器，具有许多有用的特性。更多信息请参见他们的 [**文档**](https://floor.codes/) 。它用例子和图表清楚地展示了所有的特性。

## [漂移](https://drift.simonbinder.eu)(摩尔)

Drift (Moor)无疑是功能最丰富的 flutter 关系型 DBMS 解决方案。它也是围绕 *sqflite* 的一个包装器，但是它为您提供了更多的功能，并且包含了一个**查询 API** 。尽管**网站**的支持是实验性的，但它支持所有潜在的平台。此外，它还为**事务**、**模式迁移**、**复杂过滤器**和**表达式**以及**批处理**流程提供了出色的支持。

它为 **DAOs** 和**实体**提供了类似的支持，比如 floor，但是它是以高度模块化的方式实现的，允许您毫不费力地将它与您的 **DI 容器**绑定相结合。这个解决方案的另一个出色的特性是**内置的线程**支持，它允许您毫不费力地跨**隔离**运行数据库代码。最后，值得注意的是，它包括一个用于 SQL 查询的集成 IDE。多酷啊！

让我们来看一些代码示例，以便您可以将其与 *floor* 进行比较。下面是一个如何定义表格的例子。

代替**注释**，我们**扩展**的 ***表*** 类，并为该列的数据类型使用特定的列类型。在这里我们可以为单独的列配置各种属性，比如**为空性**、**外键**、和**约束**。说到桌子定义，我必须承认我喜欢*地板的*方式。它对我来说更具可读性，注释的使用是一个绝妙的概念。

这就是**刀**的定义。

毫无疑问，您注意到的第一件事是**查询 API** 而不是**基于文本的 sql** 查询。就个人而言，我喜欢**查询 API** ，因为随着项目的扩展，您会发现一些过滤器或数据访问方法可能会被简化。你可以在不牺牲查询可读性的情况下减少代码重复。我知道学习另一种 API 而不是 SQLite 语法看起来可能不是最舒服的选择，但是绝对值得。我很欣赏这个想法，完整的数据库逻辑可以用 Dart 编写，在**编译**过程中可以检测到可能的错误。

当我需要使用一个**关系本地数据库**时，漂移是我的第一选择。它只是给出了一个更有效的开发和**扩展**的方法。因为插件采用了代码生成，我相信实体和 DAO 声明可能会更加**用户友好**。该项目仍在积极开发中，每个新版本都比前一个版本有所改进。

## [蜂巢](https://pub.dev/packages/hive)

Hive 是一个极其强大和有前途的 NoSQL 数据库。它兼容所有平台，包括 **web** 。我没有第一手的知识，但是快速搜索发现读写速度的基准测试令人印象深刻。它有一个强大的内置加密。把这看作一个**地图**，其中你的对象被存储为**键值对**。

因为是 **NoSQL** 数据库，所以用*【盒子】*(种)代替了*【表格】*。因此，您的数据被组织在这些*框*中。因为 NoSQL 适应性很强，你可以为每个值定义任何类型的结构。因此，*框*的存在并不意味着**一致数据模型**的存在。如果您的应用程序需要**灵活的**数据列用于相同类型的实体，这将是一个显著的优势。

在使用盒子之前，您必须首先**打开**它，以便将数据从**本地存储器**加载到**存储器**中，以便即时访问。因此，您可以在不使用**‘await’，**的情况下进行查询，并且在您的**小部件**的**构建**方法中使用它将非常简单。如果不需要立即访问，您可以随时使用 *lazybox* 。

上面可以看到如何用**蜂巢**做一个*盒子*。不难理解。 **Hive** 为**所有原语类型**提供基本支持，但大多数时候你要存储的是一个**实体**或**实体**的子集。为此，您必须首先创建一个**类型适配器**。这里有一个例子:

将 *HiveObjects* 视为*实体*。虽然，在这种情况下，你可以扩展 ***乘积*** 并存储在同一个*盒子*中。这里有一个如何使用 ***产品*** 类的例子。

**Hive** ，在我看来，对于**小规模灵活**的应用来说是理想的。学习简单，适应变化。我很高兴能把这个用在副业项目上。

## 森巴斯特

**Sembast** 是另一个 **NoSQL** 数据库，用于颤振(和飞镖)应用，它支持所有可能的平台，包括 **web** (通过 *sembast web 包*)。Sembast 由于其有前途的特性而在这个列表中，但我不相信它还在那里。它以类似于 **Hive** 的方式管理数据库，但是有一些不同。我没有看到对**实体**的任何支持，我认为这在数据模式可读性方面是有益的。你仍然可以使用你自己的类型，但是它们必须正确地被 **JSON 编码/解码**。

要使用数据库，必须用**指定文件的路径。db** 扩展名。该文件将用于所有数据库操作，并将根据需要进行更新。如果您不想使用该选项，您仍然可以将 **Sembast** 与 [*sqflite*](https://pub.dev/packages/sembast_sqflite) 一起使用。

以上，你可以看到如何**保存和读取记录**。该 API 很容易学习，但我更喜欢 Hive 语法而不是 Sembast，因为它消除了读取数据时对**‘await’**的需要。然而，你仍然可以探索森巴斯特。值得注意的是，Sembast 支持**【触发器】****【数据加密】。**这两个有用的特性可以帮助提高数据**的安全性**和**的一致性**。

## [**奖励解决方案:共享偏好**](https://pub.dev/packages/shared_preferences)

如果你的应用不是**数据关键型**，你就不需要花很多时间去学习额外的库。**共享偏好**利用**平台特定的存储 API**来存储和读取**键值对**。因为数据可以异步保存到磁盘，所以这个插件不应该用来存储关键数据。

正如你所看到的，使用插件简单明了。

## 关系数据库或 NoSQL

我觉得有义务解释一下**关系数据库管理系统**和 **NoSQL** 解决方案之间的区别。都有优缺点，但这不是重点。因为我们不能说一个比另一个好。这一切都归结于你的需要。

**关系数据库管理系统:**

*   数据**一致性**
*   数据模式**不太可能显著改变**
*   存储**实际**和**数值**数据

NoSQL:

*   **庞大的**金额和**凌乱的**数据
*   **灵活的**模式定义，**实时的**数据，更容易**缩放**
*   **没有联接**，查询速度更快，但数据重复更多

**这些是两个数据库系统的关键特征。当使用本地数据库进行 flutter 开发时，您应该彻底了解您的应用程序的数据需求。**

**如果你正在开发一个既有数字产品又有实体产品的商店应用程序，这些产品可能会有**多种多样的特性**。即使是同一类别的产品也可以有**不同的特征**。在这种情况下，你需要一个 **NoSQL** 数据库，或者你会得到一堆**可空的**列。**

**考虑另一个示例应用，例如加密货币投资组合应用。自然，你的 app 会依赖**第三方 API**。这些 API 经常会发生变化。不用每次都改变你的模式，你可以使用 NoSQL 数据库，它比关系数据库更容易适应变化。我相信你明白这一点，但你可以阅读更多关于该主题的帖子，以帮助你为未来的项目做出更好的决定。**

## **结论**

**我试图简化颤振开发中最流行的本地数据库解决方案的基础。这些都是了不起的计划，背后都有聪明的头脑。尝试通过**给他们星星**或**贡献给他们的仓库**来帮助他们。我希望这篇文章对你决定下一个数据库解决方案有用。**

**最后一个想法。我很清楚**领域**和 **Isar** 数据库，我知道它们正在崛起。这里没有列出它们，因为它们最近才发布了 alpha 版本。**

**谢谢你的宝贵时间。**