# 图灵完备在编程中到底意味着什么

> 原文：<https://levelup.gitconnected.com/what-turing-complete-exactly-means-in-programming-d12e64edb6f9>

## 对概念的探究

![](img/c7ac9bd13ee54b435df4ae7eb8a323e1.png)

照片由[黑脸田鸡岛崎](https://www.pexels.com/photo/serious-ethic-businessman-working-on-laptop-5668870/)拍摄

图灵完全性是计算机科学中一些算法的属性，这意味着它们总是有一组有限的步骤要执行，可以产生算法的解决方案。

这个概念是由艾伦·图灵在 1936 年作为他的论文的一部分[首次提出的。](http://www.cs.virginia.edu/~robins/Turing_Paper_1936.pdf)

从那以后，这个术语在计算机工程和理论计算机科学等领域被广泛使用；它还用于这些字段认为不可计算的算法。

# 科学理解图灵完备性

1936 年，艾伦·图灵考虑了一个问题，即一个函数有一个答案意味着什么。他感兴趣的是确定形式系统的特征，这些特征是必要的，如果它们是为了计算可以由特定种类的数学算法回答的问题的解决方案。

他的著作《论可计算数》描述了形式系统的几个特征，并描述了一些他认为是可计算的函数。在下一节中，给出了一些传统的和现代的可计算性概念。

图灵论文的标题描述表明，他谈论的是机器(通用计算机)的可计算性，而不是人类的可计算性。

本文没有区分算法和程序的概念:前一个概念只是随着高级编程语言的出现才变得普遍。

# 图灵机

图灵机实际上是一种编程设置。图灵的定义受到了很多讨论，许多人认为图灵机的技术困难会使其实际实现(如在艾伦·图灵的时代)不可能或不切实际。

然而，仍有许多问题需要计算机来解决，而不是由人来手工解决。

图灵将算法定义为保证终止的过程。图灵机是自动机(计算机器)的一种形式，它可以从磁带中读取指令，并在磁带中来回移动以执行指令。

指令用“代码”(符号)写在磁带上。当图灵机读取到一个告诉它停止的指令并输出它已经获得的任何部分结果时，它就会停止。

换句话说，它旨在用于解决一些问题，这些问题的最佳解决方案可以通过算法立即计算出来，但是这些问题过于复杂，无法通过图灵机计算的公式(即答案可以写成公式)来描述。

# 编程中的应用

这种差异的一个简单例子是数学函数，如加法或乘法。当详细写出时，这些函数就变成了相当复杂的公式(表达式),有许多变量和常数。

然而，由于数学函数是由公式定义的，因此可以将其写为计算机程序中的一组指令，该计算机程序可以用作在任何图灵机上运行的“程序”(即程序)。这就是为什么这些函数有时被称为“递归可枚举的”。

作为这种差异的一个例子，生命的组合游戏的一般解是一个 NP-完全问题(相比之下，这个游戏的解不能用算法来描述)。

也就是说，没有已知的公式或算法可以根据当前状态及其先前状态来确定游戏的下一个状态。但是，可以使用图灵机模拟初始条件，然后计算下一个状态。

另一方面，如果我们正在考虑一个解决特定问题的算法(例如，在一对字符串中寻找模式)，它不一定是递归的或图灵完全的。

一个简单的例子是用数字表示字母。在两个字符串中搜索模式的一个有效(但简单)的算法是在第一个字符串中搜索模式，然后在第二个字符串中搜索，并继续这个过程，直到找到它或搜索失败。这在计算上是低效的，但是它仍然可以用来在一组字符串中寻找模式。

计算的图灵概念也关注机器，而不仅仅是算法。可计算性的概念与图灵机的过程有关，该过程指定了得出答案所需的步骤，而计算机程序允许人类可以采取任何一组内部步骤。