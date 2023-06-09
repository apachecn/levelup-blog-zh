# 角度模板语法做对了

> 原文：<https://levelup.gitconnected.com/angular-template-syntax-done-right-3a6906c86c1a>

## 如何优化双向数据绑定

![](img/bbe7f7cbd973fd652967c6c6c97dbf77.png)

如果您想构建大型应用程序而不存在与性能相关的问题，那么在使用 Angular 模板时拥有一个指南列表是一个很好的实践。

在本文中，我们将讨论 Angular 中的模板语法，以及如何通过正确的实践让我们的 Angular 模板代码 **e** 更具可读性和性能。

我们将学习用模板语法绑定的一些常见用例来绑定数据的最合适的方法，以及我们如何有效地解决当前/未来的问题。

> 我假设你对 [Angular 模板语法](https://angular.io/guide/template-syntax)有一个基本的了解，这是一篇关于模板语法的专题文章，你需要关于这个主题的基本知识。

在开始之前，让我们看一下在模板中绑定字符串变量的角度插值的基本实现。

**component.ts**

# 模板语法中的业务逻辑

让我们看一个例子:

*在 HTML 文件中编写业务逻辑不是一个好的做法。*

**这在更大的模板上产生了代码可读性、可维护性和可重用性的问题**,因为 HTML 模板不是用来编写业务逻辑的。

> 在 TS 文件中写一个逻辑代码是很好的。

推荐的方法是**在组件**中创建一个 getter 属性，并在 HTML 模板中使用各自的属性。

下面是转换后的代码:

> 上面的代码让我们有机会在多个领域使用相同的代码:在模板和组件中，如果需要的话。

# 从模板调用方法

> *当我还是一个初学 Angular 的开发者时，从模板中调用组件方法似乎是正确的*

由于数据来自父组件，**我习惯于从 HTML 中调用方法**，因为这比其他方法更容易(快捷方式对开发人员总是有用的)。

> 根据 Angular 文档，上面的代码没有问题

然而，这种方法有一些潜在的问题。

> 如果方法内部有复杂的业务，那么模板呈现将花费时间，并且性能会降低

让我们转换代码:

我们已经为`items`属性使用了 setter 方法，无论何时调用 setter 方法，它都会根据值设置`total`。

*所以不需要从模板调用方法。*

看起来不错，但是你可能会想，如果我们可以通过使用`ngOnChanges`方法实现同样的事情，为什么我还要使用 setter 方法。

我们可以，但是**如果复杂性增加，那么就很难管理带有`if`子句的`ngOnChanges`方法中的大量代码**，并且在某些地方**我们失去了 TypeScript** 中可伸缩代码的能力。

> 根据复杂性，由您决定哪一个更适合您的应用程序

*基于我的组件复杂性*，我更喜欢这两种方法。

如果我有多个`@Input`装饰器属性，那么我更喜欢用 setter 方法，否则就用`ngOnChanges`。

按照惯例，**一个方法代表一个动作**，一个**属性代表一些数据**。

> Getter 属性在没有计算复杂性、代理另一个对象的值或隐藏私有变量等情况下非常有用。
> 
> 另一方面，这些方法在我们的业务运营过于昂贵或异步流程等情况下非常有用。

我想分享一个不适合`setter` / `ngOnChanges`方法的用例:

> 数据来自返回产品列表的服务器，我们必须在表格中显示产品名称和可用性(计算)。

我更喜欢从模板中调用方法，如下所示:

解决问题的一个办法是应用[单一责任原则](https://en.wikipedia.org/wiki/Single-responsibility_principle)。

请参见下面转换后的代码:

让我们讨论几个你可能有的问题。

## **为什么我们创造了一个阶级，而不用阶级也能达到同样的目的？**

是的，我们可以，但是**我们失去了单一责任原则实践的好处**,因为除了类之外，我们还必须编写用于等级计算的代码，无论是在服务类/组件/角度模板中，并且如果在具有不同服务类的多个组件中使用相同的实体并对其进行微小的修改，则代码会变得笨拙/重复。

> 创建一个类使我们能够在多个组件中使用与实体相同的行为

这满足了代码可维护性和可重用性的需求。

类是有价值的，这仅适用于我们需要初始化属性和方法**来帮助创建对象/处理业务规则**的时候。

## **为什么我们在组件的分级方法中不使用记忆化？**

简单来说，

> 记忆用于繁重的计算逻辑，可以显著提高性能，我们的情况不适合记忆。

如果我们采用这种方法，**如果在模板中使用多个方法，可能会增加内存消耗和代码复杂性**。

到目前为止，我们关注的是访问**对象属性，而不是模板**中的方法，但是这对于更快地渲染模板来说是不够的。

**为什么？**

在这段代码中我们可以做两个改进:用`ngFor`绑定数据，并应用`OnPush`变更检测策略。

# 使用*ngFor 绑定数据

在更新产品列表的“任何人”行后，将重新计算整个列表。

> 这影响了较大数据的性能问题。

为了解决这个问题，我们可以使用 **"trackBy"** 函数，它帮助 Angular 知道如何在产品集合中跟踪我们的元素，唯一修改的值将被重新计算和重新绘制，而不是整个集合。

请参考下面修改后的代码:

# OnPush 变化检测策略

缺席

> Angular 在每次应用程序中发生变化时对所有组件执行变化检测，这将检查模板表达式的值是否发生了变化

**如果组件复杂度增加，那么检查**就需要更多的时间，但是通过`ChangeDetectionStrategy.OnPush`，我们告诉 Angular 只检查引用是否改变，而不是检查每个属性的值。

> 通过这种方法，我们显著提高了性能

使用`OnPush`，当出现以下情况时，对组件进行变更检测:

*   **输入参考值**改变
*   一个本地的 **DOM 事件**是由组件或者它的一个子组件触发的
*   **变更检测**是通过[changeedetorref](https://angular.io/api/core/ChangeDetectorRef)类的`detectChanges`方法手动触发的
*   **异步管道可观察值**获得新值

# 结论

所讨论的方法提供了基于特定需求组装代码的灵活性。

> 与方法方法相比，在模板中使用对象属性使我们的模板代码具有可读性和执行性是很好的

*感谢阅读！*