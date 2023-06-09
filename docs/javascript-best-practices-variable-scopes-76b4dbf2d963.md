# JavaScript 最佳实践—可变范围

> 原文：<https://levelup.gitconnected.com/javascript-best-practices-variable-scopes-76b4dbf2d963>

![](img/38c9b24502f9de360cf4d3b9d0177b68.png)

照片由[mar liese stree land](https://unsplash.com/@marliesebrandsma?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

JavaScript 是一种非常宽容的语言。编写可以运行但存在问题的代码很容易。

在本文中，我们将研究声明变量和使用 JavaScript 变量范围的最佳实践。

# 范围

作用域是我们可以访问变量的地方。

JavaScript 有几种作用域。用`var`声明的变量有函数作用域，用`let`或`const`声明的变量有块作用域。

`var`变量也可以被提升，这样变量在定义之前就可以被访问。

`let`和`const`变量和常量不吊。

# 本地化对变量的引用

如果变量是用关键字声明的，那么它们在 JavaScript 中都是局部的。

如果不是，那么它们是全球性的。全局变量只能在严格模式下声明。

如果它是开着的，那么我们就不能声明它们。

声明全局变量时没有使用关键字。

因此，我们应该坚持使用`let`和`const`来声明变量和常量。

# 让变量在尽可能短的时间内“存活”

我们应该在尽可能短的时间内保持它们可用。这意味着可供变量引用的代码行应该很少。

这样，我们就不会轻易地意外地给它们赋值，从而减少出错的机会。

如果一个变量只在块内可用，那么这比在块外可用要好。

这是使用`let`和`const`的另一个好处，因为它们是块范围的，我们可以确保在它们被定义之前不能被引用。

此外，它们对块外的任何代码都不可用。

短暂的生存时间使我们的代码更具可读性，因为我们不必在头脑中保留太多东西。

初始化错误的机会将会减少。

我们还可以很容易地将块范围的变量分割成更小的函数。

# 最小化范围的一般准则

我们可以很容易地最小化变量的范围。

下面是一些最小化范围的指导方针。

## 在循环之前初始化循环中使用的变量

我们应该在循环之前声明循环中使用的变量，这样我们就可以马上看到它们被用在了哪里。

如果我们修改循环，我们会记住变量被使用，我们不会犯错误。

例如，我们可以写:

```
let done = false;
while (!done) {
  //...
}
```

我们在`while`循环之前有`done`变量，所以当我们在循环中工作时不会忘记它。

## 不要给变量赋值，直到值被使用之前

变量值不应该被赋值，直到值被使用之前。

通过这种方式，可以清楚地知道变量首先在哪里获得它的值，从而最大限度地减少混淆。

## 集团相关报表

如果我们有相关的陈述，那么我们应该把它们组合在一起。

这样，当我们准备好代码来获得整个工作流时，我们就不必来回跳转了。

## 将相关语句组分解成独立的函数

较短的函数具有较短的变量跨度，这有利于可读性。

变量的范围缩小了，这样我们就不必滚动阅读所有访问变量的地方。

![](img/e8e7cb90530fe2e56fb6593dd7da7b8b.png)

由[罗伯特·尼克森](https://unsplash.com/@rpnickson?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

## 从最受限的可见性开始，仅在必要时扩展变量的范围

块范围的变量有利于限制可见性。它将变量限制在块内。

我们应该只在需要的时候扩大范围，因为我们不想扩大“活动”时间，以减少意外分配它们的机会，使它们更难阅读。

# 最小化范围

通过扩展变量作用域来最大化作用域可能会使它们更容易编写，但是程序更容易理解，因为这些变量可能在任何地方被引用。

这不好，因为我们不想那样做。

我们必须查看所有地方的所有变量，以便理解一个变量是如何使用的，这对可读性非常不利。

因此，缩小范围绝对是我们应该做的事情。

# 结论

我们应该最小化变量的范围，使它们更容易阅读。

范围更小的变量也可以更容易地移动，这样我们在所有使用它们的地方查看它们就不会有困难。

因此，块范围变量和常量是好的。我们可以分别用`let`和`const`来声明。