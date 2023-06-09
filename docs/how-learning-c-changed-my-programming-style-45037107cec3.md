# 学习 C++如何改变我的编程风格

> 原文：<https://levelup.gitconnected.com/how-learning-c-changed-my-programming-style-45037107cec3>

我的旅程以及为什么软件开发人员应该学习它

![](img/32c13b1af534790422500a2a5d6c8cb2.png)

蒂姆·高在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

人们说学习 C 或 C++是每个编程学生最糟糕的噩梦。如果你之前没有任何低级知识，开始时确实会很混乱。

根据 [2021 年堆栈溢出调查](https://insights.stackoverflow.com/survey/2021#most-popular-technologies-language)，尽管有些人这么说，C++绝对没有过时，因为它仍然被大约 25%的开发人员用于各种各样的领域，如编译器、虚拟机、人工智能和游戏引擎。

然而，大多数程序员倾向于远离它，因为它可能相当吓人，尤其是因为它臭名昭著的易出错的内存管理系统。相反，我建议每个软件开发人员都应该学习 C++作为他们工具箱的一部分。让我告诉你为什么。

## 我在 C++之前的背景

我开始在 Arduino 板上编程，用 C++编写简单的程序。然而，我只是在做初级水平的项目，甚至不知道(或不需要知道)像指针或内存这样的核心概念。

直到我开始用 Python 编程，我才真正开始理解基础——数据结构和算法、设计模式、OOP——并欣赏编程。我还学习了一些 Java 和 Dart/Flutter 用于移动开发，但我从未接手过任何复杂的项目。

## 我如何开始使用 C++

在编程的最初几年里，我从未接触过低级语言和概念，直到我对人工智能着迷。在这一点上，我决定做我编程历史上最愚蠢的事情，用 C++从头开始开发一个神经网络训练框架，尽管我不知道神经网络如何工作，也没有编写 C++代码的经验。

经过几个月的研究和努力工作，我最终未能完成我的项目。然而，在这个过程中，我学到了很多关于人工智能和 C++的知识。

我知道这种一头扎进这些硬领域——c++和神经网络——肯定不是最明智的举动，但它仍然让我对这些主题进行了大量研究，并让我获得了可能不会发展的新技能。

## C++如何改变了我的编程风格

来自更高级的语言背景，我不太习惯编写高效和优化的代码。通过我的 C++学习过程，我开始在写代码的时候更像计算机一样思考。

在我第二次深入一个复杂的 C++项目——从头开始构建编译器和虚拟机——的过程中，我学到了更多更高级的语言特性，如模板、常量表达式、移动语义……我还必须从头实现许多常见的数据结构，如链表和树，并开始使用原始二进制数据来处理虚拟机的内存和编译器生成的二进制文件。

此外，学习如何管理内存和数据如何存储在 RAM 中让我在使用资源密集型但常见的数据结构(如字符串和复杂对象)时三思。除此之外，我开始使用适当的数字数据类型，而不是到处扔`int` s。例如，您不会将人的年龄存储在一个`int`中，它可以表示介于-2，147，483，648 和 2，147，483，647 之间的数字。一个 1 字节的数据类型(`unsigned char`、`byte`、`u8`)可以存储 0 到 255 之间的值，除了更节省空间之外，还能很好地完成这项工作。

另一个重要的经验是基于索引的[查找表](https://en.wikipedia.org/wiki/Lookup_table)或[哈希表](https://en.wikipedia.org/wiki/Hash_table)的好处，而不是必须多次执行资源密集型运行时计算。

## 一种新的学习方法

对于你在底层世界所学到的一切——无论是一个错误、一个新的数据结构或概念、优化技术——你都会看到许多新的路径，这些路径反过来会导致兔子洞更深。

这种学习方法是递归的，因为每一步都要求你(或导致)对主题做更多的研究，因为你错过了一些需要额外知识的重要拼图。

这种方法效果的一个明显例子是我的编译器之旅。首先，我需要理解编译的各个阶段:标记化、语法分析、中间代码生成和可执行输出。后者让我了解了汇编语言以及它们是如何工作的，这反过来又让我去研究 CPU 是如何工作的。这一步对于构建我的虚拟机也是至关重要的，这也需要弄清楚内存是如何工作的，以及最终的系统中断。

如你所见，这是一个永无止境的低级兔子洞之旅。然而，这种方法不仅适用于编程，也适用于生活中的其他事情:如果你想真正学到东西，你最好把它分成几部分，深入研究每一部分。

## 结论

虽然许多开发人员倾向于远离学习 C++，要么是因为他们被其臭名昭著的困难所吓倒，要么是因为他们认为他们永远不会需要它。然而，我强烈建议您尝试一下，因为这将帮助您更加了解您日常使用的技术是如何工作的。了解您的工具是掌握它们、利用它们的优点、避免它们的缺点的第一步。

除此之外，了解像 C++这样的语言确实有助于您学习其他语言，因为它们可能共享许多类似的概念，如内存地址和指针、类型泛型、OOP 等等，更不用说大多数现代语言更容易掌握了。

> 开始就努力工作，然后一切都会变得容易。

我希望你喜欢这篇文章。如果你有什么要补充的，请在评论中分享你的想法。**感谢阅读！**

如果你是一个对提高程序性能感兴趣的 Python 开发者，我建议你看看下面这个故事:

[](https://betterprogramming.pub/speed-up-your-python-codebases-with-c-extensions-94859875eb70) [## 用 C 扩展加速你的 Python 代码库

### 给你的 Python 程序带来 C 语言的速度

better 编程. pub](https://betterprogramming.pub/speed-up-your-python-codebases-with-c-extensions-94859875eb70)