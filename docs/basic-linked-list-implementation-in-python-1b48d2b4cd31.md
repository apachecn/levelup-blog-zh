# Python 中基本链表的实现

> 原文：<https://levelup.gitconnected.com/basic-linked-list-implementation-in-python-1b48d2b4cd31>

![](img/b7acdf9c09784f3b5bfd0c36da19c930.png)

照片由[郭佳欣·阿维蒂西安](https://unsplash.com/@kar111?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 什么是链表？

链表是一个项目序列，其中每个项目指向列表中的下一个项目。与常规的 Python 列表不同，链表中的项目(节点)在内存中不必相邻。列表中的每个节点都由数据和指向下一个节点的指针组成。记住这一点，我们将从节点类开始。

# 节点类

这里我们创建了节点类。在 **__init__** 方法中，我们传递想要用来初始化节点的数据。我们还将节点的 next 设置为默认值 None。我们这样做是因为一旦我们点击了下一个没有任何内容的节点，我们就知道我们已经点击了列表的末尾。这就是我们这节课所需要的。接下来，我们将学习链表类。

# 链表类

现在我们创建 LinkedList 类。在 **__init__** 方法中，我们将头部和尾部设置为 None。这确保我们从一个空的链表开始。链表的头是一个非常重要的属性。没有头，我们就无法得到名单的其余部分。

# 附加

我们要添加的下一个方法是 **append** 方法，它将一个项目添加到列表的末尾。这里我们将开始使用我们上面定义的节点类。

append 方法只接受 1 个参数，这是我们想要添加到列表中的项目。然后，我们用传入的项目创建一个新节点。现在我们有了一个新节点，它的数据是我们想要添加到列表中的条目。接下来，我们检查头部是否为空，如果是，我们将头部设置为新创建的节点。如果头部不为空，我们将尾部的 next 设置为新节点。在这两种情况下，我们都将新节点设置为尾部，因为我们添加到列表末尾的任何节点现在都将是尾部。

现在代码应该是这样的:

# 前置

接下来我们将添加 **prepend** 方法。这将在列表的开头添加一个项目。

就像 append 一样，prepend 接受我们想要添加到列表中的项目作为参数。我们再次创建一个新的节点，并检查头部是否为 None。如果是，我们将该节点设置为尾部，如果不是，我们将新创建的节点的 next 设置为头部，因为我们将添加到列表的开头。在这两种情况下，我们现在都将头部设置为新节点

在 append 和 prepend 中，如果 head 是 None，我们将新节点设置为 head 和 tail。这是因为当标题为 None 时，意味着列表中没有项目。然后我们添加一个条目，因为它是列表中唯一的条目，所以它既是列表的开始也是列表的结尾。

现在代码应该是这样的:

现在我们已经有了添加到列表中的方法，让我们创建一个从列表中删除的方法。

delete 方法接受要删除的项作为参数。我们首先检查头部是否没有。如果是，我们立即返回，因为列表中没有要删除的内容。如果不是，我们继续检查头节点的数据是否是我们想要删除的项目。如果它们匹配，我们将当前头的 next 设置为新头。如果它们不匹配，我们需要开始遍历整个列表来找到这个项目。

我们需要一种方法来跟踪我们当前正在检查的节点，所以我们设置了一个变量 **current** 来为我们做这件事。我们需要头部来访问整个列表，所以我们将**当前**初始化为头部。现在我们循环直到当前节点的下一个是 None，所以当我们到达列表的末尾时我们将停止循环。

随着循环的每次迭代，我们检查当前节点的下一个节点是否有我们想要删除的数据。如果是，我们将当前节点的 next 设置为下一个节点的 next。这意味着，如果我们在列表中有 3 个项目，我们想删除第二个项目，我们会让项目 1 现在指向项目 3，而不是项目 2，因为项目 2 的下一个将是项目 3。

现在代码应该是这样的:

# 清点物品

我们现在有了在列表中添加和删除条目的方法，但是我们怎么知道列表中有多少条目呢？让我们添加一个**长度**方法来做到这一点。

length 方法没有参数。在内部，我们初始化一个**计数**和**当前**变量，以跟踪我们计数了多少个节点，以及我们当前在哪个节点上。然后我们循环，直到到达列表的末尾，并为循环的每次迭代增加 1。

就是这样。现在我们完成了链表的基本实现。现在我们有了在列表中添加、删除和计数条目的方法。完成的代码现在应该如下所示:

[](https://skilled.dev/course/linked-lists) [## 链表| Skilled.dev

### 链表是一种简单、轻量、灵活的低级数据结构。它们通常用于…

技术开发](https://skilled.dev/course/linked-lists)