# 设计 Cassandra 数据模型 101

> 原文：<https://levelup.gitconnected.com/designing-cassandra-data-models-101-27bce86a014d>

![](img/e299524ea7526ff26dc544ed51b8bb04.png)

照片由 [Sidorova Alice](https://unsplash.com/@sesambrotchen?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

如果您来自关系数据库背景，在 Cassandra 中设计数据模型可能会很棘手。尽管 Cassandra 在术语方面尽力与关系数据库相提并论，但我觉得它变得更具误导性。当然，CQL (Cassandra 查询语言)与 SQL 如此相似也于事无补。

从根本上说，Cassandra(一个 NoSQL 数据库)和其他关系数据库(MySQL，PostgreSQL)是非常不同的。 **Cassandra 不是关系数据库的替代品。你必须用完全不同的思维方式来设计你的模式。**

为了让您开始设计 Cassandra 数据模型，我将回顾一下从关系背景迁移到 Cassandra 时学到的一些基础知识。

# 分区键是基础

理解分区是 Cassandra 的基础。分区是 Cassandra 存储数据的基本单位。在设计模式时定义分区键(简单的或复合的)。Cassandra 使用您的 keyspace 的分区键来决定您的数据驻留在哪个节点。

具有相同分区键的记录在同一个分区中结束。一个分区驻留在一台主机中。谈到分区，有四点需要考虑:

*   最大分区大小应该是 100MB，理想情况下小于 10MB
*   理想情况下，一个查询从单个分区获取数据
*   所有分区的大小应该大致相等，以避免偏斜和热点
*   分区键不应该产生无限增长的无限分区久而久之

必须仔细设计 Cassandra 分区，以获得最佳的 I/O 性能，包括读取和写入。保持分区小也有助于 Cassandra 的内存使用、修复和墓碑驱逐。

# 聚集列很重要

聚类分析列是主键中不属于分区键的字段。**它们决定行在给定分区中的排列顺序。**

如果您注意通常查询数据的排序顺序，可以在设计时定义聚类分析列的顺序。假设您正在为用户信息设计一个数据模型，并且您的表是按部门划分的。还有，有人加入的那一天(`recently_joined`)是聚类栏。现在想象一下，您有一个常见的查询，要查找给定部门中最近加入的人。在这种情况下，您可以按降序对`recently_joined`聚类列进行排序。这样，当查询 Cassandra 时，您可以通过执行分片顺序读取来获得最佳性能。

顺序读取总是更快。相对于查询对集群列进行排序将使顺序读取在您的键空间中变得常见，这正是您想要的。

# 数据的反规范化和复制

在计算机科学中，我们到处都学到了 DRY(不要重复)。谈到代码，我们总是尽量不重复功能和业务逻辑。当涉及到关系数据库时，我们总是试图规范化数据并使用外键连接表。

**在卡珊德拉，复制和反规范化数据是被鼓励的。**否则，您的查询几乎永远不会有好的性能。分区键和聚集列的工作方式，查询的性能很大程度上取决于数据在 Cassandra 中的布局。您可能已经用一组特定的查询设计了它，但是需求一直在变化。现在您可能有了对您的表来说次优的新查询。在这种情况下，总是可以在一个新的表中复制数据，只是以不同的方式来满足新的查询。

**卡珊德拉没有关系数据库那样的连接概念。在像 Cassandra 这样的分布式数据库中，可靠地进行跨节点连接是不可能的。因此，我们鼓励您复制数据，并根据不同的业务需求进行不同的分区，而不是连接。**

与内存和 CPU 相比，磁盘空间通常是最便宜的资源。Cassandra 就是围绕这个假设设计的。

# 围绕您的查询建模

我已经多次提到了这一点，但是为了更好地理解这一点，**您的模型是由您的查询需求决定的。**

如果你来自一个关系背景，这可能是违反直觉的。在那里，我们习惯于基于类、对象和实体来设计模型。之后，我们可以通过连接和其他复杂的子句获得任何想要的数据。

在 Cassandra 中，你希望你的查询非常简单。这就是为什么您希望您的模型围绕您的查询来设计。

如果您的查询发生变化，会发生什么？您复制了另一个表中的数据，并在此基础上创建了新的查询。这看起来开销很大，但是如果您已经用 Cassandra connectors 和消息代理(比如 Kafka)建立了基础设施，那么用另一个表中的数据创建一个新表就相对简单了。

# 写比读便宜

在 Cassandra 中，写要比读便宜得多。

在高层次上，当你给卡珊德拉写信时，会发生两件事:

*   该节点将记录写入仅附加提交日志
*   该节点将您的记录写入内存中的数据结构，称为 MemTable
*   节点会确认您的写入

磁盘不是直接涉及的，所以在 Cassandra 中写作非常便宜。这就是为什么 Cassandra 是写密集型应用程序的绝佳选择。各种写操作的效率都差不多。

然而，正如您在本文中看到的，在阅读时，您的数据必须以正确的方式排列。否则，Cassandra 需要扫描多个分区进行读取，这意味着扫描多个主机上的数据。它会很快变得昂贵。

在 Cassandra 中设计数据模型明显不同于其他数据库，尤其是关系数据库。您真的需要在数据模型背后进行一些思考，记住您的查询。然而，如果您正确地设计模式，您可以获得惊人的 I/O 性能。