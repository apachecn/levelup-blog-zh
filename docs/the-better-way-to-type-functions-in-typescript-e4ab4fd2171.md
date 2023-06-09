# 在 Typescript 中键入函数的更好方法

> 原文：<https://levelup.gitconnected.com/the-better-way-to-type-functions-in-typescript-e4ab4fd2171>

![](img/a0a6313eea6cfc7d71971a1006ac80ea.png)

不同的实例，但属于同一类型。

让我们从底线开始:有一个简单的替代键入 Typescript 函数的方法，它比 Typescript 的“本机”方法更简洁、更符合逻辑。它利用了一个实用类型，我称之为函数，它很容易定义:

例如:

请随意保存它，并在任何您认为有价值的地方使用它！

这个定义背后没有黑客——它只是有效地使用了 Typescript 的一些高级特性:

*   它的核心是类型 A 和 B——它们是[泛型](https://www.typescriptlang.org/docs/handbook/generics.html),它们是许多语言中面向对象编程的流行(高级)概念，包括 Typescript。简单地说，A 和 B 是通配符，它们使自己适应给定的上下文(或者适应您明确告诉它们的任何内容，如果您这样做的话)。它们可用于在更复杂或抽象的情况下提供更好的实施，以及更好的编程体验，并且在 Typescript APIs 和库中广泛使用。例如，对于上例中的`fn`参数，A 和 B 都变成了数字类型。
*   我们利用 Typescript 的能力将元组类型推断为函数参数集。例如，如果 A 得到类型`[number, boolean]`，编译器会将其解释为接收两个参数的函数——第一个是数字，第二个是布尔值。
*   为了提供 Typescript 的本机函数类型的真正一般化，即接收任何参数集(`any[]`)并可以返回任何东西(`any`)，我们为泛型 A 和 B 设置默认值。这意味着如果 A 和 B 没有显式设置，并且 Typescript 无法从上下文中推断出它们，A 将被设置为`any[]`(即，您可以向函数传递任何数量的任何类型的参数)，B 将被设置为`any`(即，函数可能返回任何东西)，就像本机函数类型一样。当然，如果不想让这个类型遮蔽原生函数类型，可以给它取个不同的名字，比如`Func`。
*   为了方便起见，在函数接收单个参数的情况下，我们使用[条件类型](https://www.typescriptlang.org/docs/handbook/advanced-types.html#conditional-types)将参数自动包装到单元素元组中。如上所述，Typescript 编译器知道将其解释为接收给定类型的单个参数的函数。因此，接收数字并输出数字的函数可以被键入为`Function<number, number>`而不是`Function<[number], number>`。注意:如果您希望这样的函数接受 A 类型的单个参数，*，其中 A 是数组或元组*，您必须用方括号将 A 括起来，例如`Function<[A], number>`。否则，编译器将解释该类型，使得函数需要接收多个参数，这些参数的类型是。

既然命题到位，那就来说说*为什么*:

# 动机

您可能会问:“Typescript 的内置函数类型化功能有什么问题？”对此我要说——不多，老实说，不是在基层。这肯定是可行的，但是有点麻烦，并且要求程序员包含可能是多余的信息。

如果您不熟悉内置的函数类型符号，它看起来像这样:

```
(arg1: Type1, arg2: Type2, /*...*/, argN: TypeN) => ReturnedType
```

例如，上面定义的函数 minimumOf()可以用如下的基本符号编写:

而且，说实话，基本符号并没有用太久，在这个例子中是*。但是这个参数看似不起眼的标签“x”在许多现实生活中变得更加突出。事实上，这是您在实际应用程序中很快会遇到的一个不便——您必须给这个参数起一个名字，您的困境是选择一个有意义的长名字，使类型(和您的代码整体)可读性更差，并且经常增加冗余——还是选择一个短的、非指示性的名字，使标签没有价值。对于有多个参数的函数，尤其是那些有类似用途的参数的函数(因此命名类似)，这就成了一个真正的问题。*

*例如，假设您正在开发一个团队任务管理器应用程序，并且您目前正在实现向队友分配任务的简单操作。该函数接收任务和队友作为参数，以及一个“分配者”参数，以跟踪谁分配了什么。作为一名优秀的 Typescript 程序员，您为每个参数(在整个应用程序中使用)定义了类型，分别命名为 Task、Teammate 和 Assigner，每个参数都有自己的字段。现在假设您需要显式地指定函数的类型(例如，您正在定义一个 React 组件，该组件将此函数作为一个属性接收，或者通常是包含此字段的任何接口)。*

*使用 Typescript 的基本符号，您可以写:*

```
*assignTask: (task: Task, teammate: Teammate, assigner: Assigner) => void*
```

*但是，正如您可能注意到的，类型确实很长，而且显然是多余的:单词“task”、“teammate”或“assigner”出现两次并没有什么好处。如果你想知道的话，那些参数标签不会对可赋给该类型的函数中的实际参数名施加任何约束。这意味着函数*

```
*assignTask(aaa: Task, bbb: Teammate, ccc: Assigner): void {
	//...
}*
```

*完全可以分配给我们的函数，使得参数标签变得毫无用处。*

*使用`Function<>`符号，我们可以得到一个更清晰、更易读的类型:*

```
*assignTask: Function<[Task, Teammate, Assigner], void>*
```

*值得注意的是，在一些函数中，参数标签*可以*服务于一个有意义的目的，并且是一种文档形式，明确哪个参数应该得到什么。然而，这绝不应该是强制性的，正如我们在上面看到的，这会使代码变得更糟。无论哪种方式，用`Function<>`符号标记参数现在也是可能的——我们稍后会谈到。*

*我的下一个观点是，函数——作为一个基本实体——不知道你给它们的参数贴了什么“标签”，我接下来会解释:*

# *作为一个实体运作*

*在数学中，函数的基本定义由三部分组成:*

*   *一个**域** —该函数接收到的所有值的集合(并且只有它们)。简单的例子是所有数字的集合，或者所有字符串的集合——但是任何集合都可以，真的。*
*   *一个**范围** —包含函数可以返回的所有值的集合(但不一定只是它们；所有实数的集合是一个函数的有效范围，该函数总是返回 1)。*
*   *一个**图**——域中的每个值到范围中的一个值的“映射”(从技术上讲，这也是一个集合)。*

*当且仅当这三个函数完全相同时，这两个函数才被认为是相等的。*

*通常，这些集合是隐式的。例如，在高中数学中，符号“𝑓(x) = x”经常被用来表示定义域和值域都是ℝ的函数，所有(实数)数的集合，并且将定义域中的每个元素(每个数 x)映射到它的平方。*

*计算机科学中的函数与数学中的函数并不完全相同。例如，程序中的函数对其环境有一些了解，并且会受到给定上下文的影响，如使用某个类成员的类方法，这会影响函数的输出。然而，为了讨论的目的，数学中的函数和编程中的函数之间的差异可以放在一边。*

*如果您将上面的函数定义与我们最初对 TS 函数类型的讨论进行比较，您会发现函数类型中考虑的两个因素是它的定义域和值域。函数“从ℝ到ℝ”，即具有域和值域ℝ的函数，是接收数字并输出数字的函数；毫无疑问，这两者是完全等同的。您可以对接收字符串、布尔值或任何其他类型的函数做同样的事情；从数学角度的函数到 Typescript 函数类型的“转换”是，TS 函数类型表示集合的元素—数字、字符串、布尔值等。—数学表示集合本身(例如，ℝ，所有实数的集合)。*

*数学定义还考虑了接收多个变量(参数)的函数——通过将变量的组合视为单个值(元组)，并将所有可能组合的集合(n 元组——就像编程中的元组)作为域。如果你看看上面，你会看到,`Function<>`符号正是这样做的——它将 assignTask 标记为一个接收包含任务、队友和分配者的“元组”的函数，Typescript 足够智能，可以理解我们引用的是函数的不同参数。*

*但是函数作为一个抽象的、基本的实体(遵循数学定义)，与你给定义域或值域元素的标签无关；事实上，上面的“高中”符号使用 x 作为ℝ的一般元素的标签(即一个数字的标签)，但我们也可以使用“y”、“z”或任何其他符号。这在编程中也是一样的——编译器不在乎*你用什么*来命名你的变量或者函数参数，它只需要知道什么标签指的是什么参数。美国程序员出于文档目的使用强制标签——我们给参数取了一个反映其目的的名称，这样函数更易读——这是一个很好的、值得鼓励的做法，但它不是函数“类型”(域&范围)的主要部分，因此在键入函数时不需要它。*

*总结这一点，`Function<>`符号**更好地反映了函数作为实体**的类型；参数标签有时很有帮助，但它们与函数的基本概念没有联系。*

# *Typescript 4 元组标签*

*如前所述，函数参数标签通常是无意义的和多余的，但偶尔可以用于澄清哪个参数是什么，主要是当参数类型或函数名称不能有效地这样做时。在这种情况下，您可以选择使用 Typescript 中的内置符号来键入函数，这完全没问题。但是， [Typescript 4.0 增加了一种标记元组元素的方式](https://devblogs.microsoft.com/typescript/announcing-typescript-4-0-rc/#labeled-tuple-elements)，因此即使使用`Function<>`符号，您也可以给参数加标签。*

*minimumof()函数，上面写为*

*也可以写成*

*如果你真的关心在函数类型中包含 x。但是，请注意，如果您选择标记一个参数，则必须标记所有参数。因此，**使用 Typescript 的内置函数类型符号的主要优势同样可以用** `**Function<>**` **符号**来实现，而且代码长度的“成本”几乎相同。*

# *摘要*

*正如我们已经看到的，`Function<>`符号是 Typescript 的内置符号的一个更好的替代，用于输入函数；它是用一行非常简单的代码定义的。它“覆盖”了 Typescript 的本机函数类型，添加了提供更强类型的泛型(归根结底，这就是 Typescript 的意义所在)，从而构成了本机类型的一个方便的一般化。*

*正如我们所看到的，它通常会使代码更干净，避免冗余，特别是在现实生活中的项目中，但它也支持额外的参数标签，在这种情况下可能更好。*

*最后，`Function<>`符号呼应了函数作为一个基本的数学概念的性质——这可能不是一个非常实用的优势，但我对此深表赞赏。*

*唯一的“缺点”,如果你可以这么说的话，是`Function<>`类型是一种你必须自己定义的类型——它不是 Typescript 提供的本机类型。也就是说，**这只是一行简单的代码来定义！**对于任何跨越几个文件的项目，尤其是对于现实生活中的应用程序，这实在是微不足道。*

*让我听听你的想法——欢迎你的想法、反馈和批评。*

*我希望我已经帮助你学到了一些新的东西！*