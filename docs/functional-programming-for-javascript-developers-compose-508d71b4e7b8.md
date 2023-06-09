# 面向 JavaScript 开发人员的函数式编程—编写

> 原文：<https://levelup.gitconnected.com/functional-programming-for-javascript-developers-compose-508d71b4e7b8>

![](img/d480e86315e3e41e607602d6c76dbcdb.png)

这篇文章是我一步一步教你如何从函数式程序员初学者成为专家的系列文章的一部分。如果你是一个完全的初学者，并且这是你第一次看到我的文章，我建议你阅读我之前的两篇文章，在那两篇文章中，我讲述了一些基本概念，如[纯函数、不变性](/functional-programming-for-javascript-developers-669c3db705f0)和[奉承](/functional-programming-for-javascript-developers-currying-2d16766909e9)。如果您已经了解了这一点，那么让我们继续讨论 Compose——函数式编程中最强大和最常用的技术之一。

## 什么是作曲

函数是函数式编程(FP)中最基本的构件，这可能不会让你感到惊讶。当以面向对象的风格编码时也是如此，但是在 FP 中我们使用它们有点不同。由于整个程序是由小的构建块组成的，我们需要一些技术来使它们一起工作。这就是作曲的用武之地。我希望您将 compose 视为一种将两个或多个函数组合起来创建新函数的方法。

在 FP 中，我们强调我们的函数应该只做一件事的理念。此外，函数应该是完全纯的，这种粒度会使单个函数看起来有点无用。但是当它与其他功能组合在一起时，它的威力才真正开始显现。

让我们开始做一些简单的例子。

那么我们如何使用这些函数来格式化一个字符串呢？我遇到过几个开发人员，他们会像下面的例子那样做——如果这是你，我无意冒犯。这就是你在这里的原因，对吗？

让我们看看 FP 的方式:

什么，那是怎么回事？诀窍是从内向外阅读这段代码。首先调用`trim`。然后这个函数的结果被发送到`capitalize`，然后这个结果被发送到`exclaim`，后者返回最终的字符串。很酷吧。所有这些都是在没有任何数据突变的情况下发生的。原始字符串保持不变，因为我们只使用纯函数进行组合。

另一件有趣的事情是，如果像这样格式化字符串是我们经常做的事情，我们可以像这样创建一个全新的函数:

哇，看那个，我们刚刚做了一个可以重用的通用函数。好吧，也许这不是世界上最有用的函数。但希望你开始看到它提供的力量。

在 FP 中，你可以看到像乐高积木一样的功能。当你为一个特定的领域开发一个程序时，你会惊讶地发现我们重复的代码数量。使用只做一件事的小而简洁的函数，您将会有更少的重复代码。此外，您将有更少的错误，并且您的函数可以很容易地测试——这是使用纯函数的巨大好处之一。

# 合成功能

您可能已经发现，将函数包装在一个函数中，而这个函数又被包装在另一个函数中，这对可读性来说并不好。那么，我们为什么不写自己的函数来处理这个问题呢？我们喜欢函数，对吗？

我们先来看简单版:

你知道这是怎么回事吗？我们的`compose`函数将函数`f`和`g`作为参数。然后，它返回一个新函数，该函数将字符串`x`作为参数。注意看起来整洁多了。

不过，这里有一件奇怪的事情需要注意。这些函数从右向左应用，这是惯例。如果你向上滚动，看看我们在创建`compose`函数之前是如何应用这个函数的，这可能会更有意义。在这个例子中，你也是从右向左阅读。

如果我们想要组合两个以上的函数呢？那么，撰写功能就变得复杂得多，对于大多数人来说，是不可读的。如果你感兴趣，这篇文章很好地解释了它是如何工作的。

不过，你并不真的需要知道`compose`内部是如何使用它的。

看这里变得多干净。就像在看书一样，对吧？首先我修剪，然后我大写，然后我惊呼三声。

同样，`compose`的工作方式和我们的第一个例子一样。您传递的最后一个参数被发送到最右边的函数。然后，在为整个表达式返回最左边函数的结果之前，将结果传递给它左边的函数。

还有一个对应的是从左到右工作的，通常叫做`pipe`。如果你真的不能理解从右向左阅读，可以随意使用`pipe`来代替。但正常情况下，用不了多久就会习惯`compose`。

# 自由点

我需要坦白。还有一个技巧我一直瞒着你。你有没有注意到我们作曲的时候在`exclaim`、`trim`和`capitalize`后面没有使用任何括号？这怎么可能呢？嗯，我们利用了一个叫做无点执行的概念。你看，在 JavaScript 中，如果我们打算在以后用一些参数调用函数，我们可以跳过函数的最后一个参数。以上面的 compose 函数中的`trim`为例。当我们宣布`capitalizeAndShout`的时候，我们没有执行任何事情。这只有在我们运行`capitalizeAndShout('yo, format me plz')`时才会发生。这就是`trim`被发送其参数的时间。

让我用`array.map`展示另一个例子

请记住，您发送给`map`的函数不会立即执行。每当我们到达循环中的一个项目时，它就会被执行。然后，JavaScript 将自动调用传入的函数，并将该项作为参数。所以，使用第一个版本只会让你的代码更难阅读。阅读第二部分要容易得多，比如——我们映射数组中的每一项并增加数字。

我建议你开始习惯无点数风格。过一段时间，就变得很自然了。只是少了些杂乱感觉很好。

作曲是一个非常强大的概念。不要被我这篇文章中的愚蠢例子所迷惑。一旦你在现实生活中这样做了，你就会明白我的意思。没有理由不立即开始。使用`compose`，你不需要全功能编程。就开始写一些纯函数，看看效果如何。首先，它很有趣。此外，没有什么比看到你的功能突然开始融合在一起更令人满意的了，就像最美丽的艺术品一样。

既然你已经知道了纯粹的函数，curry 和 compose，你的口袋里就有了一把神奇的瑞士刀。如果这是您从本系列中得到的唯一收获，那么您已经有了一些惊人的技术来使您的代码更具可读性和可测试性。而且更棒的是，用起来超级好玩。快乐作曲！

哦，我们才刚刚开始。在接下来的文章中，我们将开始研究更高级的概念。不像更难的那样高级。对大多数面向对象开发人员来说更像是陌生的。随着我们的深入，我们还需要看到一些现实生活中的例子。所以系好安全带，你即将成为 FP-gang 的一员！