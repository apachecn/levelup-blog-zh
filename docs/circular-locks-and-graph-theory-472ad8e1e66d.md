# 圆形锁和图论

> 原文：<https://levelup.gitconnected.com/circular-locks-and-graph-theory-472ad8e1e66d>

![](img/5aa47594949f861b58ac33e3de0ea276.png)

*这篇短文将探讨在编码面试中，图论算法如何出现在看似不相关的问题中。*

*随意探索* [*往期*](/arbitrage-and-graph-theory-ecd26391908b) [*帖子*](https://cppcodingzen.medium.com/cycles-in-directed-graphs-in-unexpected-places-c5306460b60e) *阅读更多涉及图算法的问题(及其解答)*

# 问题:

给你一个有三个轮子的圆形锁，每个轮子都按顺序显示数字`0`到`9`。这些轮子中的每一个都顺时针和逆时针旋转。

此外，锁有一定数量的“死胡同”，这意味着如果你把轮子转到这些组合中的一个，锁就会卡在那个状态，无法打开。

让我们把“移动”看作是单个轮子在任一方向上转动一个数字。给定一个初始设置为`000`的锁、一个目标组合和一个死胡同列表，编写一个函数，返回达到目标状态所需的最少移动次数，如果不可能，则编写`-1`。

# 解决方案:

这个问题有一个基于图算法的显而易见的解决方案——只要你正确地表述它。这里有一种表达算法的方法:

1.  每个锁的组合，就像`{1, 2, 3}`一样，构成了图形的一个节点。
2.  一位数不同的组合形成图的相邻节点(并通过边连接)(例如`{1, 2, 3}`的邻居是`{0, 2, 3}, {2, 2, 3}, {1, 1, 3}, {1, 3, 3}, {1, 2, 2}, {1, 2, 4}`)。
3.  “死胡同”在图中根本不存在，没有边进出它们！
4.  寻找最少移动次数的问题归结为寻找这个图中的最短路径！它可以使用标准的图形算法来解决，如*广度优先搜索(BFS)* ！

在实现 BFS 算法之前，让我们先做一些准备:我们将定义数据结构来表示一个密码锁。我们将使用一个三元素数组`std::array<int, 3>`来完成这个任务。此外，

1.  我们将定义一个`unordered_set`锁组合来存储访问过的锁组合。为了定义集合，我们需要在`std::array`上定义一个哈希函数。我们的散列函数将简单地把数组转换成一个三位数的整数(`arr[0] * 100 + arr[1] * 10 + arr[2]`)。
2.  最后，我们需要定义一个队列类型来保持一对锁的组合和步数(int): `std::queue<std::pair<std::array<int, 3>, int>>`。

我们现在准备实现我们主要的*广度优先搜索(BFS)* 算法，系统地迭代不同的锁组合，找到从初始组合`{0, 0, 0}`到目标组合的最短路径。

1.  我们将初始节点`{0, 0, 0}`插入到 BFS *队列中。*我们还插入`0`来表示达到初始状态所需的最少移动次数。
2.  在每次迭代中，我们弹出队列的最前面。我们计算队列前面的*有效*邻居。有效邻居被定义为先前没有被访问过并且不是死角的邻居节点。
3.  我们将步数加 1，并将每个有效的邻居连同这个步数一起插入 BSF 队列。
4.  一旦到达目标节点，我们就返回步数。如果我们清空 BFS 队列，并且从未到达目标节点，我们返回-1，表示目标节点不可到达。

下面是使用上面定义的数据结构的 C++实现:

# 测试:

下面是一些可以尝试的测试案例:

1.  “不可能”的目的地，即所有路径都通向死胡同的目的地
2.  没有死角
3.  死胡同/目的地的复杂组合。

*原载于* [*https://This。com*](https://cppcodingzen.com/?p=3202)*2021 年 7 月 15 日。*