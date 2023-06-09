# 书呆子如何解谜

> 原文：<https://levelup.gitconnected.com/how-nerds-solve-puzzles-1c9677fd8fb1>

## 暴力破解单词阶梯难题

![](img/ba5887ae41d5c86f4b4f56109af1a76e.png)

一个字谜。通过每步仅改变一个字母来连接这两个单词。图片由作者提供，背景图片由 Pixabay.com[上的](https://pixabay.com/)[flyum ike](https://pixabay.com/users/flyupmike-5768/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=69661)和[像素](https://pixabay.com/users/pexels-2286921/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=1839218)提供。

今年，我的母亲准备了一个难题降临日历。每天早上，她都会给我和我的兄弟姐妹们发一个新的谜题来解答。今天它是一个单词阶梯，你必须通过一次改变一个字母来连接两个单词。

我没有立即看到解决方案，所以我没有尝试手动解决，而是走了一条更简单的路线，编程一个工具来为我强行解决问题。

# 单词阶梯

单词阶梯谜题是一个简单的概念，但很难解决。你从一个单词开始，你必须通过一次改变一个字母来获得第二个单词，并且链中的每个单词本身必须是有效的单词。下面是一个将*冷*连接到*暖*的例子:

冷→CO**R**D→C**A**RD→**W**ARD→战争 **M**

我可能最终会解开今天的谜题。然而，有一个非常真实的机会，我不知道一个字的解决方案。即使在我的母语中，我也只经常使用大约 5000 个单词，而且可能还知道另外 5000 个。因此，当一个罕见的单词是正确答案的一部分，而我不认识这个单词时，就很难答对。

# 强力解决方案

我没有花半个小时试图手工找到答案，而是做了明智的事情，开始编写程序来为我找到答案。

## 词典

首先，我需要一份可以被计算机轻松解析的所有德语单词的列表。Open Office 的德语字典扩展正是我一直在寻找的。这是一个 258，200 字的列表。每行一个，这使得解析非常容易。

为了让最后的搜索快一点，我必须清理数据。因为正常的单词阶梯规则只允许相同长度的单词，所以我只需要考虑六个字母的单词，这使得集合减少到 9958 个单词。

不幸的是，在德语中我们有一些令人讨厌的变音符号(δ，θ，ü，δ),它们不能很好地与 C++中的普通字符串和字符一起工作。文本编码是一个噩梦，我不想为这个小项目处理它，所以我只是删除了所有包含其中一个的单词。它们非常罕见，不太可能是解决方案的一部分。德国的填字游戏也不用元音字母。虽然事后看来，我应该使用另一种更好地处理非 ASCII 字符的语言。

因为该列表是 Open Office 的字典，所以它还包含一些人名和地名，这些不计入单词梯。文件中的每个单词还有第二个参数，该参数编码了该单词的一些可能的前缀和后缀。乍一看，似乎大多数名称共享一个规则，所以我试图删除它们，但似乎有一些不一致，所以我把它作为一个可选参数。

之后，剩下 8512 个六个字母的单词。

## 树

为了找到解决方案，我采用了一种简单的树形方法。以起始单词为根节点，用恰好一个字母中与其不同的所有单词展开。然后所有的孩子以同样的方式递归扩展，直到深度达到 6(特定的谜题需要 6 个步骤，但它是一个变量，所以其他深度也是可能的)。深度为 6，分支因子小于 10，我相信它很容易工作(比 10⁶节点少)，所以我没有做任何其他优化。

## 搜索

有了一个完全展开的树，找到一个解决方案所需要做的就是遍历树，直到找到结尾的单词，然后保存到这个单词的路径。

我本可以使用一种更贪婪的方法，同时进行扩展和搜索，一旦发现解决方案就停止。然而，我很好奇有多少个解决方案，所以我做了一个完整的搜索，返回所有可能的解决方案。

## 结果

我母亲字谜中的单词是*克仁*(蜡烛)和*维特*(表亲)。我的程序找到了 9 种可能的解决方案。一些解决方案是双重的，因为就像在英语中，一些单词既可以是名词也可以是动词。不过，我可以使用`tolower()`来删除 doubles。这也包含了两个城镇名称( *Herten* 和 *Kerken* )，但是当名称移除选项打开时，它也移除了对我来说似乎有效的解决方案。虽然字典文件包含所有的单词，但是包含名称会使它有点混乱，所以我可能需要在将来寻找一个更好的单词列表。

![](img/81ee6c1a43da7dd25b594181a80c4006.png)

连接 Kerzen(蜡烛)和 Vetter(表亲)的所有 9 个解决方案，这包括一些名称和动词/名词，作者的图像。

## 速度

对于给定的谜题，完全展开树并找到所有解只需要不到一秒钟，这已经足够快了。

现在，我很确定我是今天解谜最慢的人。开发这个程序花了我一个多小时。然而，当有另一个相同类型的难题时，最好做好准备，我需要做的只是改变三个变量，我会在不到一秒钟内完成。

## 源代码

[这里的](https://gist.github.com/pingpoli/5741b95426088c0b714ea29aaea32de7)是我程序的源代码。使用正确的字典，它可以处理英语和德语，也可以处理大多数不使用太多非 ASCII 字符的语言。

我没有花时间试图手工找到一个我可能找到也可能找不到的解决方案，而是选择了我确信会返回结果的路线。我姐姐可以利用她在德语方面的卓越知识，那么我为什么不能利用我卓越的编程技能呢？

手动解谜很有趣，创建小程序也同样有趣。毕竟，无论是困惑还是编程，都有很大一部分是解决问题。

# 资源

*   [源代码](https://gist.github.com/pingpoli/5741b95426088c0b714ea29aaea32de7)
*   [打开办公德语词典](https://extensions.openoffice.org/en/project/german-de-de-frami-dictionaries)