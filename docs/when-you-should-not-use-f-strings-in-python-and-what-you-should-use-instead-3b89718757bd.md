# 在 Python 中什么时候不应该使用 f 字符串，而应该使用什么

> 原文：<https://levelup.gitconnected.com/when-you-should-not-use-f-strings-in-python-and-what-you-should-use-instead-3b89718757bd>

## 计算机编程语言

![](img/4e10c9f2c8bd6e7d42d905b265d10d38.png)

由 [Jacob Ferus](https://medium.com/@dreamferus) 使用 Midjourney 生成的图像。

自从在 Python 3.6 中引入 f 字符串以来，f 字符串变得非常流行，这是有原因的。既简单又简洁。这可以在与 Python 中的其他方法进行比较时显示出来:

在大多数情况下，使用 f 字符串是最干净的选择。也就是说，有些情况下使用`.format()`有好处。什么原因？简而言之 **:** `**.format()**` **可以与字符串解耦。**

让我举个例子来说明这一点。假设您有一个应用程序，其中模板用于各种类型的电子邮件、简历等。例如，其中一个模板可能如下所示:

> 亲爱的<receiver_name>，</receiver_name>
> 
> 我们感谢您对<company_name>的捐赠。我们将努力工作来完成…</company_name>
> 
> 最诚挚的问候，
> <公司名称>

在这里，我们在<>中有占位符，在每种特定情况下，这些占位符必须由公司和接收方名称来替换。现在，如果您想用 Python 构建这样一个应用程序，您会怎么做呢？

在括号中使用变量占位符是有意义的，例如`{variable_name}`，因为它用在 f 弦和`.format()`中。使用 f-string 的问题是变量会立即被当前作用域中的变量替换，因此存储模板变得更加复杂。

另一方面，使用`.format()`效果很好。让我们看一个例子:

可以看出，我们可以很容易地重用带有不同变量的模板，只需将它们添加到`.format()`中。还要注意的是，模板并不是某种内部带有占位符的特殊对象，**它只是一个普通的字符串。**这意味着无需额外工作即可轻松将其存储在任何持久存储中。例如:

# 的脆弱性。格式()

综上所述，`.format()`的一个问题是它不应该直接*应用于从*用户输入创建的模板*。例如，如果你有一个接受用户模板的 API。相反，您必须净化输入以确保没有漏洞。*

以下是这种滥用的一个例子:

因此，虽然它在开发人员创建模板或非用户交互应用程序时很有用，但在用户输入中使用它时必须小心。对于这些情况，有更好的选择吗？

# 用模板类处理用户模板

幸运的是，在您确实需要包含来自用户的模板的能力的情况下，并且不必经历额外的清理工作，可以使用**模板类**。它没有`.format()`灵活，但避免了注射。见下文:

和以前一样，这个类只需要一个可以存储在任何地方的普通字符串。

# 其他应用的例子

在前面的示例中，电子邮件被替换为适当的详细信息。以下是其他一些可以应用的例子:

*   格式化聊天机器人的答案
*   语言模型的格式化提示模板(例如 GPT-3)
*   按一天中的时间格式化邮件

感谢阅读！

如果您有兴趣阅读更多关于 Python 的文章，请查看我下面的阅读列表:

![Jacob Ferus](img/3fe8a4152942d124e84f4370bdeaa704.png)

雅各布·费罗斯

## 计算机编程语言

[View list](https://medium.com/@dreamferus/list/python-c8e4719d93da?source=post_page-----3b89718757bd--------------------------------)32 stories![](img/04c5beba0e198bb074b51dab1e99cea5.png)![](img/ddc10e2a657adb0dca6dc40fbab3ef74.png)![](img/c0376aaf2f82f915fbbb9e6f86a2c621.png)

如果你想成为中级会员，你可以使用我的[推荐链接](https://medium.com/@dreamferus/membership)。祝你有愉快的一天。