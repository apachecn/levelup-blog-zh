# 更好的类型脚本代码的 5 个技巧

> 原文：<https://levelup.gitconnected.com/5-tips-for-better-typescript-code-5603c26206ef>

![](img/5e94353808293377d2607d91e3fb2512.png)

提高打字质量的 5 个技巧

JavaScript 有很多问题。TypeScript 有很多解决方案——但是其中一些需要稍微挖掘一下才能找到。

在我前端旅程的早期，我发现 TypeScript 是 JavaScript 的许多问题的解决方案。在我的开发过程中，传递不正确的参数、无组织的开关或空访问每天都会出现。

在我的 JavaScript 上添加一个 TypeScript 层，使我的生产率飞速提高。我一直在学习 TypeScript 的来龙去脉，在这里和大家分享一下我学到的东西。

如果这些技巧对你来说还不够高级，我推荐你去看看这篇文章，在这里我写了 5 个高级打字技巧！

# 1.零聚结

有时，TypeScript 会自动在属性访问字段中插入一个问号。类似于`let t = myObj?.property` 然后`t`以值:`property | undefined`结束。这很好，但是确切地知道这里发生了什么是很重要的，这样您就可以将它作为一种工具来使用，而不是作为 TypeScript 自动完成的副产品。

如果我们使用一个常规的属性访问，`myObj.property`，并且 myObj 未定义，我们会得到一个错误:`Cannot access property 'property' of undefined.`这显然不是我们想要的，所以使用`.?`意味着如果`myObj`未定义，我们就“停止查找”那里，只将`t`赋值为未定义。

这对于避免错误非常有用，但有时我们需要默认情况。例如，如果我们有一个用户从未激活的文本字段，因此内部文本是未定义的，该怎么办？我们不想把`undefined`送到后端。我们可以将**可选访问操作符**(我们刚刚学过的，`.?`)与**空合并操作符链接起来。大概是这样的:**

```
sendFieldToServer(textField?.text ?? '')
```

这是非常有弹性的代码，可以非常安全地处理很多情况。事实上，**不可能将未定义的传递给函数。TypeScript 知道这一点，所以如果`sendFieldToServer`接受`string`的属性，它就能工作！**

这是因为 null 合并操作符使得如果左边的是`undefined`，我们转而传入右边的，一个空字符串。

在 JavaScript 中，很容易忘记代码中所有可能未定义的地方。谢天谢地，TS 处理了这个问题，并在这里警告你`sendFieldToServer`不能接受未定义的。通过使用问号运算符，您现在拥有了 100%安全的代码。

# 2.不要使用默认导入

TypeScript 优于 JavaScript 的一个原因是代码自动完成。因为在 TypeScript 中，编译器确切地知道你当时正在处理什么对象，它确切地知道什么属性对你可用。如果你有一个`dog`对象，我们知道我们可以访问`bark()`方法。

也就是说，如果`dog`在范围内。

如果我们用默认导出在`dog.ts`中导出`dog`，就像这样:

```
default export interface Dog {
     bark: () => void,
}
```

那么进口可以是任何东西。如果我愿意，我可以将`dog`作为`cat`从另一个文件导入:

```
import cat from 'dog.ts'cat.bark()
```

这是有效的类型脚本代码。这意味着如果我们这样做:

```
let t: dog = {
   bark: () => console.log('woof!')
}
```

TypeScript 不知道`dog`是什么。在`dog`下面会有一条小红线，表示`dog`未定义。您需要找到 dog 的定义位置，并手动导入它——然后确保将其命名为 dog。

这就是常规出口的切入点。像这样导出`dog`:

```
export interface dog {..} //export without 'default'
```

意味着现在，在我们的另一个文件中，当我们键入`let t: dog`时，typescript 知道寻找一个名为`dog`的接口！这意味着您将自动将导入放入文件中，并且 TypeScript 知道您可以吠叫。

代码自动完成是一个很棒的特性。我发现没有理由更喜欢默认导出，因为常规导出系统实际上更有用。即使你只出口一件东西，常规出口仍然可以轻而易举地处理。

eslint 有一个`no default export`规则，可以让任何默认的导出都被标记出来。

# 3.使用受约束的字符串字段

枚举是这个星球给程序员的礼物，所以当 JavaScript 决定不使用枚举时，它充其量从 S 层语言变成了 B 层语言。

虽然 TypeScript 有自己的枚举，但说…你并不 100%需要它们可能会令人惊讶。枚举由于必须定义它而增加了一点开销。TypeScript 有更好的东西。

`t: "left" | "right" | "middle" = "middle"`

这在功能上作为枚举操作。你可以打开它，除了这三个值，你不能给 t 赋值。但是我们在一行中定义了它，并且 TypeScript 知道不允许在其中包含任何其他内容。如果我尝试做`t="center"`，TypeScript 会出错。我可以 100%确定`t`的值是这 3 个值中的一个，所以我可以做像打开这 3 个字符串这样的事情，而不必担心缺省值。

另外，t 仍然是一个字符串。因此，如果我们想向用户显示值，我们可以将它传递到字符串字段中，这样就可以很好地工作了。

# 4.使用地图

JavaScript 确实有一个优势，那就是灵活的原型系统。你可以毫不费力地在任何物体上添加任何键。`myObj.nonExistantField = "Is This" + 12312 + "A string or a number? Who Cares!" * 4`有效。但是，让我在一个一些秘密…

1.  并不快。
2.  迭代不容易(需要`Object.keys(myObj)`或者类似的)
3.  如果每个程序员都只是将字段附加到对象上，那就很难共事了
4.  一个字段的存在并不意味着它的值被定义

你也可以在 TypeScript 中做同样的事情，允许值是任意的，但是我甚至不打算告诉你怎么做，因为我不希望你这样做。

相反，存在着`Map`。它也存在于 JS 中，但是在 JS 中它没有类型限制，所以它不是很有用。它是这样工作的:

`let myMap: Map<string, string> = new Map()`

这创建了一个地图，它解决了我提到的基于原型的地图的所有问题。

1.  它很快:HashMaps 的检查速度是 O(1 ),添加速度也很快。
2.  很容易迭代，用`map.forEach()`
3.  只要键和值的类型正确，您仍然可以将任何内容放入其中
4.  undefined 不能在其中(只要你没有将类型定义为 undefined)

地图很棒，这也是为什么它们是面试中最常被问到的数据结构问题。在我看来，它们比基于原型的映射要好。如果您曾经试图允许用户定义一个对象的键，也许您正在使用错误的数据结构。

# 5.算出你的 eslint 配置/ tsconfig

一般来说，TS 和 JS 最大的优点是可以在代码中进行大量的定制。例如，我来自 python，我偏爱无分号风格。所以我说“不要分号！”在我的 eslint 配置中，现在当我不小心放入分号时，我的编译器对我大喊大叫。

在我看来，保持双引号一致会使代码看起来更漂亮，因为你经常使用“in strings but not”。所以我在我的 eslint 配置中，必须使用双引号。

我非常喜欢在模式匹配中强制耗尽，所以我在我的 tsconfig 中强制这样做。

我更喜欢无默认导出，所以我强制这样做。

我强烈建议你每天花一个小时浏览一下`.tsconfig`和`.eslintrc`文件中的所有值，并根据自己的喜好设置所有选项。然后，将这些文件保存在计算机上的某个地方，这样当您开始一个新项目时，就可以很容易地将其粘贴进去。

我对我的代码非常满意，并且我发现当所有这些规则都被强制执行时，它变得更加干净——作为一个额外的奖励，任何参与你的项目的人都必须遵守`eslintrc`中一致同意的风格和`tsconfig`中一致同意的功能，所以你可以保证项目的一致性。

就是这样！这是我对打字稿代码的 5 个建议。我总是在寻找更多的建议，所以如果你有任何重要的东西，请让我知道！