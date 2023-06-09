# 用可读的代码拯救世界

> 原文：<https://levelup.gitconnected.com/save-the-world-with-readable-code-2f55dbdade46>

## 初级开发人员可读性指南

![](img/889f1606cd4efad67a4fc98fa78ec89c.png)

克里斯·本森在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在您的编程生涯中，有一句话您可能会听到重复出现:

> *计算机科学中只有两件难事:缓存失效和事物命名。*

直观地命名事物、保持代码干燥、重构代码以使其可读:这些重要的最佳实践很容易被忽视，但它们对开发人员的成功至关重要。

记住，总有人要试着去读你写的东西。可能是两年后的另一个开发人员，可能是两周后的同事，也可能是两小时后的你。

如果那个人不伸手去拿阿司匹林就不能理解你写的内容和原因，那么你就有工作要做了。

一开始，编写可读的代码可能具有惊人的挑战性。让我们关注四个基本的可读性原则:

## 你的代码是一位大小的吗？

作为开发人员，您试图解决的问题通常相当大。因此，编写庞大的函数(或方法、类等)来解决它们是很有诱惑力的。

解决大问题更有效的方法是把它分解成小问题。然后你可以用更短的、有针对性的、简单的解决方案来解决这些小问题。

> 当解决一个大问题时，把它分解成小问题。
> 
> 然后写出可读性强、简单易懂的解决方案。

一口大小的解决方案更容易阅读，更容易重构，并且通常简化了首先解决问题的过程。

让你的功能简短而有目的。臃肿的函数更难阅读、重构和重用。你的功能是像子弹还是像铅弹？

## **你的代码干啥？**

写干巴巴的(不要重复)代码是软件开发的一个基本原则，它很好地发挥了编写小型解决方案的作用。

干代码通常与湿代码形成对比(每件事都写两遍，每次都写，我们喜欢打字，浪费每个人的时间，等等)。如果你不能在几秒钟内看到一个函数并知道它的明确目的，它可能需要被烘干。

当您消除不必要的重复和冗余时，干代码会出现在重构过程中。然而，有了意向性，您可以首先编写干代码，然后为自己节省时间和精力。

## 你的代码可以重用吗？

可重用代码是干代码的副产品。可重用代码通常采用简洁函数的形式，这些函数足够宽泛，可以在多种情况下再次调用。

根据定义，函数和方法旨在被多次使用或调用。在写一个的时候，问自己几个问题:我已经写了一个解决我当前问题的函数了吗？我能不能写这个函数，让它能解决我程序中其他地方的多个问题？

尽可能避免“硬编码”解决方案是很重要的。硬编码实际上保证了您刚刚编写的任何东西都不会成为您以后可以重用的东西。

## 你的代码直观吗？

这就是“命名事物”发挥作用的地方。让我们想象一个叫做*“num _ p”*的函数。

在上下文中，有人可能能够弄清楚该功能的设计目的是什么——但这可能需要一分钟的时间。这个函数会把玩家人数加起来吗？返回一个人数众多的数组？列举一堆馅饼？

取而代之的是，将这个函数命名为类似于*“查找玩家数量”*。这更加清晰易读。当你试图辨别它的目的时，你多花一秒钟去写的东西可以为你(和其他人)节省一分钟。

不要假设其他人(同样，包括你未来的自己)都知道你的首字母缩略词和缩写代表什么。

现在花一秒钟，为以后节省一分钟；这在一个程序的生命周期中积累了极好的时间投资。

![](img/7223d5e3463aaa7af49ea165919918d3.png)

几周前，我在熨斗学校开始了我的软件工程之旅。作为一个相对的新手，作为一名开发人员，我正努力让自己适应最佳实践。

突出的一点是:**可读性才是王道。**

可读的代码导致更好的应用程序。更好的应用程序能够对你的市场或客户群产生更大的影响。

让我们看一个例子。

下面是我用 Ruby 写的一个小科学怪人。这种方法试图解决 Hashketball 中的一个问题，这是一个传奇的熨斗学校预习课。

我的方法试图接受一个篮球运动员名字的参数，并返回该运动员的鞋号。为此，我进入一个嵌套的数据结构，提取两个包含玩家的数组，组合这些数组，将新数组设置为一个变量，然后通过该数组进行枚举以找到正确的玩家。

如果你在这方面有困难，你并不孤单。这表明需要进行一些重构和可读性工作。

```
def shoe_size(player_n) home_players = game_hash[:home][:players] away_players = game_hash[:away][:players] all_players = (away_players + home_players) all_players.each do |element| element.each do |key, value| if element[key] == player_n return element[:shoe] end end endend
```

呀。有用，但是很丑。那么我们怎样才能做得更好呢？看看重构后的版本。

```
def get_all_players(player_name) game_hash.map do |_, team| team[:players] end.flattenenddef get_player_by_name(player_name) get_players.find |player| player[:player_name] == player_name
   endenddef number_points_scored get_player_by_name(player_name)[:points]enddef find_shoe_size(player_name) get_player_by_name(player_name)[:points]end
```

从技术上讲，原始版本是 13 行，重构是 19 行。但是 refactor 可读性更好，它是干巴巴的，可重用的，甚至更容易编写。

重构中需要注意的几件事:

*   变量和元素的书写方式就像一个真正的人必须阅读它们一样(“玩家 n”对“玩家名”，“价值”对“团队”)
*   试图通读一个很长的方法会使理解这个方法正在完成什么变得困难。阅读一些简单的方法可以帮助你弄清楚你的代码正在完成什么。
*   新的一口大小的方法是可重用的。事实上，我后来在程序中调用了它们几次，这最终缩短了我的整个程序。

还有一点。在软件开发社区中，注释可能是一个极具争议的话题。有一种理论认为，你应该用注释来解释你的意图，从而向他人阐明你的代码。

然而，有一个替代的方法来大量评论。如果你把清晰明确的名字和简洁的函数结合起来，你就不需要很多注释来解释你的代码。你的代码读起来像一本书。

编写简单、枯燥、可重用、直观的代码需要练习。**在一天结束的时候，你的代码的可读性将是给所有将来使用它的人的礼物。**你也将在编写更好的全面应用程序方面迈出一大步。

编写可读的代码会让你成为一个更好的开发者，并且会提升你的作品的质量。你的同事和你未来的自己都会非常感激。

> 行不重要，可读的代码重要。

相关阅读:如何解决:数学方法的一个新方面作者[乔治·波利亚](https://www.goodreads.com/author/show/663311.George_P_lya)