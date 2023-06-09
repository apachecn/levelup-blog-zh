# 截断和填充条目:JavaScript 数组技巧

> 原文：<https://levelup.gitconnected.com/more-javascript-array-tips-truncating-and-filling-entries-b112b8b149b8>

![](img/285c43b786bf9bf8dd6efe6b48dc2c61.png)

照片由 [Jametlene Reskp](https://unsplash.com/@reskp?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

JavaScript 和其他编程语言一样，有许多方便的技巧，让我们可以更容易地编写程序。在这篇文章中，我们将看看如何做涉及数组的不同事情，比如截断数组、将数组转换为对象以及用数据填充数组。

# 截断数组

在 JavaScript 中，数组对象有一个指定数组长度的长度属性。它既是一个 getter 属性，也是一个 setter 属性，所以除了能够获得数组的长度，我们还可以用它来设置数组的长度。

将`length`属性设置为小于数组的原始长度会将数组截断到我们指定的条目数。例如，如果我们只想保留数组的第一个条目，那么我们可以这样写:

```
let arr = [1, 2, 3, 4, 5, 6];
arr.length = 1
console.log(arr);
```

我们简单地设置数组的`length`属性，然后神奇地我们只剩下数组的第一个元素。

或者，我们可以使用`splice`方法从数组中移除条目。这个方法允许我们删除、替换现有的元素或者在适当的位置添加新元素，但是我们只需要用它从数组中删除元素。

`splice`方法的参数是开始改变数组的起始索引`start`。它可以是积极的，也可以是消极的。如果它是负的，那么它将从数组的末尾开始改变数组，并向数组的开头移动。结束索引是-1，第二个是-2，依此类推。

`splice`方法的第二个参数是`deleteCount`，这是一个可选参数，让我们指定从第一个元素的`start`参数开始删除多少项。

后续参数是我们想要插入到数组中的项目。我们想多久就多久。只有第一个参数是必需的。

例如，如果我们想要截断一个数组，只保留前两个元素，我们可以编写类似下面的代码:

```
const arr = [1, 2, 3, 4, 5, 6];
arr.splice(2)
console.log(arr);
```

正如我们所看到的，我们只需要指定第一个参数，然后`deleteCount`将被自动设置，以便它删除数组右侧的条目。我们还可以指定一个负的`start`索引，如下面的代码所示:

```
const arr = [1, 2, 3, 4, 5, 6];
arr.splice(-1 * arr.length + 1)
console.log(arr);
```

因此，如果我们在第一个参数中指定了`-1 * arr.length + n`，那么我们将保留原始数组的前`n`个条目。

我们也可以使用`slice`方法来截断数组。它通常用于从数组中提取值，并返回一个包含提取值的新数组。`slice`方法有两个参数。

第一个参数是可选参数，用于指定从数组中开始提取条目的位置。第二个参数是另一个可选参数，它指定原始数组的结束索引，以结束从中提取值。结束索引本身的值被排除在提取之外。

例如，如果我们想要原始数组中的前两个值，那么我们可以编写如下代码:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.slice(0, 2);
console.log(arr);
```

当我们运行代码时，我们将得到`[1, 2]`作为`arr`的新值。我们还可以为开始和结束指定负索引。数组的最后一项位于-1，倒数第二个元素位于索引-2，依此类推。因此，如果我们想要提取一个具有负索引的数组的前两个元素，我们可以编写如下内容:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.slice(-1 * arr.length, -1 * arr.length + 2);
console.log(arr);
```

如果我们用负索引来表示数组，那么数组的第一个元素将位于索引`-1 * arr.length`处。那么随后的条目将在`-1 * arr.length + n`处，其中`n`是在第`n`位置的数组条目。

![](img/2676c142d3a0de102ef9a7926ea54cfd.png)

Judi Neumeyer 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

# 用数据填充数组

在 ES6 或更高版本中，我们可以用一个数组填充新数据，使用`fill`方法。`fill`方法最多接受 3 个参数。第一个是我们想要添加到数组中的`value`。

第二个可选参数是开始填充数据的起始索引。

第二个参数的默认值为 0。第三个参数是可选的，它允许我们指定数组条目的结束索引。

第三个参数的默认值是数组的`length`。注意，结束索引本身被排除在填充之外，所以当我们调用`fill`方法时，它不会溢出。

该方法返回一个填充了新值的新数组。所有已填充的现有值将替换原始数组中的任何现有值。

例如，我们可以按以下方式使用它:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8)
console.log(arr);
```

然后我们从`console.log`得到以下输出:

```
[8, 8, 8, 8, 8, 8]
```

我们也可以改变`fill`方法的索引来指定填充边界。例如，我们可以写:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8, 3, 5)
console.log(arr);
```

然后我们得到:

```
[1, 2, 3, 8, 8, 6]
```

从`console.log`开始。如果我们指定了一个超过原始数组的`length`的结束索引，那么它将替换原始数组中的值，直到原始数组的最后一个位置。例如，如果我们有:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8, 3, 10)
console.log(arr);
```

然后我们得到:

```
[1, 2, 3, 8, 8, 8]
```

我们也可以使用负索引通过`fill`方法指定填充边界。数组的最后一个位置是-1，倒数第二个位置是-2，依此类推。所以我们可以像下面这样用负索引调用`fill`:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8, -4, -1)
console.log(arr);
```

然后我们得到:

```
[1, 2, 8, 8, 8, 6]
```

因为第三个参数不包括最后一个索引。如果我们想用新值填充最后一个元素，那么我们只需省略最后一个参数，如下面的代码所示:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8, -4)
console.log(arr);
```

当我们运行上面的代码时，我们得到了`[1, 2, 8, 8, 8, 8]`。如果第二个参数的值大于第三个参数的值，则不会发生填充操作，并返回原始数组。例如，如果我们有:

```
let arr = [1, 2, 3, 4, 5, 6];
arr = arr.fill(8, 4, 1)
console.log(arr);
```

然后我们得到原来的数组`[1, 2, 3, 4, 5, 6]`。

# 结论

在 JavaScript 中，数组对象有一个指定数组长度的长度属性。它既是一个 getter 属性，也是一个 setter 属性，所以除了能够获得数组的长度，我们还可以用它来设置数组的长度。这意味着将`length`属性设置为小于数组的原始长度。我们也可以使用`splice`和`slice`方法来截断数组。

在 ES6 或更高版本中，我们可以用新数据填充数组，方法是`fill`。`fill`方法最多接受 3 个参数。第一个是我们想要添加到数组中的`value`。第二个可选参数是开始填充数据的起始索引。

第二个参数的默认值为 0。第三个参数是可选的，它让我们指定填充数组条目的结束索引。第三个参数的默认值是数组的`length`。

我们还可以对第二个和第三个参数使用负索引来设置边界。