# 如何用 Python 求解和创建数独网格

> 原文：<https://levelup.gitconnected.com/how-to-solve-and-create-sudoku-grids-in-python-ee2b05d9298e>

## 使用递归进行回溯

![](img/eda975f010eb334959459a8c9db27768.png)

约翰·摩根在 Unsplash[拍摄的照片](https://unsplash.com/s/photos/sudoku?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我试图解决的问题是什么？这就是我这么做的原因:因为我开始使用在线服务生成的网格创建一本数独书(关于 KDP ),并通过 React 生成 PDF。我女儿过来对我说:“爸爸，爸爸！其实在这个格子里，有两种可能！”所以我想确认我没有犯错误，我的东西工作正常。这就是为什么我编写了这个程序来做这个测试。所有这一切的好处是，如果你知道如何用 python 解决数独，你也知道如何生成它。

代码相对简单，使用了四个函数:第一个函数读取数据并创建网格，第二个函数寻找正方形的可能性，第三个函数求解，第一个函数完成网格的简单解析，第四个函数完成网格的完整解析。

# 使用 createGrid 创建网格

网格是如何构造的？首先，我们读取现有数据，然后创建一个数组，实际上是数组的数组。在每一个小表格中，有九个数字，这九个数字可以在 0 到 9 之间，0 表示一个空的单元格，数字 1 到 9 表示已经填充的单元格。

# 用 getPossibilities 检索单元格的可能性

在这个数字 0，9 的数组中，我们将创建一个名为`getPossibilities`的函数。该函数将返回一个单元格在当前网格状态下所有可能性的数组。如果单元格不为空，唯一的可能是已经填入的数字，所以我们返回一个只包含该数字的数组。如果单元格当前为 0，我们将查看同一行、列或 3x3 单元格中的所有数字(大于 0)，并将它们列在一个数组中。
然后，我们从 1 到 9 进行迭代，以找到不包含在现有号码表中的号码集，因此这些号码可能是这种情况的候选号码。然后，该函数将返回一个数组，该数组可以没有元素(如果网格中有错误)，只有一个元素(因此是正方形的正确元素)，或者有几个元素。

getPossibilities 函数

# 使用 simpleSolve 的第一个简单解析

如其名称所示，simpleSolve 函数将执行基本解析。这个基本的解决方案从制作数组的深层副本开始，以便不改变作为参数接收的数组。然后，该函数对所有单元格进行迭代。对于网格中包含 0 的每个单元格，它调用`getPossibilities`来获取该单元格的可能性。那么有三种可能的结果。首先，一个单元格中只有一种可能性:在这种情况下，函数将在单元格中填充这种可能性(这也是为什么我们在开始时做了深度复制)。第二，没有可能:在这种情况下，函数返回一个错误。第三，有几种可能性:在这种情况下，该函数增加一个计数器，该计数器用于测量网格中剩余的 0 的数量。一旦函数遍历了所有单元格，就会发生以下两种情况之一。要么我们已经找到了新的值，但网格中仍然有 0，在这种情况下，我们通过重置 0 的计数器来开始新的循环。或者，没有(或没有更多的)替换，或者网格中没有剩余的 0，在这种情况下，该函数已经达到了它所能做的极限。(如果没有更多的 0，网格已经解决了。)因此，该函数返回它对网格成功完成的操作，以及剩余的 0 的数量。

简单求解函数

# solveGrid 的完全求解

`solveGrid` 函数将通过在网格上运行`simpleSolve`来启动，这样做还有一个额外的好处，那就是制作网格的深层副本。如果`simpleSolve`没有解决网格，也就是说，如果它返回一个剩下 0 的网格，这意味着有几个可能的单元格。那我们该怎么办？我们尝试了不同的可能性。我们选择具有几种可能性的单元(例如，具有最少数量的不同可能性的单元之一)。然后我们创建网格的几个副本，每个副本代表一种可能性。在这些网格中，我们应用了每一种可能性。好像新的现实正在被创造。就像在量子力学中，就像薛定谔的猫，我们创造了一个现实的变体，我们说:“这个细胞现在有这种可能性”。

我们用这些网格做什么？我们做一个递归:我们让`solveGrid`用新的网格来称呼自己。从`simpleSolve`开始，这些新的执行将把上面描述的一切应用于每个网格变体。如果该函数仍然找到有几种可能性的单元格，它将自己重新启动不同的分辨率。这一过程将会展开，并将产生分支，分支的分支，就像一棵树，探索不同可能性的可行性。

在这些分支中，可能会发生几种情况。最简单的情况是以一个没有可能性的细胞结束。在这种情况下，分支是不可行的:我们把它放在一边，它只会返回一个空数组。另一方面，也有可能得到一个有效的解，一个没有任何 0 的已解网格。在这种情况下，该函数返回包含解决方案的数组。

现在，让我们回到创建几个分支的函数的上下文。每个分支，每次执行都返回一个包含找到的解的数组。此时，该函数连接这些数组，并将它们返回到它们的父数组，只要该有效网格数组具有 0 或 1 个元素，这就是解决方案如何在可能性树上向上移动的方式。如果数组有两个或更多的解，该函数将创建一个错误，因为两个有效网格的存在意味着父网格是错误的。

在第一次执行我的`solveGrid`函数的情况下，有三种可能的结果，这取决于找到的解决方案网格的数量。如果有多个解决方案，则网格包含的信息不足以解决问题。如果找不到解决方案，网格将被破坏。如果只找到一个解决方案，则网格有效。

solveGrid 函数

# 更进一步

这种递归回溯系统不仅允许我们检查网格是否有效，还允许我们通过测量需要多少级递归来测量网格的难度，因为每一级意味着网格涉及另一个不明显的单元。
另外，同样的代码还允许我们生成有效的网格。给定一组初始数字(随机放置或手动放置)，我们可以调用`solveGrid`函数并选择一个只返回一个解的分支。并且我们可以选择递归树的深度级别来校准难度。

完整代码可以在这里找到:[https://gist . github . com/Gosev/ce 3 defb 6415 b 67 EC 03 f 48 fa 11 fc 158 f 0](https://gist.github.com/Gosev/ce3defb6415b67ec03f48fa11fc158f0)

玩得开心！