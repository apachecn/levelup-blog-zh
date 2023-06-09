# 当注释是脚手架时，它们不应该是永久的

> 原文：<https://levelup.gitconnected.com/when-comments-are-scaffolding-they-should-not-be-permanent-433f80927a2d>

![](img/6cdff77487ffb9edce5cce47a4350083.png)

[迪安·布瑞尔利](https://unsplash.com/@milkandbourbons?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在建筑过程中，工人们需要脚手架来帮助他们接近建筑物的较高部分。施工结束后，工人们拆除脚手架。

计算机程序中的注释也有类似的作用。但是不像花费一千美元的搭建，似乎没有太多的动机从一个完成的程序中删除注释。

脚手架可以被带到不同的建筑工地。注释通常不能以任何有意义的方式移植到不同的程序中。

正如我之前提到的，对评论的普遍看法赋予了它们一定程度的持久性。但事实是，如果它不是一个许可证头，也不是一个文档生成工具，注释肯定会失去它的用处。

当一个评论不再有用时，它应该被删除，而不是被保留。一个过时的评论可能会适得其反，让团队成员和评审者感到困惑。

充其量，支架注释只是变得多余。

在这种情况下，显而易见，注释可以简单地删除，因为它们的含义在子例程的名称中重复了。

其他时候，可能不清楚需要做什么。例如当将数学公式放入注释中时。

```
 // Kinetic energy formula:
    // k = 1/2 mv^2, where k is kinetic energy,
    // m is mass and v is velocity
    double m = obj.getMass();
    double v = obj.getVelocity();
    double k = 0.5 * m * v * v;
```

我认为这里需要进行的重构是，单字母变量名应该由单词名代替。

```
 // Kinetic energy formula:
    // k = 1/2 mv^2, where k is kinetic energy,
    // m is mass and v is velocity
    double mass = obj.getMass();
    double velocity = obj.getVelocity();
    double kineticEnergy 
            = 0.5 * mass * velocity * velocity;
```

或者将 *m* 和 *v* 变量保留为`m`和`v`就足够了。不管怎样，解释这是动能公式的评论现在变得没有必要了，可以安全地删除了。

那个评论本质上是一个脚手架评论。程序员把数学公式记下来是有意义的，这样以后就不用再去查了。

你们中的一些人可能会对 Java 中的`^`操作符做了一些数学家不希望它做的事情感到恼火。评论不是抱怨的合适地方。

我在评论中看到过这种事情，指出你必须以某种方式做某事，因为你正在使用的编程语言或库中的特性或缺陷。

你可能会看到的另一种类型的评论基本上是这样的:“我不知道为什么这有效，但我尝试的所有其他方法都失败了。”

这显然不是脚手架评论。同样，它不应该是一个永久的评论。不难想象，如果这样的注释在程序源代码中停留的时间超过了它应该停留的时间，它会成为一个问题。

假设你真的弄明白了为什么某样东西会起作用，并且也想出了一个更好的方法来做同样的事情。您将程序更改为更优雅的方式，但是您忽略了删除注释。

这个评论很可能会让你的团队感到困惑。它甚至会让你困惑。对项目质量的批评应该变成行动项目。例如，代替

```
// I don't know why this works, but nothing else did
```

写

```
// TODO: Figure out why this works
```

待办事项评论可能会像其他评论一样过时。但至少更清楚的是，该评论预计最终将变得没有必要。当这种情况发生时，可以安全地删除它。

面对你不太理解的待办事项，问题很简单:任务完成了吗？如果是，则应删除该评论。如果没有，问题还是很简单:任务还需要做吗？如果没有，则应删除该评论。就是这样。

随着我想的越来越多，我觉得所有的脚手架评论都应该是 Do 评论。这提供了另一种方法来衡量团队的项目进展。在开始的时候，项目会有很多待办事项的注释。随着项目的进展，待办事项的数量应该会下降。

我知道 IntelliJ IDEA 和 Apache NetBeans 都提供了一种收集和访问项目中所有待办事项注释的简单方法(它们属于 NetBeans 中的操作项类别，还有编译错误)。

当弄清楚为什么某些东西能工作时，有必要通过注释掉一些行来使它们失效。可能所有的集成开发环境都提供了一个简洁的键盘快捷键来实现这一点。

但是这种停用的行不能进入下一个版本控制提交。如果它们是必要的，它们必须被重新激活(取消注释)，如果它们是不必要的，它们必须被删除。

如果您错误地删除了被注释掉的行，而这些行后来被证明是必要的，那么您总是可以从远程存储库中检索它们，或者如果不能，从本地历史中检索它们。

停用的行比过时的注释更有可能在以后迷惑程序员。

简而言之，必须删除所有不必要的评论。

上述内容不适用于许可证头，许可证头是样板文件，不表示控制流，可能是您的法律部门所要求的，因此是必需的。

这也不适用于文档注释(如 Javadoc ),这些注释对您、您的团队以及潜在的使用您的程序但无权访问程序源代码的人来说是真正有用的。

我决定采纳一条个人原则，只使用三种类型的评论:

*   许可证头(每个类或接口源代码列表的顶部各有一个)
*   文档注释(例如 Javadoc)
*   待办事项注释

在我使我的存储库符合这个规则之前，还需要一段时间，但是我认为在达到完全符合之前，它将开始得到回报。