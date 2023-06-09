# 关系数据库索引以及何时使用它们

> 原文：<https://levelup.gitconnected.com/relational-database-indexes-and-when-to-use-them-fb2104cf7af4>

![](img/0f267c9b84028581bb0389664f2a6be5.png)

关系数据库索引可以大大提高数据库的查询速度。然而，使用它们是有代价的——让我们深入探讨一下！

## 什么是指数？

索引是一种数据结构，它包含数据库表中一列(或多列，稍后将详细介绍)的副本，排序该副本是为了提高对表中原始列的数据库检索操作的速度。索引还在每个复制的行上包含一个“键”，它指向表的列中的原始数据行。创建索引的代价是额外的*写操作*和存储空间。

## 什么时候应该使用索引？

当数据库执行的*读*操作多于*写*操作时，索引最有用。让我们假设我们正在建立一个类似于 IMDB 的网站。我们的数据库有许多表，包括一个`movies`表。我们的`movies`表有`title`、`genre`、`rating`和`release_date`列。虽然 IMDB 非常频繁地向他们的`movies`表中添加(或*写*电影，但我敢打赌用户在网站上搜索`movies`的次数要多得多。

由于对我们的`movies`表的数据检索操作是最常见的操作，我们将很好地为最常查询的列添加索引。让我们给`title`列添加一个索引，因为这是`movies`表中最常见的查找。我们将按字母顺序对新创建的索引进行排序。因此，我们的新索引实际上是按字母顺序排列的`title`列的副本，并带有指向表中每个无序标题的原始行的指针。现在，当用户根据电影名搜索电影时，可以更快地找到它，因为数据库更好地知道在哪里搜索它。

## 什么时候应该使用索引？

如前所述，索引是以数据库中额外的写操作和存储空间为代价的。让我们考虑另一个使用 [IMDB](https://www.imdb.com/) 的例子，但是这次让我们使用数据库中的`reviews`表，并假设它有`content`、`rating`和`movie_id`的列。IMDB 本身并没有给用户提供搜索电影评论的能力。在`reviews`台上执行的主要操作是*写入。*新的行不断被写入表中，所以我们希望这个动作尽可能高效。

假设我们向我们的`rating`列添加了一个索引。现在，每次创建新的评论时，`rating`都会被复制并以正确的顺序插入到排序后的索引中，并被赋予一个键。这给我们的操作增加了额外的时间，消耗了额外的内存——而且没有任何理由，因为我们甚至没有为用户提供一种基于他们的评级来搜索评论的方法。

**TLDR；如果您的表列更多地用于*写*的操作，而不是*读*的操作，那么您可能不需要索引，反之亦然。**

## 为多列创建索引

可以为多个数据库列创建一个索引，列的顺序非常重要。让我们在这个例子中再次使用`movies`表，并假设我们有一个针对`director_id`的附加列。我们正在我们的网站上实现一项新功能，允许用户使用导演的名字搜索电影，并按时间顺序返回电影结果。因此，为了提高数据库性能，我们将使用`director_id`和`release_date`列创建一个新的索引。现在，为了更快地查找，将对导演进行排序，并对每个导演的发布日期进行排序。

如果我们首先用`release_date`创建了索引，那么它几乎没有用，因为每个`release_date`可能有多个`director_id`与之相关联。我们必须搜索每一个`release_date`来寻找相应的`director_id`。

## 索引如何提高性能

如果我们考虑在未排序的列上进行正常的数据库条目查找，那么 [Big-0](https://www.bigocheatsheet.com/) 时间复杂度将是线性的，或者是 0( *n* )。这是因为我们的最坏情况是我们必须搜索每一行，并且对于每一个添加的行，最坏情况下的查找时间以线性方式增加。

当创建了一个索引，并且从未排序的列创建了一个排序的列时，我们的查找时间在最坏的情况下会减少到 0( *log(n)* )。这是因为关系数据库索引被构造成平衡树，或 [B 树](https://use-the-index-luke.com/sql/anatomy/the-tree)。B 树如何构造的确切复杂性取决于数据库(PostgreSQL、MySQL、SQLite)。这里的关键是要认识到，我们基本上能够对时间复杂度为 0( *log(n)* )而不是 0( *n* )的列执行查找，这将提高性能。