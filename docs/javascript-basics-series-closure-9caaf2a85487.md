# JavaScript 基础系列:闭包

> 原文：<https://levelup.gitconnected.com/javascript-basics-series-closure-9caaf2a85487>

## 用简单明了的例子解释了一个重要的概念

![](img/c483bc7742a8c77c2c4e53aabcfcd23b.png)

> JavaScript 基础是一个探索每个前端软件工程师都应该理解的一些核心概念的系列。这些概念不仅对工作面试的成功很重要，对开发人员的职业生涯也很重要。

在【JavaScript 基础系列的这一部分，我们将解释一个非常重要的概念，即闭包。这不仅是 JavaScript 本身的一个核心概念，而且很可能在与 JavaScript 相关的访谈中出现，这一点尤为重要。事不宜迟，让我们开始吧！😃

什么是终结？

一个更好的定义是由 [Mozilla 的网络文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)提供的:

*一个* ***闭包*** *是用对其周围状态的引用捆绑在一起(封闭)的一个函数的组合(即* ***词法环境*** *)。换句话说，闭包允许您从内部函数访问外部函数的范围。在 JavaScript 中，闭包是在每次创建函数时创建的。*

换句话说，这是将一个函数放在另一个函数内部的事实，这使得被封闭的函数可以访问外部的变量。术语“词汇环境”在这种情况下指的是外部函数的范围。让我们用一个例子说明这一点:

```
function outer(){
     let outerVar = "outside"; function inner(){ let innerVar = "inside";
            console.log("The outer variable is " + outerVar); } return inner;
}
```

输出:`[Function: inner]`

> **在 JavaScript 中，默认情况下，任何被执行的函数都会创建一个闭包**

内部函数可以访问外部函数的变量，因为它在其*局部*或词法范围内。更具体地说，我想指出以下几点:

*   inner 可以访问 outer 函数的变量，而后者**不能访问 *innerVar* 。词法范围是单行道，只有内部函数可以访问外部函数中的任何内容。**
*   外部函数只能通过返回内部函数来获得结果(返回值、控制台输出等)。
*   只返回 ***函数定义*** ，不返回调用！不调用内部函数。
*   内部函数在执行之前从外部函数*返回。*

这意味着从技术上讲，它不应该能够访问外部函数的变量。在许多编程语言中，外部函数的所有变量都会被声明并一直存在，直到函数返回值为止(在本例中是内部函数)。当一个函数被调用时，它会创建一个*调用(或执行)栈，*，这只是专门分配的内存空间。每个调用都用一组局部变量创建自己的执行堆栈。例如，在 C/C++这样的传统语言中，调用内部函数会创建自己的内存堆栈(见下图)。因此，*内部函数不能访问其自身作用域*之外的任何变量。然而，在 JavaScript 中，执行的每个函数都会创建一个*闭包*。换句话说，每一个函数都有能力*将函数封装在其中，这种封装让它们的内部函数可以访问它们内部的所有变量*。因此，闭包就是函数和它的词法范围的简单组合。

![](img/507a4d1d9cd70502fdd020f86cc79279.png)

在其他语言中，调用一个函数会在内存中创建一个调用栈。在 JS 中，会创建一个闭包。

现在，假设我们想返回第二个函数中的实际值，而不是它的定义。为此，我们可以添加以下代码行:

```
let innerOutput = outer();  //Output: [Function: inner]
/*
 Here's what happens behind the scenes after the code above runs:
 innerOutput = inner
*/console.log(innerOutput())
//Same as innerOutput = inner();
```

输出:`The outer variable is outside`

闭包之所以如此重要，是因为它使内部变量保持私有。封闭函数外部的任何东西都不能访问它的变量。这在使用事件处理程序、部分应用程序和回调函数时非常重要。目标是保持事情简单，因此我们可以在另一个博客中讨论这些概念。

目前，我们可以将上述内容总结如下:

*   闭包是将一个函数封闭在另一个函数中的事实，这样被封闭的函数就可以访问其自身范围之外的变量。
*   默认情况下，JavaScript 会为创建的每个函数创建一个闭包。
*   闭包允许被封闭函数的变量的私密性

感谢您的阅读！编码快乐！😃