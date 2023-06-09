# 你对你的代码做了太多的注释(以及对文档的其他有争议的想法)

> 原文：<https://levelup.gitconnected.com/youre-commenting-your-code-too-much-and-other-controversial-thoughts-on-documentation-1ee617ed46af>

![](img/63382b4a4512f47afa087f7f64b45392.png)

最好的代码注释通常是完全没有注释…在你拿出你的干草叉之前，让我来解释一下。

注释过多的代码通常比没有注释的代码更难理解。

来自一个项目的所有不同维护者的小笔记经常会变得混乱。你花在阅读注释上的时间比实际代码要多。通常，没有注释，你也能理解程序是如何工作的。

当然也有例外！我不是说你应该永远不写评论。

我是说，如果你能避免写评论，那就不要写！让你的代码独立存在！

有几个原因说明少评论是个好主意。在这篇短文中，我会试着解释我的意思，然后你可以在下面的评论中与我分享。；)

# **什么时候应该发表评论**

在我开始我的反评论谩骂之前，我应该说写评论绝对是个好主意！

但是这样的时间很少。

经典的经验法则是:[代码告诉你如何做，注释告诉你为什么](https://blog.codinghorror.com/code-tells-you-how-comments-tell-you-why/)。

这是一个很好的、有用的规则。但是并没有完全解决过度评论的问题。任何曾经和蹒跚学步的孩子相处过的人都知道你可以问“为什么？”永无止境的循环。

你可以对代码中的任何事情问为什么，但这并不意味着你应该对所有事情都进行注释。所以，你需要一个更严格的规则来决定何时添加评论。我的哲学是:

> 只有在无法避免的情况下才写评论。

当另一个开发人员阅读您的代码时，需要帮助来了解您为什么以这种方式解决问题，或者什么依赖使得某种方法是必要的，然后添加注释。

但是注释并不是解释代码的唯一方式。让我们看看我的意思。

# 如果你的评论解释了如何做——删除它！

消除评论的最大规则是不要这样做:

```
# Nested for loops to iterate through valuesfor i in outer_loop:
    for j in inner_loop:
       do something
```

任何优秀的开发人员都知道什么是嵌套的 for 循环，以及它是如何工作的。他们可以计算出代码运行时会发生什么。无需添加评论来解释。

下面是我第一次学习时写的一些代码，可以说明我的观点:

```
/* Use modulo and base-10 division/multiplication to reverse an 
 * int */while (original > 0) {
    reverse *= 10; 
    int r = original % 10;
    reverse += r;
    original /= 10;
}
```

这个评论很好，本身相对无害，但是没有必要。随着代码库的增长，类似这样的小注释会越来越多。添加足够多的内容，最终你的代码的未来维护者必须阅读的内容会翻倍。

删除这样的注释的最好方法是对变量使用正确的命名，并将代码放在一个像`reverse_int()`这样的命名良好的函数中

# 必要工作与增值工作

作为开发人员，你能做的最好的工作是增值工作。它是向用户提供功能的代码。你想最大限度地利用你的时间做增值工作。

然而，还有其他必要的工作。文档是其中的一部分。很好地记录你的代码使它易于维护和理解。

然而，文档并没有为用户增加任何东西。因此，尽量减少你写评论和其他文档的时间应该是一个目标。不要吝啬未来维护者需要的文档，但也不要浪费时间写没人需要的文档。

# 一个例子

下面是我最近写的一些代码，注释少了很多，但函数名和代码说明更好了:

```
unsigned int sum_squares(int m) {
    int i;
    int squares = 0; for (i = 0; i <= m; i++) {
        squares += i*i;
    } return squares;
}/* Quadratic, so could reach billions. Use long long.*/
unsigned long long square_sums(int n) {
    int j;
    int sum; for (j = 0; j <= n; j++) {
        sum += j;
    }

    return sum*sum;
}
```

(完全开放的更正我的 C 代码。绝不是专家！)

但是，您可以看到，在这段代码中只有一行注释。它解释了为什么我们需要更多的内存来返回`square_sums()`。

否则，好的命名会让一切变得清晰。当我在代码中的其他地方使用这些函数时，通过它们的名字就可以明显看出这些函数做了什么。

# 维护评论

很少提到的一点是，评论也必须维护！

当将来有人更改您的代码时，他们也必须在注释中更改对该代码的解释。花在改变上的时间越多，过程越慢。

如果您使用变量名和函数名作为文档的基线，那么您只需要重构代码，就大功告成了。但是如果你为你的函数和变量使用抽象的名字，那么你将不得不花时间去改变代码和注释。

这也是保持评论最少的另一个原因。

# 警告

在程序的顶部写一个块注释——或者在函数/类/支持文档字符串的语言的开头写一个多行文档字符串——解释程序的预期行为和算法采用的一般方法，通常是有帮助的。

当你去阅读一段你从未见过的代码时，这些也真的很有帮助。它使代码人性化，让你知道写代码的人在想什么。

# 少评论，但不要牺牲可读性

我错过了什么吗？关于你的编码工作流程和你如何使用注释，我是不是太过分了？

在下面的评论里告诉我！

如果你喜欢这篇文章，如果你鼓掌并跟随我，这将意味着很多。我定期写新帖子。

# 更多资源

[DeveloperPurpose.com](http://DeveloperPurpose.com)——关于如何建立有意义、有目的的科技职业的电子邮件课程

[混乱的代码让你付出了什么代价](https://bennettgarner.medium.com/what-your-messy-code-is-costing-you-3317e419df3a) —代码变得混乱是很自然的，但是清理它是每个人的责任

软件开发杂货——一个寓言。当你写代码的时候，想想杂货店