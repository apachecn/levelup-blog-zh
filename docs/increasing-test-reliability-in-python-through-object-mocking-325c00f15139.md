# 通过对象模拟增加 Python 中测试的可靠性

> 原文：<https://levelup.gitconnected.com/increasing-test-reliability-in-python-through-object-mocking-325c00f15139>

![](img/301968ad4a4ed5387c8a7f1d4f9944df.png)

由 [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在软件开发生命周期中，测试已经成为确保我们创建的软件满足用户需求和期望的最重要的活动之一。在软件发布供公众使用之前，测试在识别潜在问题方面起着至关重要的作用。因此，软件的测试套件足够可靠和有效是很重要的。

虽然也存在手动测试方法，但是一些测试是使用库自动进行的，这显著减少了每次测试所需的时间并增加了所述测试的可靠性。然而，自动化测试库通常由一组严格的指令组成，这带来了一些问题，例如:

1.  依赖于随机化或外部因素的程序可能会使任何此类试验在不断变化的条件下不可重复。
2.  依赖于其他程序的程序可能会因为其他程序的改变而破坏测试套件。

这些场景似乎否定了创建自动化测试套件的好处。由于测试套件很容易产生不可重复的结果，甚至完全崩溃，它不能被充分依赖，尤其是对于大型项目。然而，我们确实需要记住，最佳实践编程原则之一是**依赖倒置**(程序不应该/应该减少对具体实现的依赖)。

为了解决依赖问题，程序必须以这样一种方式来规划，即它依赖于一个抽象，而不是一个具体的实现。在 Java 和 Kotlin 等语言中，这很容易通过使用接口来实现，这些接口的实现可以在测试期间交换。然而，Python 并不了解接口。因此，Python 的内置测试库提供了一套方法来**在测试**中创建和使用 **模拟对象。**

# 创建模拟对象

模拟对象有助于减少被测程序对其他类/对象的依赖性。模拟对象可以站在所有对象的位置上(因为 Python 无论如何都不执行静态类型检查),并且可以模拟任何对象的行为。可以随意添加属性，也可以用特定的返回值配置对象方法，所有这些都不需要定义或使用实际的对象本身。这些专长可以通过 Python 中`unittest.mock`模块下的 **Mock** 类来实现。

```
from unittest.mock import Mockmock_object = Mock()
```

重要的是要注意，模拟对象不需要模拟特定对象的所有方面，以便能够在该对象的位置上使用。我们只能模拟测试程序所需的方面。

让我们以 Django 中的一个 HttpRequest 对象为例。下面的方法是一个视图函数，用于创建用户和他/她正在处理的项目之间的关系:

在这种情况下，所需的输入只是用户的 ID 和帐户类型(包含在`request`有效负载中)以及项目的 ID(通过`registration_data`参数包含在请求体中)。因为用户的 ID 和帐户类型是从传递给这个函数的 HttpRequest 对象中获得的，所以这个函数的任何测试要么必须提供这个对象，要么必须找到模拟它的方法。

仅供参考，HttpRequest 对象是一个复杂的对象，它包括客户机用户代理、IP 地址等属性。我们在测试这个功能的时候不需要这样的属性。我们只需要对象有适当的用户 ID 字段，它嵌入在`request.auth`字段中。因此，我们可以在请求对象的位置上使用模拟对象，只让特定的字段可用。结果如下所示:

```
request_mock = mock.Mock()
request_mock.auth = mock.Mock()
request_mock.auth.id = self.annotator_user.id
request_mock.auth.account_type = User.ANNOTATOR
```

在上面的模拟对象中，我们正在创建一个名为`request_mock`的模拟请求对象。在对象内部，我们使用另一个模拟对象注入`auth`字段，该对象稍后也由测试用户的 ID 和帐户类型注入。因为这是函数需要的唯一信息，所以我们不需要模仿任何其他字段，只需将对象作为函数的参数传递。我们现在可以执行测试，就像传递了一个实际的请求对象一样。

这种技术可以应用于任何对象，只要你确切地知道程序的哪一部分将被使用。在 Java 和 Kotlin 中，这些可以很容易地通过接口指定。然而，在 Python 中，开发人员提前计划对象用法的意识很重要。