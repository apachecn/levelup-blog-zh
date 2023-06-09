# Swift 中的依赖注入容器—第 1 部分

> 原文：<https://levelup.gitconnected.com/dependency-injection-container-in-swift-b4d7e139338c>

## 如何松散地耦合您的整个项目

![](img/01bf3a35acc85c32ec4c26433c503ccb.png)

帕特里克·布林克斯马在 [Unsplash](https://unsplash.com/s/photos/container?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

在本文中，我将讨论 swift 中的依赖注入容器(DIC)。在我之前的文章中，我探讨了如何在 Swift 中解耦代码，并介绍了解耦阶梯的四个级别，如果你不确定我的意思，可以看看。我已经提到了依赖注入或 DI，它是一种通过从外部注入类的依赖来将类与其依赖解耦的方法。

使用 DI 有助于类的解耦，但不能完全解决问题。创建子类的父类呢？我们只是将耦合从子类转移到父类。父类现在是紧密耦合的，让我们看一个例子。

`ParentClass`创建了`serviceOne`和`serviceTwo`。`ServiceOne`对`ServiceTwoProtocol`有依赖性，我们可以假设它们都是松散耦合或解耦的。然而`ParentClass`与`ServiceOne`和`ServiceTwo`紧密耦合，因为它创建了不可替换的特定对象。那么我们如何才能解耦`ParentClass`？

一种方法是注入`ParentClass`依赖项，在本例中是`serviceOne`。让我们看看那会是什么样子。

通过注入`serviceOne`，我们使得`ParentClass`松散耦合！这很好，但让我们更深入地思考一下。我们没有完全解决这个问题，因为现在`LooselyCoupledParentClass`‘母’将紧密耦合。创建对象的类将总是与创建的对象紧密耦合。我们只是把这个问题转给了其他班级。那么，我们如何尽可能多的解耦类呢？

在一个复杂的项目中，可能有许多类，每个类都有自己的依赖项。这些类可能会被排列成复杂的层次结构。对象的创建可能是分散的，导致许多类紧密耦合。

为了避免这种情况，我们可以创建一个负责创建所有其他对象的对象。你可能已经猜到了，我指的是依赖注入容器对象，让我们看看它会是什么样子。

# 依赖注入容器

我们对 DIC 的要求是能够从协议中解析(创建)我们需要的任何对象。这意味着我们向 DIC 请求一个符合协议的对象，DIC 创建它及其所有的依赖项。这听起来可能有点不可思议，事实是，确实如此。

为了能够解析对象，我们需要首先赋予 DIC 创建对象的能力。我们通过登记小工厂关闭来做到这一点。这听起来可能有点抽象，所以让我们看看这可能是什么样子。下面的例子是一个非常简单的 DIC，因为它的目标是理解它是什么，以及如何使用它。还有很多具有更多特性的库，例如 [swinject](https://github.com/Swinject/Swinject) 。

这可能看起来有点混乱，所以让我们一行一行地检查一下。

1.  我们声明一个 FactoryClosure 类型别名，它将我们的容器作为输入，并返回我们想要创建的对象。
2.  向特定协议注册工厂外壳。服务是泛型的，所以类型是在运行时解析的。服务也可以是一个类类型，但是我们希望我们的对象是松散耦合的，因此我们将只使用协议。
3.  解析(创建)符合协议的对象。服务是在运行时解析的一般服务。
4.  服务拥有所有的工厂，它的关键字是协议名，它的值是工厂闭包。

让我们看看将对象注册到容器会是什么样子。

1.  我们创造我们的容器。
2.  我们向`ServiceTwoProtocol`注册了一家工厂。工厂不需要容器，因为`ServiceTwo`没有依赖项，所以我们让它为空。我们返回一个`ServiceTwo`对象。
3.  我们给`ServiceOneProtocol`注册了一个工厂。工厂使用容器是因为`ServiceOne`有依赖关系。我们返回一个`ServiceOne`对象，其中容器被用来解析它的依赖关系。

现在我们已经设置了容器，让我们看看如何使用它。在继续阅读之前，请查看上面的代码，并尝试计算出创建了多少个对象。请随意留下您的答案作为回应。

# 把所有的放在一起

在我们的第一个例子中,`ParentClass`创建了自己的依赖项，这使得它与它们紧密耦合。让我们看看如何使用容器来解析`ParentClass`的依赖关系。

现在将 container 作为唯一的参数，并使用它来解析它的所有依赖项！在这种情况下，只有一个依赖项，但是在更大的项目中，可以有更多的依赖项。预先删除和添加依赖关系会影响初始化器，从而导致整个项目中的连锁反应。现在，删除和添加依赖项不会影响初始化器，这使得它更容易处理。

使用容器也有一些缺点。设置依赖关系是隐式的，而不是显式的，这意味着我们相信容器能够在运行时解析我们的依赖关系。另一个问题是，我们不知道一个对象依赖于它的初始化器。之前我们确切地知道类的依赖关系是什么，但是现在我们需要深入一点来弄清楚它。

为了尽量减少不利因素，让我们把事情说得更清楚些。我们可以添加容器初始化器作为一个方便的初始化，并保留我们原来的。让我们看看那会是什么样子。

这将需要更多的维护，因此开发人员需要权衡使用这种方法的利弊。

# 面向协议的方法

我们可以通过使用面向协议的方法来进一步改进我们的`DIC`。对于每个服务协议，我们可以创建一个`HasServiceProtocol`，它声明一个变量来解析所需的服务。让我们看看那会是什么样子

在声明我们的`HadServiceProtocol`之后，我们将它们添加到`DICProtocol`。`DIC`需要实现一个额外的 getter 来解析服务，如下所示

现在我们可以用面向协议的方式来解决依赖性了！让我们看看那会是什么样子

让我们一行一行地过一遍

1.  我们声明了一个`Dependencies` typealias，它定义了类需要的依赖关系
2.  我们的类是用符合`HasProtocols`的`DIC`对象初始化的
3.  我们使用`HasProtocols`来解析我们的依赖关系。请注意，每当我们解析一个依赖项时，都会创建一个新的实例。

这个解决方案要干净得多，我们只创建一个实例来保存我们所有的依赖项！添加和删除依赖项不会改变类的接口，减少了维护，尤其是在较大的项目中。

# 包扎

我们已经看到了如何使用 DICs 松散耦合我们的类。如果在整个项目中正确使用，我们可以松散地耦合所有的类，除了注册容器的类。这是对 DICs 的介绍，我建议查看一下 [swinject](https://github.com/Swinject/Swinject) 中的全功能 DIC。我希望你喜欢这篇文章，并祝你好运实现你的 DIC！

在下一篇文章[Swift 中的依赖注入容器——第 2 部分](/dependency-injection-containers-in-swift-part-2-5b24f1c4238a)中，我将探讨如何在解析对象时传递参数。

# 我的应用

[](https://apps.apple.com/us/app/koala-nap/id1478157024?ls=1) [## 考拉午睡

### 你或你的伴侣打鼾吗？现在你可以从第一天开始积极减少打鼾，使用考拉午睡。除了展示如何…

apps.apple.com](https://apps.apple.com/us/app/koala-nap/id1478157024?ls=1) [](https://apps.apple.com/us/app/last-flower/id1112524681?ls=1) [## 最后一朵花

### 你能拯救最后一朵花吗？iPad 上也有-小行星正在撞击地球，所有的…

apps.apple.com](https://apps.apple.com/us/app/last-flower/id1112524681?ls=1) [](https://apps.apple.com/us/app/tile-color-match/id1294483076?ls=1) [## 瓷砖颜色匹配

### 彩色瓷砖匹配是一个令人兴奋的新游戏。目的是通过移动底部的瓷砖来匹配上面的棋盘布局…

apps.apple.com](https://apps.apple.com/us/app/tile-color-match/id1294483076?ls=1) 

【www.koalanap.com 