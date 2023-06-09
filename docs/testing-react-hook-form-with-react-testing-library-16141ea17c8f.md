# 用 React 测试库测试 React 钩子形式

> 原文：<https://levelup.gitconnected.com/testing-react-hook-form-with-react-testing-library-16141ea17c8f>

![](img/eb5ac59f3f4593ba47317bc1f54434d6.png)

在[之前的帖子](/managing-forms-with-react-hook-form-ae771dcf343d)中，我们使用 [React Hook 表单](https://react-hook-form.com/)添加了一个基本的食谱表单。为它添加一些单元测试将是一个好主意，以确保表单正常工作并捕捉任何未来的回归。我们将使用 [React 测试库](https://testing-library.com/docs/react-testing-library) (RTL)作为测试框架的选择，因为它与钩子形式配合得非常好，并且是测试它的推荐库。

像往常一样，让我们从安装所需的包开始。

```
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

除了测试库，我们还添加了 [jest-dom](https://github.com/testing-library/jest-dom) 来使用定制的 jest 匹配器。现在我们可以开始为 Recipe 组件编写测试了。让我们创建 **Recipe.test.js** 文件，并添加第一个测试，检查基本字段是否正确呈现。

熟悉 RTL 的人可能会注意到，我们在这里没有使用`getByText`查询，而是默认使用`getByRole`。后者更受欢迎，因为它更接近用户与页面的交互方式——既使用鼠标/视觉显示，也使用辅助技术。

这是使用 RTL 的一个特别有说服力的理由——如果编写代码时考虑到可访问性，那么在大多数情况下,`getByRole`查询就足够了。为了能够有效地使用`*ByRole`查询，有必要了解每个 HTML 元素有什么作用。在我们的表单中我们使用`h1`，它有**标题**角色，文本`input`和`textarea`有**文本框**角色，数字`input`有**微调按钮**角色，`button`有**按钮**角色。由于我们有多个具有相同角色的元素，我们可以使用`name`选项来缩小搜索范围并匹配特定的元素。需要注意的是，这不是我们赋予输入元素的**名称**属性，而是它们的[可访问名称](https://www.w3.org/TR/accname-1.1/)，辅助技术使用它来识别 HTML 元素。浏览器使用几个规则来计算可访问名称。

出于我们的目的，输入的可访问名称是从它的相关元素中计算出来的，在本例中，它是输入的标签。然而，要做到这一点，标签必须与输入正确关联，例如，输入被包装在标签中，或者标签具有与输入的`id`相对应的`for`属性。现在我们看到了具有可访问的表单是如何使测试变得更容易的。对于 button，如果没有`aria-label`或关联的`aria-labelledby`属性(优先于其他提供的和本机的可访问名称)，则可访问名称是使用其内容计算的。在这种情况下，需要**添加配料**和**保存**文本。此外，我们可以使用 regex 语法来匹配名称，这很方便，例如，对于不区分大小写的匹配。

现在我们已经完成了基础测试，让我们继续测试领域验证。在此之前，我们将通过添加`saveData` prop 来稍微修改表单组件，它将在表单提交时被调用。这样我们可以测试它是否被调用，并检查参数。

通常`saveData`会调用 API 将表单数据发送到服务器或进行一些数据处理。出于字段验证的目的，我们只对该函数是否被调用感兴趣，因为如果任何字段无效，表单的`onSubmit`回调就不会被调用。

我们通过提供无效数据一次性测试所有字段——没有名称、太长的描述和超过 10 的服务数量。然后我们提交表单，并检查错误消息的数量(呈现为`span`和`alert`角色)是否与出错字段的数量相同。我们甚至可以更进一步，检查特定的错误消息是否显示在屏幕上，但这似乎有点过分。由于提交表单会导致状态改变和重新呈现，我们需要使用`findAllByRole`查询和`await`来获取表单重新呈现后的错误消息。最后，我们确认没有调用模拟保存回调。

在我们开始测试整个提交表单流之前，最好验证一下是否正确地添加和删除了成分字段。同时，让我们花点时间来改进“删除配料”按钮的可访问性，该按钮目前看起来像这样:

HTML 字符`&#8722;`被用作减号`-`，从可访问性的角度来看，这远非最佳选择。如果我们能提供一个实际的文本来描述这个按钮的功能，那就更好了。为了解决这个问题，我们将使用`aria-label`属性。

这是更好的方式，加上现在我们可以很容易地在测试中查询特定的删除按钮。

我们继续使用类似的文本结构，并验证是否正确添加和删除了成分字段。值得注意的是，我们仍然可以使用`*ByRole`查询，只是在移除按钮的情况下`aria-label`现在是它的可访问名称。

最后是测试表单提交流程的时候了。为了测试它，我们填写所有的字段，提交表单，然后验证我们的`mockSave`函数已经被调用，并带有预期的值。

这里需要注意的是，我们使用`waitFor`实用程序来测试异步操作(提交表单)的结果。它将在异步操作完成后触发提供的回调。

现在我们有了一个相当全面的单元测试套件来验证表单的行为。

*最初发表于*[*【https://claritydev.net】*](https://claritydev.net/blog/testing-react-hook-form-with-react-testing-library/)*。*