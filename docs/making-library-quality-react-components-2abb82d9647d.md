# 使库质量的 React 组件

> 原文：<https://levelup.gitconnected.com/making-library-quality-react-components-2abb82d9647d>

## 使部件具有柔性和弹性的技术

![](img/509aaa28b7312086f13e5d7eb2b3b1dd.png)

当你为自己或者作为一个团队中的一个前端开发者编写一个应用程序时，很容易跟踪你自己的组件的局限性。当你的组件被一个更大的群体使用时，或者如果它们被开发成一个共享库，脆弱或不灵活的组件将是你生存的祸根。其他开发人员会以您从未预料到的方式使用您的组件，或者要求需要几个小时或几天的返工。

不要害怕！下面你会发现一些使组件更加灵活的技术，并且在某种程度上，是经得起未来考验的。

# 用 useRef 管理 effects 中的函数属性。

如果我们的组件接受注入的处理程序，比如一个`onChange`处理程序属性，我们需要小心在`useEffect`、`useLayoutEffect`、`useCallback`或`useMemo`中使用它。人们会期望处理程序“正常工作”，但是如果不让它们在父组件喜欢的时候改变，那就不会发生。

我们来看看一个可调整大小的`<textarea>`。我们想让消费者跟踪它何时调整大小:

在这种情况下，如果父组件在组件的 main 函数中定义了,`onResize`的话，那么每次父组件呈现时，都会重新创建它。这意味着需要多次创建和重新创建 ResizeObserver，这将是非常昂贵的。

一个简单的方法就是从依赖数组中删除`onResize`:

这个[不仅破坏了依赖关系](https://reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies)的规则，它还可能在一个陈旧的父组件上结束工作。由于`onResize`只在组件第一次挂载时被捕获，如果父组件因为任何原因改变了`onResize`，ResizeObserver 不会知道。如果父进程使用`useCallback`在处理程序中嵌入组件状态，该状态将失效。

跟踪效果中的函数属性的正确方法是使用 ref:

通过使用`onResizeRef`而不是`onResize`，我们可以保证 ResizeObserver 将总是获得`onResize`的最新版本，不管父组件中发生了什么；我们不打破依赖数组；我们不强迫不必要的重播效果。

(useCallback 是为您在自己的组件中创建的函数创建稳定依赖关系的一种完全可以接受的方式。当您试图在通过属性接收的函数上使用它时，就会出现问题。)

# 将选项绑定到地图。

在设计元素时，您经常希望对相同的基本组件实现稍微不同的功能或样式。使用对象来选择做事的方式，而不是创建备选方案树。

在表示的情况下，利用从 CSS 模块返回的基于对象的映射:

SCSS 样式表如下所示:

您可以通过添加另一个类来轻松添加新的样式。(您可以对样式化组件和其他 CSS-in-JS 库做类似的事情。)

`[clsx](https://www.npmjs.com/package/clsx)`是一个小的库，可以让你轻松地组合类，省略假值并返回一个格式正确的`className`值。通过将`className`定义为`clsx(styles.basicStyling, styles[format])`，最终`<Button format="default" />`指向 CSS 模块选择器`.basicStyling.default`。如果开发者选择了一个不存在的类名，`clsx`不会尝试添加。

# 假设其他人想像使用 HTML 一样使用你的 HTML 包装器。

如果您构建了一个包装了 HTML 元素并添加了一些样式或次要功能的组件，假设使用您的组件的人会像使用 HTML 元素一样使用它。这意味着:

1.  **传递任何你没有明确消费的属性。有些人不明白为什么 T8 不起作用，他们只是在需要的时候知道它不起作用。不要试图解释出现的每个特殊情况，让 React 和浏览器来处理它。**
2.  **允许开发者给你的组件添加一个引用。**除非你的组件*必须*隐藏它所包装的 HTML，否则使用`React.forwardRef`添加一个对包装元素的引用。这使得开发人员可以完成他们自然期望用常规 DOM 元素完成的所有动态 HTML 工作。Refs 并不是对所有事情都是必要的，对于更复杂的 UI 元素来说可能会变得棘手，但是对于简单的包装器来说，它们是一个简单的附加物，使您不必维护额外的功能。

# 从简单的模块构建复杂的功能。

您可以使用*功能组合*通过在其他函数中包装函数来构建功能。外层函数不做主要工作。相反，它为你作为参数传递给它的函数做准备。

在文件列表的情况下，我们需要一种简单的方法来按照不同的字段以不同的方式对文件进行排序。通过组合排序器函数，我们可以通过向排序器的基本映射添加功能来创建复杂的排序组合:

在这里，您可以看到我们如何使用“选项映射”的思想来区分我们希望如何对特殊情况字段进行排序，然后如果需要的话，将它包装在一个反向排序器中，然后将它注入到一个根据请求的对象字段进行排序的排序器中。

需要注意的是:这些函数都有相同的签名:

```
(a, b) => number
```

它们中的任何一个都可以用作排序函数。(`sortByField`对对象进行排序，而不是对值进行排序，但这需要值排序器来告诉它如何处理对象的字段。)就功能组合而言，这并不是绝对必要的，但在这种情况下，它可以更容易地替换不同种类的功能。

通过使用这些样式和功能的映射，修改一个现有的选项或者创建一个新的选项变得更加容易，而不需要触及其他选项。

# 让您的设置被覆盖。

你不可能为你的组件的用户解决所有的问题。给他们一个出口，让他们按照自己特别想要的方式做事。在上面的`<Button />`例子中，你可以看到我们让用户包含他们自己的`className`属性，以防他们想要添加或覆盖任何样式。同样，我们可以为功能创建一个逃生出口:

您也可以在创建固定组件(如确认模式)时这样做。您的站点可能使用 MaterialUI 或 Ant Design 的全功能模态组件，但您真正需要公开的是“我应该是可见的吗？”以及“他们点击确定了吗？”

您最终可能会得到一个类似于

如果组件的用户对默认文本满意，他们只需要提供`onConfirm`、`visible`和`setVisible`。但是如果他们想改变模态或者确认按钮的文本，他们可以。(我故意不调用确认按钮上的`setVisible(false)`，因为我不知道`onConfirm`是否异步。)

## 让 const 帮助你重构代码。

顺便说一句，通过在代码中使用常量，当代码变得太复杂时，情况会变得非常清楚。

在上面的`FileList`例子中，当我们添加了`sorter`旁路时，很明显构建我们自己的分类器的行为会偏离组件本身的目的:分类。试图在我们构建的分类器和他们提供的分类器之间进行选择将会增加一堆常量，并使组件…忙碌起来。

我们可以用`let`代替`const`，如果我们没有得到`sorter`属性，我们可以用`if`来重新分配`usedSorter`，但是这样做告诉我们，我们正在解决在我们的分配中有一个大的`if`的问题。通过将分类器构建代码提取到它自己的函数中，组件本身就变成了一个紧密的、自顶向下的、只有一个目的的函数。同时，`buildSorter`也变成了一个紧密的、自上而下的、只有一个目的的功能类型。

虽然这是一个小而简单的组件，但“提取以形成线性”的原则更适用于复杂的组件。在我写的一篇关于结合上下文、归约器和定制钩子的文章中可以看到这一点。

# 假设您的组件属性是未定义的。

因为您可能不知道其他人如何使用您的组件，所以您不会知道他们是否会在异步填充属性的情况下使用它们。此外，如果一个组件依赖于在`useState()`中没有给出`initialState`参数的状态，那么第一次渲染将总是以未定义的状态开始。

因此，你必须假设你所依赖的任何属性在某个时候都是未定义的。这就是为什么如果`files`未定义，那么`FileList`组件会确保有一个空数组来扩展。否则，当组件试图遍历一个未定义的值时会崩溃。

# 使用耦合组件而不是属性将 JSX 嵌入到布局中。

上下文对于下推属性很有用，但是对于上拉数据也很有用。React 文档中的[是组合](https://reactjs.org/docs/composition-vs-inheritance.html#containment)的一个经典例子，其中一个具有`left`和`right`属性的组件将这些值添加到主组件中。虽然这种方法可行，但它为其他开发人员创建了一个笨拙的界面，尤其是如果整个组件树必须适合这些属性中的一个。

构建布局组件时，另一种方法是将组件与上下文耦合在一起，使用子组件来填充父组件:

在这种模式下，组件不输出任何内容，而是将其内容存储在父组件中。由父组件输出这些内容。您最终会像这样使用组件:

注意，`<Header/>`、`<Footer/>`和`<Sidebar/>`可以出现在`<Layout/>`的任何地方，嵌套的深度不限，顺序不限。(如果你想的话，你甚至可以把它们嵌入到彼此之中，但是……为什么呢？)只要他们在`<Layout/>`里面，就会按预期表现。

**注意:**您必须更新效果中子组件的内容。由于渲染的工作方式，在渲染时让子级设置父级的状态会导致内存泄漏。

对于那些担心过度渲染的人来说，这将为 *n* 个耦合的子组件渲染并协调 DOM *1 + n* 次。第一次渲染渲染并协调子组件，包括耦合组件，但是耦合组件返回`null`，不管它们的子组件是什么，所以开销很小。然后运行每个子组件的布局效果，更新父组件状态。这些都会导致父对象再次单独渲染和解析。

如果在一个页面的很多地方使用，这可能会很昂贵。我建议这种模式只使用非常少量的耦合子组件——一个或两个，最多三个。

如果耦合组件的子组件频繁更改，这也会很昂贵。幸运的是，只有当您有条件地将组件呈现为直接子组件时，或者当您在没有给元素提供有意义的键的情况下遍历元素时，子组件结构通常才会改变。子组件属性可以在不改变实际子结构的情况下改变。

但是好的一面是，在这个组件的生命周期中，上下文不会改变。设置器不会改变，所以带备忘录的上下文值也不会改变。

# 记住你复杂的钩子结果。

如果你向其他团队和开发人员提供钩子，并且你的钩子返回对象或数组，那么在返回之前一定要记住结果。您可能会假设其他开发人员会传播结果或立即使用它们，但是如果他们决定在依赖数组中使用返回的结果，他们的组件可能会遇到无限的呈现循环。

一个经典的例子与使用上下文有关。假设开发人员有一个简单的组件，它提供了通过上下文全局获取和设置状态的能力，还有一个钩子，它提供了对上下文的简单访问:

这相当简单，但是看看如果我们创建一个简单版本的`useGetterAndSetter`会发生什么:

(没错，这就是超级幼稚。我相信在现实生活中，从一个钩子返回的值会更复杂。)

如果这个钩子的消费者传播结果独立使用`state`和`setState`，一切都好。但是`GlobalStateProvider`不传播。它使用整个数组作为其上下文提供者的值。这意味着，每次`GlobalStateProvider`渲染时，每个使用`useGlobalState`的组件也会渲染，即使`state`从未改变。

如果`useGetterAndSetter`在我们的组件内部，并且我们可以在被`GlobalStateProvider`使用之前记忆结果，那就很好。但是如果它要在任何地方使用，我们需要记住它的结果:

这确保了每次`state`相同时`useGetterAndSetter`返回相同的值，如果返回值的标识很重要，这将是至关重要的。

注意，React 的`useState`钩子返回的数组是*而不是*内存化的。(我想在每个使用`useState`的实例上都要做很多工作。)这意味着，即使您可以确信状态设置器不会触发依赖关系更改，但是将整个数组用作依赖关系将导致每次呈现的依赖关系更改。

就是这样！(至少，现在想到的就是这些。)从地图和功能组合的角度考虑，让用户覆盖你的默认设置，并注意你如何引用和返回东西。这些将有助于你制造出其他人乐于使用的组件。

附注:我不太喜欢使用 TypeScript，尽管我知道它对于定义接口和帮助 IDE 创建建议非常有用。我是 TypeScript 的粉丝，但我没有足够的能力来说任何有启发性的东西。如果你能做出好的类型和接口，你的库用户会喜欢你的。