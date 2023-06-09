# Python 类的所有基础知识

> 原文：<https://levelup.gitconnected.com/all-the-basics-of-python-classes-8b07046d2a52>

## 关于 Python 类你需要知道的一切！

![](img/2b7dda0fe7dde48f74fa206badd54dad.png)

> 想获得灵感？快来加入我的 [**超级行情快讯**](https://www.superquotes.co/?utm_source=mediumtech&utm_medium=web&utm_campaign=sharing) 。😎

Python 编程语言本质上是一种高级面向对象语言。它的设计旨在帮助程序员为任何规模的项目编写清晰的逻辑代码。

Python 简单、清晰、易于理解，但功能强大。这些设计原则真正体现出来的一个特性是 Python 类。

# Python 类

Python 中的几乎所有东西都是对象。当然，每个物体都有自己的特征、属性和功能。

我们可以把类看作是创建对象的“蓝图”。具体来说，我们自己为一个物体定制设计的蓝图。因为我们是定制它的人，我们可以给它任何我们想要的特性、属性和功能！

让我们从一个简单的例子开始。我们将创建一个具有属性“x”的类，其中 *x=10* 。这是我们的类定义:

班级

就是这样！我们已经创建了第一个名为`my_class`的 Python 类，该类有一个名为`x`的属性，其值为 *10* 。为了实际使用我们的类，我们“调用”我们的函数，然后可以单独访问该类的任何属性。

上面的代码打印出数字 10。轻松点。

我们也可以修改这个变量，只需给它赋一个新值。不要让`x`等于 10，让它等于字符串“鲍勃”。

# __init__()函数

所有的类都有一个我们可以随时修改的函数叫做`__init__()`。从该类创建一个对象时，总是会执行`__init__()` 函数，该函数可用于初始化一些类变量。所以，当我们希望我们的 Python 类总是以某些属性开始时，`__init__()` 变得非常有用。

我们以下面的代码为例。

在上面的代码中，我们用名为 Bob 和 Kate 的“Person”类创建了两个人。在这两种情况下，`__init__()`都被执行，为人名、性别和国家初始化类变量。

对于姓名和性别，我们将自己的变量传递给由`__init__()`接收的类。在“country”变量的情况下，它是在对象创建时初始化的，也是在`__init__()`中。唯一不同的是，因为它不是`__init__()`*的函数变量，所以不能从外部赋值——即所有人的国家都是“美国”！*

*代码打印结果将是:*

```
*Bob
Male
USA
Kate
Female
USA*
```

# *类函数*

*就像任何对象一样，Python 类可以包含函数！这些函数的行为和执行方式与类外的函数完全相同。唯一真正的区别是，类函数能够直接访问类变量，而不必将它们作为参数。*

*第 9 行的第一个类函数叫做`print_info()`，它打印关于我们的 Person 对象的所有可用信息。请注意，由于我们在`self`中使用了类变量，我们可以从类中的任何地方访问 Bob 的信息！这使得在 Python 对象上应用函数变得非常方便，因为您可以直接获得所有数据。*

*另一方面，注意我们需要多少额外的代码在外部使用 Python `print()`打印出 Bob 的信息。在一个特定的类中定义专门为该类设计的函数也更加有组织和简洁。*

*我们编写的第二个函数叫做`grow_person()`，它将人的年龄增加用户指定的年数。自然，将它作为一个类函数更有意义，因为它主要与我们的 Person 类相关。代码看起来也更加易读和干净！*

# *喜欢学习？*

*在推特上关注我，我会在这里发布所有最新最棒的人工智能、技术和科学！也在 LinkedIn[上与我联系](https://www.linkedin.com/in/georgeseif/)！*