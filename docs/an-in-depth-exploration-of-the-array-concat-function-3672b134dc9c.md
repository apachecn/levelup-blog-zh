# 对 Array.concat()函数的深入探究

> 原文：<https://levelup.gitconnected.com/an-in-depth-exploration-of-the-array-concat-function-3672b134dc9c>

## Javascript 数组方法完全指南

![](img/3790a173ef33fafe648c96f1940e57d3.png)

照片由[沙哈达特·拉赫曼](https://unsplash.com/@hishahadat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

在过去的几年中，Javascript `Array`全局对象中增加了很多有用的函数，当开发人员编写使用数组的代码时，这些函数为他们提供了各种各样的选择。这些函数提供了许多优势，其中最值得一提的是，虽然过去开发人员必须实现自己的复杂逻辑来执行各种数组操作，但现在所有这些新函数都消除了对这种自主实现的需求。本文将探讨的有用函数之一是`[concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)`函数。

# 功能概述

`concat()`函数提供了将一组指定的数组项与一个数组的浅拷贝内容合并成一个全新数组的能力，并在函数完成时返回这个新数组。由于该函数产生了一个全新的数组，因此一旦该函数完成了操作，原始数组以及与原始数组合并的任何现有数组都将保持不变。在开始操作之前，不需要采取任何预防措施来确保原始阵列或任何包含的阵列得到维护。

`concat()`函数能够接受无限数量的参数，所有参数都是可选的*。每个指定的参数可以是单个项，也可以是任意数量项的数组。每个参数都被命名为`valueN`，其中的`N`由具体参数的位号代替。由于`concat()`函数的所有参数都是可选的，所以完全没有必要提供任何参数，在这种情况下，函数没有使用默认值来弥补参数的不足。*

# *没有参数*

*在介绍了一般的函数行为之后，让我们来看一些`concat()`函数在实践中如何工作的例子。以下示例演示了未指定参数值的情况:*

```
*var array1 = [1, 2, 3];
var array2 = array1.concat();
// array2: [1, 2, 3]*
```

*调用`concat()`函数时没有参数值。函数 shallow 复制原始数组的内容，并在函数完成后将这个副本作为一个全新的数组返回。使用`concat()`函数是这种方式基本上提供了产生原始数组的浅层克隆的能力。*

# *多个独立参数*

*以下示例演示了指定多个单独项目的情况:*

```
*var array1 = [1, 2, 3];
var array2 = array1.concat('abc', 'def', 'ghi');
// array2: [1, 2, 3, 'abc', 'def', 'ghi']*
```

*用三个单独的字符串参数值调用`concat()`函数。函数 shallow 复制原始数组的内容，并按照指定的顺序将三个字符串参数值连接到该副本的末尾，然后在函数完成时将其作为一个全新的数组返回。这是使用`concat()`功能最简单的方法。*

# *多个数组参数*

*下面的示例演示了指定多个数组的情况:*

```
*var array1 = [1, 2, 3];
var array2 = ['abc', 'def', 'ghi'];
var array3 = [4, 5, 6];
var array4 = array1.concat(array2, array3);
// array4: [1, 2, 3, 'abc', 'def', 'ghi', 4, 5, 6]*
```

*用两个数组参数值调用`concat()`函数。函数 shallow 复制原始数组的内容，并将第一个数组内容的 shallow 副本连接到原始数组副本的末尾，然后再连接第二个数组内容的 shallow 副本。完成连接后，它返回一个全新的数组，包含原始数组的内容和两个指定数组的内容。本质上，当遇到一个数组参数时，`concat()`函数处理该数组内容的方式与处理它们的方式相同，就好像它们是以与上一个示例相同的方式指定的一样，按照指定的顺序依次处理每个数组参数。*

# *多重嵌套数组参数*

*下面的示例演示了指定多个嵌套数组的情况:*

```
*var array1 = [1, 2, 3];
var array2 = [[4, 5], [6, [7, 8]]];
var array3 = [[[9, 10], 11], [12, 13]];
var array4 = array1.concat(array2, array3);
// array4: [1, 2, 3, [4, 5], [6, [7, 8]], [[9, 10], 11], [12, 13]]*
```

*用两个嵌套的数组参数值调用`concat()`函数。函数 shallow 复制原始数组的内容，并将第一个数组内容的 shallow 副本连接到原始数组副本的末尾，然后再连接第二个数组内容的 shallow 副本。完成串联后，它返回一个全新的数组，包含原始数组的内容和两个指定嵌套数组的内容。*

*与处理非嵌套数组参数值的方式不同，`concat()`函数以不同的方式处理嵌套数组参数值。`concat()`函数不会递归到嵌套数组中，而是将每个嵌套数组的内容连接到原始数组副本的第一级。对于嵌套数组内容，这意味着它们将作为数组直接连接到原始数组的副本，有效地将这些嵌套数组的嵌套级别减少一级。*

# *多个单个和数组参数*

*下面的示例演示了指定多个单独项和数组的情况:*

```
*var array1 = [1, 2, 3];
var array2 = [4, 5];
var array3 = [8, 9];
var array4 = array1.concat(array2, 6, 7, array3);
// array4: [1, 2, 3, 4, 5, 6, 7, 8, 9]*
```

*用两个单独的数字参数值和两个数组参数值调用`concat()`函数。函数 shallow 复制原始数组的内容，并将第一个数组的 shallow 副本连接到原始数组副本的末尾。在连接两个单独的参数值之后，它在完成连接并返回一个全新的数组之前，连接第二个数组的浅层副本。使用`concat()`功能时，可以根据需要混合单个项目参数值和数组参数值。只需关注所有这些参数值的指定顺序，因为它们将按照指定顺序连接到原始数组内容的浅层副本。*

# *经验教训*

*从这篇关于`concat()`函数的文章中可以学到一些东西。要记住的第一件事是`concat()`函数不会以任何方式改变原始数组，所以在使用该函数之前不需要维护它的状态。唯一会被`concat()`函数改变的数组是该函数完成后返回的全新数组。*

*关于`concat()`函数，要记住的第二件也是最重要的事情是，它如何复制包含在原始数组中的项目，以及被指定连接到原始数组的任何数组。对于像字符串、数字和布尔这样的原语数组项，`concat()`函数会将它们的值复制到新数组中。这意味着对原始数组或参数值数组中复制的字符串、数字或布尔值所做的任何更改都不会影响新数组。以下示例展示了这一功能的实际应用:*

```
*var array1 = [1, 2, 3];
var array2 = [4, 5, 6];
var array3 = array1.concat(array2);// array3: [1, 2, 3, 4, 5, 6]array1[0] = 7;
array1[1] = 8;
array1[2] = 9;
array2[0] = 10;
array2[1] = 11;
array2[2] = 12;// array3: [1, 2, 3, 4, 5, 6]*
```

*对原始数组和级联数组中的原始值进行更改不会导致对包含在由`concat()`函数生成的新数组中的原始值进行更改。*

*与处理原语不同，`concat()`函数处理对象引用的方式不同。对于作为对象引用的数组项，`concat()`函数会将这些引用复制到新数组中。这意味着从原始数组或参数值数组复制到新数组的任何对象引用都将引用完全相同的对象。如果对引用的对象进行了任何更改，这些更改将在原始数组或参数值数组以及新数组中看到。以下示例展示了这一功能的实际应用:*

```
*var array1 = [{ a: 1, b: 2, c: 3 }];
var array2 = [{ d: 4, e: 5, f: 6 }];
var array3 = array1.concat(array2);// array3: [{ a: 1, b: 2, c: 3 }, { d: 4, e: 5, f: 6 }]array1[0].a = 7;
array1[0].b = 8;
array1[0].c = 9;
array2[0].d = 10;
array2[0].e = 11;
array2[0].f = 12;// array3: [{ a: 7, b: 8, c: 9 }, { d: 10, e: 11, f: 12 }]*
```

*对原始数组或参数值数组中引用的对象进行更改也会导致这些更改反映在由`concat()`函数产生的新数组中。更改后的数组和新数组都将反映所做的任何引用对象更改。*

*关于`concat()`函数要记住的最后一点是，当需要复制一个现有数组时，它是 Javascript `Array`全局对象上可用的几个选项之一。由于`concat()`函数从原始数组生成了一个全新的数组，因此在调用该函数时不提供参数会影响这一特定行为。请记住，任何对象引用也将被复制到新数组中，因此`concat()`函数只是在需要浅层复制功能而不需要深层复制功能时才是可行的选项。*

# *结论*

*非常感谢您阅读这篇文章。我希望这次对 Javascript `Array`全局对象上的`concat()`函数的探索能够提供一些信息，并且我希望在获得一些关于它的知识之后，您能够在自己的代码中很好地使用它。如果您对其工作原理还有任何疑问，我鼓励您参考下面的资源链接，以获得关于`concat()`函数的所有信息。请在将来停下来阅读更多关于 Javascript `Array`全局对象上有趣且有用的函数的文章。*

# *资源*

*[Javascript Array.concat()函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)*