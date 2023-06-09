# 测试 React 组件:酶与 React 测试库

> 原文：<https://levelup.gitconnected.com/testing-react-components-enzyme-vs-react-testing-library-3d0671a90093>

![](img/120be1fca813185c4dfa9318b2164ea6.png)

在[的上一篇文章](/build-your-own-unbeatable-tic-tac-toe-with-react-hooks-and-styled-components-6f36a6dcb8cc)中，我们用 React 钩子和风格化组件构建了一个井字游戏。然而，它缺少了开发过程中的一个关键部分——测试。在这篇文章中，我们将通过向 **TicTacToe** 组件添加测试来修复这个遗漏。此外，这似乎是比较两个最流行的 React 测试工具的好机会— [Enzyme](https://github.com/airbnb/enzyme) 和 [React 测试库](http://github.com/testing-library/react-testing-library)。提醒一下，游戏的最终版本可以在[这里](https://clarity-89.github.io/React_tic_tac_toe/)找到，代码可以在 [Github](https://github.com/Clarity-89/React_tic_tac_toe) 上找到。

这种比较的目的不是试图决定哪种框架是最好的，而是为了说明他们方法的不同。首先让我们安装软件包。

```
npm i -D enzyme enzyme-adapter-react-16 @testing-library/react @testing-library/jest-dom
```

接下来，我们将在`src`目录的根目录下创建`__tests__`文件夹。我们将使用 [Jest](https://jestjs.io/) 来运行测试，它预装了 create-react-app，用于 Tic Tact Toe 游戏。在这里我们添加两个文件，每个测试框架一个:**tictactoe . enzyme . test . js**和 **TicTacToe.rtl.test.js.**

## 反应测试库

从 React 测试库开始，在 **TicTacToe.rtl.test.js** 中，我们将介绍一个基本设置并编写第一个测试。但在此之前，我们需要回到 **TicTacToe.js** 做一个小小的修改，即给每个方块加上`data-testid`。

这个`testid`是 React 测试库用于查询 DOM 元素的特殊属性。

如果你还记得以前的教程，当游戏开始时，玩家看到**选择你的玩家**屏幕。我们在这里通过选择 **X** 做出选择，并验证网格是否以正确的方块数呈现。注意，我们也可以通过部分匹配获得条目，使用正则表达式语法—`getAllByTestId(/square/)`—返回所有在`testid`属性中包含`square`的条目。该库有大量关于可用查询类型的文档。

**测试异步动作**

接下来，让我们验证一下，当我们点击一个空的方块时，那个玩家实际上走了一步。此外，我们可以测试计算机下一步行动。

在触发点击第一个方块后，我们成功验证了方块的文本内容是 **X** 。为了使用`toHaveTextContent`和其他一些有用的 Jest 匹配器，我们需要安装并导入 [Jest-dom](https://github.com/testing-library/jest-dom) 包。

玩家移动后，我们会测试电脑是否也移动了。在游戏组件中，由于`setTimeout`的原因，电脑移动会有轻微的延迟，所以结果会异步呈现在屏幕上。在这种情况下，我们将使用返回承诺的`findByText`查询，当找到与给定查询匹配的元素时，该查询将被解析。基本上它是`waitFor`和`getBy*`查询的组合。此外，由于我们使用的是`await`，我们的测试函数必须是`async`。

请注意，尽管测试通过了，您可能仍然会在控制台中得到一个类似于`Warning: An update to TicTacToe inside a test was not wrapped in act(...)`的警告。这是因为在 React 16.9.0 之前,`act`测试工具只支持同步功能。因此，为了摆脱警告，只需更新反应到最新版本。如果你对这个问题本身感到好奇，在 Github 上有一个冗长的讨论。

接下来，我们将测试当玩家点击一个非空方块时，移动不会有任何影响。在这一点上，很明显我们需要写一些相同的代码来使人类玩家移动，然后等待计算机移动。当我们想测试最终游戏时会发生什么？我们要把所有的动作都编码到棋盘上吗？这听起来不像是一种有效的消磨时间的方式。相反，让我们修改 **TicTacToe** 组件来接受一个可选的网格，我们可以使用它来测试将游戏快进到任何状态。我们称它为`squares`(我在这里已经没有名字了，因为*网格*和*板*已经被占用了)，它将默认为我们之前声明的`arr`。

现在，当渲染组件进行测试时，我们可以提供一个带有预填充值的网格，所以我们不需要手动设置它们。有了这个设置，我们可以很容易地测试出移动到同一个方块并改变它的值是不可能的。

为了使这个测试套件更加全面，我们还需要测试两件事情:

1.  当有赢的组合或平局时，显示结果的模式。
2.  按下**重新开始**按钮开始新游戏并显示初始屏幕。

对于第一个场景，我们将提供离游戏结束还有一步的网格状态，然后通过这一步我们测试游戏是否正确结束。

为了完整起见，我们正在测试所有 3 个可能的结局场景。请注意，网格的格式与游戏的网格相同，因此更容易看到游戏的状态。如果你使用[更漂亮的](https://prettier.io/)进行代码格式化，你可以用`// prettier-ignore`禁用它，以保持自定义格式。

请注意，在最后一个测试中，我们设置了一个棋盘，这样在人类玩家移动后，留给计算机移动的两个选项都将使它获胜。我们不必明确地等待轮到计算机，而是等待模态出现，这应该发生在最后一步棋之后。

作为最后的测试，我们确认游戏在按下**重新开始**按钮后重置。

完成后，我们有了一个很好的综合测试套件，我们使用了 React 测试库，并以最终用户与之交互的相同方式测试了游戏。

## 酶

现在我们将从最终用户的角度用 Enzyme 来测试这个游戏。我们首先将**tictactoe . enzyme . test . js**文件添加到`__tests__`文件夹中。在编写实际的测试之前，我们需要做一些设置，即配置 React 的酶适配器。

确保使用与 React 当前版本相同版本的适配器。在初始设置之后，我们可以开始编写测试。让我们遵循与 React 测试库相同的路径，验证游戏在选择玩家后以正确大小的网格开始。

从第一次测试可以明显看出，用酶测试组件，就像我们用 React 测试库一样，会更有挑战性。首先，我们需要使用强大的`findWhere`方法来查找带有特定文本的项目。还需要检查它实际上是一个按钮，这样我们就不会捕捉到任何包装组件。然后，为了获得`Square`组件，我们需要首先[覆盖它们的显示名称](https://github.com/styled-components/styled-components/issues/896#issuecomment-332348516)。

我们也可以通过组件引用来找到它们，但是在这种情况下，我们必须导出`Square`组件并直接将其导入到测试中。另一个选择是使用类似于`wrapper.find('div[data-testid^="square"]`的查询，来匹配以“square”开头的测试 id，其中`^=`用于匹配部分属性，然而这看起来一点也不漂亮。

我们在这里也使用了`mount`而不是`shallow`，它对组件及其子组件进行完整的 DOM 渲染，这在我们需要研究我们的样式组件时非常有用。

按照与使用 React 测试库时相同的测试结构，我们现在将验证玩家的移动是否被正确渲染。

既然可以通过显示名称选择样式化的组件，那么使用`at`选择器就可以很容易地获得特定索引处的组件。之后，我们可以使用`text()`方法断言其文本内容是正确的。

还有一件事:看起来我们将在相当多的地方使用我们的详细按钮查找方法，所以让我们把它转换成一个实用函数。

在这之后，我们可以用更少的代码通过特定的文本得到按钮。让我们继续检查玩家是否不能移动到被占领的方格。

**测试异步动作**

测试通过了，所以我们都很好。接下来，我们将检查所有的残局组合是否被正确处理。

用酶测试异步组件的作用被证明是一个相当大的挑战。首先，我们需要将显示名称 prop 添加到模态内容组件:`ModalContent.displayName = "ModalContent";`因为我们不仅要测试状态是否正确更新，还要测试状态本身是否在超时后被设置，所以我们需要利用 Jest 的`useFakeTimers()`方法来模拟组件中使用的计时器。为了手动运行这些定时器，我们将使用来自 React TestUtils 的`act`函数中的`runAllTimers()`。此外，我们需要再次触发计时器来计算计算机的移动，并最终调用 Enzyme 的`update`方法来强制组件重新渲染，确保状态得到更新。

**提示:**如果您在确定测试不应该失败的时候还在想为什么测试会失败，Enzyme 的包装器有一个方便的`debug()`方法，它可以打印出呈现在 DOM 中的组件。可以这么用- `console.log(wrapper.debug()).`

最后的测试是断言游戏正确重启。

## 结论

我们看到，用酶和 React 测试库测试 React 组件，而不需要了解太多实现细节是可能的。由于它的设计，用酶来做更有挑战性。对于酶，我们仍然通过它们的名称来获取成分，如果这些名称在未来发生变化或者成分被移除，我们的测试将会中断。此外，随着开发人员远离基于类的组件，许多 Enzyme 的测试类实例的方法不再有用，因为它们不适用于功能组件。

然而，仍然有可能用酶进行全面的测试。我个人已经开始用酶测试 React 组件，但是由于上面提到的原因，现在我更多地转向 React 测试库。最终，您的选择将取决于个人偏好和测试组件的结构。

希望本文通过举例说明两个最流行的框架的应用，使选择测试 React 组件的框架的任务变得更容易。

对这篇文章有任何问题/评论或其他类型的反馈吗？请在下面的评论中或者在 [Twitter](https://mobile.twitter.com/Clarity_89) 上告诉我。