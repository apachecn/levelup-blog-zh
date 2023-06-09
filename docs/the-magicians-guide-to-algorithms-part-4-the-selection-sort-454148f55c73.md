# 魔术师算法指南，第 4 部分:选择排序

> 原文：<https://levelup.gitconnected.com/the-magicians-guide-to-algorithms-part-4-the-selection-sort-454148f55c73>

![](img/ee1bc18e127790138ab6edf88a1a7644.png)

这个星期，海格教我们选择排序，所以嘘！既然他真的不应该教我们任何魔法，也不应该提到他在完成霍格沃茨之前就被开除了，那么他将要教我们的咒语并不那么有效也是很自然的。然而，它仍然有它的用途。

**选择排序**

这是你的咒语:

为了简单起见，我把我们的咒语分成了两个函数，因为一个函数只是抽象出了算法的一个小细节——交换。

swap 函数有三个参数，第一个是列表，第二个是要交换的第一个值，第三个是要交换的第二个值。在将`list[first]`改为等于`list[second]`之前，它将`list[first]`处的元素存储在一个临时变量中。最后`list[second]`将等于`temp`，这是我们更改之前`list[first]`的原始值。`temp`是存储原始值所必需的。否则，您将返回一个包含重复数字的列表。

至于咒语本身，发生的事情很简单。

选择排序算法有一个内部和外部循环。外部循环从零开始，并设置`min`值。该值从 0 开始。

内部循环将数组的其余部分与从 0 开始的`list[min]`处的值进行比较。如果`list[j]`处的项目大于`list[min]`，我们将`j`作为新的`min`。

最后，我们检查`min`是否已经改变。如果它不再等于`i`，它将已经改变。如果是这样，我们调用`swap`函数，将`list`、`i`和`min`作为参数传入。然后我们重复这个循环，这也是为什么这个算法如此低效的部分原因。

该算法将遍历列表中的每个元素，不管它是否部分排序。无论如何，它都需要顺其自然。这种算法甚至有各种变体，无论如何都会交换，这实际上没有什么区别，因为交换不会使算法变得更慢。这是内部和外部循环本身，加上算法在整个数组上迭代的方式，无论是什么使这个咒语如此缓慢。

**结论**

但是你有它:一个选择排序。施放这个法术有点像用慢动作发射 Flipendo，但它有时仍然会起作用。希望你喜欢本周的咒语，下周我将进行一次[广度优先搜索](https://medium.com/@AndrewBonner2/the-magicians-guide-to-algorithms-part-4-the-breadth-first-search-b800aec8ccf8) (BFS)。干杯！