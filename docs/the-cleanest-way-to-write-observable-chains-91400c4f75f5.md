# 写可观察链的最干净的方法

> 原文：<https://levelup.gitconnected.com/the-cleanest-way-to-write-observable-chains-91400c4f75f5>

我经常面临这样的情况，我需要保存一个可观测值的输出，但也要将它用作其他可观测值的输入。我遇到了如何清晰地组织信息的挑战。我经常面临以下情况:

*   我有一个可观察对象，它发出一个值，我需要保存并显示在 UI 上
*   第二个可观察对象需要第一个对象的值来执行其功能。

对我来说，这是一个很常见的场景。有几种方法可以写出你的观察值来实现这个目标。

## 解决方案 1:嵌套订阅

显然这种做事方式并不理想。一方面，如果`thingThatReturnsObservable`没有完成，我不得不担心创建太多的订阅。此外，它是可怕的嵌套，这使得它很难阅读。

## 解决方案 2:允许副作用

我认为这是一个可以接受的解决方案。这消除了一些嵌套，同时仍然在正确的时间设置一切。我唯一不喜欢的是我们在`[switchMap](https://rxjs.dev/api/operators/switchMap)`内部设置了一个组件级变量。这可能会使在代码库中进行可视化捕捉变得困难。我可以使用一个`[tap](https://rxjs.dev/api/operators/tap)`操作符来更好地描述副作用。但是理想情况下，我希望这样的属性设置发生在订阅调用中。

## 解决方案 3:结合可观察的结果

另一个解决方案是强制将第一个 observables 值传递给子对象。

我认为这是朝着错误方向迈出的一步。为生成复合可观察对象而添加的代码增加了复杂性。我认为这降低了可读性，而不是增加了可读性。

## 解决方案 4:打破可见链

我们可以使用另一种策略来提高可读性。也就是把可观察的事物分解成不同的函数。要做好这一点，可以使用`[shareReplay](https://rxjs.dev/api/operators/shareReplay)`函数在订阅者之间多播可观察对象。

我认为这个策略有很多优点。组件级变量都是在订阅中以一种非常清晰易读的方式设置的。`[shareReplay](https://rxjs.dev/api/operators/shareReplay)` 使得父可观察对象只被调用一次，但仍然在任何需要的地方提供信息。人们甚至可以更进一步，直接使用新创建的`parseId$`，而不是使用`componnetLevelVariable`。在 Angular 的上下文中，这意味着根据需要使用[异步管道](https://angular.io/api/common/AsyncPipe)或其他可观察的函数链。

我不喜欢这种模式，因为它更冗长，会导致应用程序中更多的回调。随着代码库变得越来越大，存在一些风险，这些现在自治的代码可能会以这样的方式移动，从而丢失原始上下文。此外，还有更多订阅需要管理和取消订阅。

# 那么答案是什么呢？

抱歉，今天没有明确的答案。在我看来，写可观察链的正确方式介于“解决方案 2”和“解决方案 4”之间。对我个人来说，我想更多地尝试“解决方案 4 ”,以更好地理解它在复杂的代码库中面临的挑战。目前，至少这概述了不同的策略。