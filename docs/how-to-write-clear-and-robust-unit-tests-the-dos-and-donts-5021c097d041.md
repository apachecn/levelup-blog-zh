# 如何编写清晰和健壮的单元测试:该做什么和不该做什么

> 原文：<https://levelup.gitconnected.com/how-to-write-clear-and-robust-unit-tests-the-dos-and-donts-5021c097d041>

![](img/dd2285aff28472f8131dee9e6d87854e.png)

**来源:** [**awmleer**](https://unsplash.com/@awmleer)

这篇文章涵盖了编写清晰和健壮的单元测试的一些最佳实践。该做什么，不该做什么，以及介于两者之间的一切。

先说一个问题；单元测试增值意味着什么？价值可以从许多不同的方面获得。

*   *:仅仅通过单元测试不足以给你信心，因为你知道测试正在进行`true.Should().Be(true)`；为了让你放心，测试也必须在应该失败的时候失败。*
*   ****省时测试*** :有些代码很难手工测试，尤其是考虑到难以到达的边缘情况。在项目生命周期的过程中，让单元测试通过，而不需要您做这些繁重的工作，可以为您节省不可估量的时间。*
*   *文档*:这将在下面详细介绍，但是单元测试在记录应用程序的预期行为方面有很大的作用，并且可以帮助其他不太熟悉应用程序某些领域的开发人员了解其中的细微差别。**
*   *****代码质量*** :测试驱动开发(TDD)被证明可以提高代码的可读性和结构，正如[这篇文章](https://theqalead.com/general/statistics-studies-benefits-test-driven-development/)更详细地解释的那样。现在，我更喜欢从头开始写代码，失败的测试已经指向了它。这可能是因为在开发过程中把红叉变成绿勾的行为非常令人满意，但这也让我可以满怀信心地编写代码，因为我已经准备好了安全网。**

**下面的例子使用了`XUnit`测试框架。如果你对这个库不熟悉，`NUnit` / `MSTest`在他们的 API 中肯定会有对应的库。**

**事不宜迟，让我们从单元测试的该做和不该做开始。**

# **务必将测试安排到“安排”“行为”“断言”(必须)中**

**也称为“AAA”模式，这在单元测试开发中已经变得司空见惯，并帮助不太熟悉单元测试读写测试的人。它包括将测试分为三个部分:**

1.  ****安排**:设置你的数据和参数，允许被测代码为你的特定场景执行。**
2.  ****动作**:用安排好的参数在测试下执行你的代码。**
3.  ****断言**:通过检查测试名称中描述的行为来验证预期结果。**

**您是否明确地将测试方法分离成带有`//Arrange`、`//Act`、`//Assert`的注释是可选的。在我看来，如果你的测试足够简洁，多重换行符也可以在视觉上分割这个方法:**

```
**[Fact]
public async Task Order_status_is_updated_to_accepted() 
{
    var orderToAdd = new Order { Status = OrderStatus.New };
    await _context.Orders.AddAsync(orderToAdd);
    await _context.SaveChangesAsync();
    var orderId = orderToAdd.Id; var request = new AcceptOrderRequest(orderId);
    await _acceptOrderService.ExecuteAsync(request); var updatedOrder = await _context.Orders.FindAsync(orderId);
    updatedOrder.Status.Should().Be(OrderStatus.Accepted);
}**
```

**对于这个例子，我们*通过建立一个测试订单来安排*我们的测试数据，执行我们的服务来接受订单( *act* ),并且*断言*订单状态根据方法的名称被更新。**

**微软也是这种结构的倡导者，正如他们的[单元测试文档](https://learn.microsoft.com/en-us/visualstudio/test/unit-test-basics?view=vs-2022#write-your-tests)中所概述的。**

# **务必使测试原子化(必须)**

**简而言之，测试应该能够独立运行，或者以任何顺序运行。当你开始思考如果不是这样，生活会是什么样子，以及维护这样一个单元测试库所需要的工作，你可以想象这将是多么具有挑战性。不自动运行的单元测试可能非常脆弱，并且可能在不合适的时候意外失败。**

**原子单元测试通常是有希望的，但有时它们的编写方式会导致它们无法实现。避免在测试之间共享状态，例如为所有测试全局插入数据，因为这通常是测试不是原子的主要原因。在这一节中，我们将介绍一些常见的陷阱。**

# **测试中未设置必需的数据**

**以下测试使用硬编码 id，而不是在测试的`arrange`部分设置数据:**

```
**[Fact]
public async Task Order_status_is_updated_to_accepted() 
{
    var orderId = 5; var request = new AcceptOrderRequest(orderId);
    await _acceptOrderService.ExecuteAsync(request); var updatedOrder = await _context.Orders.FindAsync(orderId);
    updatedOrder.Status.Should().Be(OrderStatus.Accepted);
}**
```

**这是一个单元测试的例子，不保证能够单独通过，因为我们已经假设了 id 为`5`的订单的存在。如果这个测试没有将订单插入数据库本身(或者作为测试初始化的一部分)，它将失败。相反，如果另一个测试从数据库中删除一个订单，该订单可能有也可能没有 id`5`，它也将失败。**

# **其他测试会改变你所依赖的数据**

**对于这个测试，关键的区别在于`act`中，我们基于属性进行查询，而不是特定于在`arrange`中设置的实体。**

```
**[Fact]
public async Task Order_status_is_updated_to_accepted() 
{
    var orderToAdd = new Order { Status = OrderStatus.New };
    await _context.Orders.AddAsync(orderToAdd);
    await _context.SaveChangesAsync();
    var orderId = orderToAdd.Id; var request = new AcceptOrderRequest(orderId);
    await _acceptOrderService.ExecuteAsync(request); var updatedOrder = await _context.Orders.SingleOrDefaultAsync(ord => ord.Status == OrderStatus.Accepted);
    updatedOrder.Status.Should().NotBeNull();
}**
```

**这是一个不保证能够以任何顺序通过的单元测试的例子，因为我们已经假设数据库中只有一个状态为 accepted 的订单。如果您正在使用共享的数据库上下文，并且编写了另一个测试，将一个接受的顺序插入到数据库中，那么这个测试将通过或失败，这是测试运行顺序的直接结果。要解决这个问题，直接使用`orderToAdd`的 id 从数据库中检索`updatedOrder`，就像第一个例子一样。**

# **工作区**

**如果采用不能自动运行测试的代码库，最好的办法是手动指定它们运行的顺序。大多数单元测试框架都支持这一点(例如 XUnit 的`ITestCaseOrderer`)。请记住，这应该是达到目的的一种手段，不覆盖顺序的原子单元测试应该是目标。**

# **务必使用方法名来记录您的应用程序逻辑(必须)**

**关于单元测试在记录代码库行为中所扮演的角色，已经说了很多。例如，如果`AddUserServiceTests`有一个名为`Returns_error_if_email_address_already_exists`的测试，我不用看实际的服务就知道系统的预期行为是强制用户电子邮件地址的唯一性。**

**即使对于最资深的开发人员来说，恰当地命名事物也是最难做到的事情之一，当你编写*参数化测试*时，人们通常会陷入这个陷阱。假设我们正在测试以下内容:**

```
**public static class OrderExtensions
{
    public static IsOpen(this Order order) => order.Status <= OrderStatus.Processing;
}**
```

**下面的单元测试的名字不是描述性的，也没有告诉我们任何关于领域逻辑的事情:**

```
**[Theory]
[InlineData(OrderStatus.New)]
[InlineData(OrderStatus.Accepted)]
[InlineData(OrderStatus.Processing)]
public void Order_is_open_works_correctly(OrderStatus status) 
{
    var order = new Order { Status = status }; var actual = order.IsOpen(); actual.Should.Be(true);
}**
```

**方法名告诉我们的并不比我们知道的测试是通过还是失败更多。测试方法名称应该是描述性的*，所以`correctly`这个词在这个上下文中没有意义。下面的方法完全相同，但其名称包括预期的应用程序行为:***

```
***[Theory]
[InlineData(OrderStatus.New)]
[InlineData(OrderStatus.Accepted)]
[InlineData(OrderStatus.Processing)]
public void Order_is_open_is_true_based_on_status(OrderStatus status) 
{
    var order = new Order { Status = status }; var actual = order.IsOpen(); actual.Should.Be(true);
}***
```

***这个方法名提高了我们的理解，因为它告诉我们一个订单根据它的状态被视为 open。我们在这里遗漏了一个与之相反的测试`Is_open_is_false_based_on_status`，但希望这足以说明这一点。***

***作为最后一点，如果你认为你的参数化单元测试的方法名没有给出足够的清晰度或上下文，考虑将你的测试分解成每个状态的测试，即:***

*   ***`Is_open_is_true_if_status_is_new`***
*   ***`Is_open_is_true_if_status_is_accepted`***
*   ***`Is_open_is_true_if_status_is_processing`***

# ***在构建验证管道中包含单元测试运行(必须)***

***构建验证用于证明软件可以成功构建，而不需要部署到任何地方。它通常发生在发出拉请求的时候，以确保开发者没有添加任何会阻止软件发布的东西。***

***我们可以通过在同一管道中运行单元测试来更进一步，以确保开发人员不会无意中改变任何期望的应用程序行为。以这种方式运行它们还有一个额外的好处，那就是任何脆弱的单元测试很快就会被发现，因为您将比以前更频繁地运行它们。***

***这里的缺点是它增加了审查过程的额外时间，特别是如果运行单元测试需要特别长的时间。将这些非性能测试视为真正的性能问题，并像处理性能错误一样修复它们。作为最后的手段，考虑按计划运行它们来缓解这个瓶颈。***

# ***在你写代码之前一定要写测试***

***举个例子:研究证明，通读试卷有助于你的大脑主动分解面前的任务，并下意识地开始思考你可能面临的问题的解决方案。***

***根据我的经验，测试驱动开发(TDD)也是如此。在我写代码之前，写下我希望我的新特性如何表现，让我更快地考虑边缘情况，并帮助我以更清晰的方式构建代码。***

# ***通过写一个失败的测试来开始修复错误(必须)***

***你不仅仅应该为新特性编写单元测试。可以说，遗留代码对于单元测试来说更加重要，因为文档练习无疑会帮助其他开发人员理解代码的预期目的。***

***通过问自己“我能为此编写一个失败的单元测试吗？”来开始修复你的 bug。如果 bug 违反了预期的应用程序行为，您可以相当确定它的重现不在单元测试的覆盖范围内，甚至可能发现了以前没有想到的边缘情况。***

***带着失败的意图编写测试起初看起来很奇怪，但这与 TDD 没有什么不同，因为在你让代码做那件事之前，你正在编写一个概述代码*应该*做什么的测试。***

**一旦编写了单元测试，修复 bug 的行为就变成了通过测试的行为。**

# **仍然手工测试你的代码(必须)**

**为一个特性编写单元测试是一件好事，但并不能 100%确定它能按预期工作。如果应用程序因为一些不相关的原因而失败，那么通过单元测试又有什么用呢？要考虑的一些事情不能由单元测试来保证，比如性能、安全性、UX。**

# **模仿外部依赖(应该)**

**随着您继续向项目中添加单元测试，您最终会遇到测试依赖项的情况。这可能是注入到构造函数中的东西，为了构造测试中的代码，您必须设置它。**

**依赖关系可以有各种形状和大小，并且可以以两种方式分类:*内部*和*外部*。内部依赖是你可以控制的东西(例如，你可以改变代码库中的东西)，就像同一代码库中的数据库上下文一样。相反，外部依赖类似于第三方 API。默认的方法是在可能的情况下不要模仿，正如这篇堆栈溢出的博客文章更详细地解释的那样。但是，如果外部依赖发生变化或者突然变得不可用，您的测试可能会意外失败。因此，最好模仿这些，这样你的测试就不会受到超出你控制的东西的支配。**

# **不要测试随机信息(必须)**

**为了帮助说明这一点，这里有一个单元测试，它可能通过也可能失败，这是分配给`repairCost`变量的一个随机生成的数字的直接结果:**

```
**[Fact]
public async Task User_is_quoted_excess_if_repair_cost_exceeds_excess() 
{
    var job = new Job 
    { 
        Id = 5
        Excess = 500
    };
    var repairCost = new Random().Next(); var request = new GetJobRepairQuoteRequest 
    { 
        JobId = job.Id, 
        Cost = repairCost 
    };
    var result = await _service.Execute(request); result.Cost.Should().Be(job.Excess);
}**
```

**在这个例子中，我们不能保证修复成本会大于存储在任务中的超额成本。这意味着`new Random().Next()`可能会返回一个小于超出部分的数字，从而导致测试失败。**

**这一点并不禁止你使用随机信息，Audacia 甚至有一个扩展方法的[开源报告](https://github.com/audaciaconsulting/Audacia.Random)来帮助生成随机信息，只要你随机化的信息对测试结果没有影响。**

# **不要用`DateTime.Now`(必须)**

**使用当前的系统时间(`DateTime.Now`或`DateTimeOffset.Now`，或者任何相对于系统时间(`DateTime.Today`)的*都可能导致测试出现意想不到的结果。当您编写测试时，您是在特定的时间点编写的，不能保证在任何时间运行您的测试都会通过。这导致了与前面提到的使用随机信息类似的脆弱性，因为每次运行测试时，某些变量的值都会改变。如果这些变量对应用程序的行为有直接影响，你会发现它们不会 100%通过。***

**下面是一个使用当前系统日期时间的测试。**

```
**[Fact]
public void Tomorrow_is_one_business_day_away() 
{
    var dateToTest = DateTime.Today;
    var tomorrow = DateTime.Today.AddDays(1); var result = dateToTest.BusinessDaysUntil(tomorrow); result.Should().Be(1);
}**
```

**乍一看，这似乎很简单，您可能认为我们正在测试一个名为`BusinessDaysUntil`的扩展方法，该方法返回两个日期之间的营业天数(很像 excel 的`NETWORKDAYS`函数)。幸运的是，这个扩展方法带有一个`DateTime`参数，允许我们用任何给定的日期来测试它，而不是在方法本身内部使用`DateTime.Now`。**

**上述测试将在周末失败，即使实际上没有任何问题。相反，考虑使用固定的日期，或者在这个例子中，总是确保您测试的日期是工作日。**

# **不要为了写测试而写测试(必须)**

**并不是所有的单元测试都是有价值的，甚至在维护代码库时会造成比它的价值更大的伤害。每个单元测试都应该增加*值*，并且大部分的值来自于在测试人员/最终用户之前发现的东西。那么，为什么你要写一个测试，覆盖如此琐碎的事情，它总是会通过。为了帮助决定单元测试是否值得编写，请考虑单元测试将为您的应用程序增加的价值，以及编写和随后运行测试所花费的时间。**

**来自 google 的这篇博客讨论了代码覆盖率以及为什么 100%的代码覆盖率有时会导致错误的安全感。**

# **不要使用特定领域的常量进行测试(应该)**

**这个建议来自个人经验:我并不总是有这种方法，直到一个同事用这种方法写了一个单元测试。我最初的反应是，我们应该在我们的单元测试中使用这些“神奇的数字”，直到有人向我解释了他们为什么这样写测试，我将在下面进行讨论。**

**假设我们有一个常量文件，为一个名为`Item`的实体指定静态的特定于域的信息:**

```
**public static class ItemConstants 
{
    public const int MinValuablePrice = 1000;
}**
```

**考虑以下扩展方法:**

```
**public static bool IsValuable(this Item item) 
{
    return item.Value > ItemConstants.MinValuablePrice;
}**
```

**具体来说，如果一个物品的价格超过`1000`，则该物品被认为是有价值的。开发人员可以使用这个`MinValuablePrice`常量编写一个单元测试，如下所示:**

```
**[Fact]
public void Item_is_valuable_if_price_is_over_min_valuable_price() 
{
    var itemPrice = ItemConstants.MinValuablePrice + 1;
    var item = new Item { Price = itemPrice }; var result = item.IsValuable(); result.Should().BeTrue();
}**
```

**考虑这样一个场景，开发者将我们的常数变为零。如果不是有意的，这可能会给生产环境带来毁灭性的错误，除非单元测试失败并阻止代码被合并。通过上面的测试，开发人员可以做出这种改变，单元测试仍然可以顺利通过——这是我们不希望发生的。**

**考虑同样的测试，对变量`itemPrice`进行如下细微的调整:**

```
**[Fact]
public void Item_is_valuable_if_price_is_over_one_thousand() 
{
    var itemPrice = 1001;
    var item = new Item { Price = itemPrice }; var result = item.IsValuable(); result.Should().BeTrue();
}**
```

**以这种方式编写测试增加了一层额外的安全性，以确保不会无意中发布对应用程序行为的更改，并且在我们的测试中进一步解释了项目为`Valuable`的概念。请注意，方法名还包括常量的值，因为它可以被视为应用程序行为，因此当值改变时，测试开始失败的原因就显而易见了。**

# **像对待生产代码一样对待测试代码(必须)**

**由于单元测试项目很少在任何地方部署，开发人员在编写单元测试代码时可能缺乏同样的关心和注意。在所有其他条件相同的情况下，一些人可能不关心测试是如何编写的，只要它们能增加上述的价值。他们可能忘记了维护类似的编码标准的价值，就使你的单元测试更具可读性和自我文档化而言。**

**我在上面说“相似”的原因是，尽管你可以把它当作产品代码，但是在编写测试的过程中，有些事情可能需要执行不同的编码标准。一个很好的例子是 [RCS1046](https://github.com/JosefPihrt/Roslynator/blob/main/docs/analyzers/RCS1046.md) 分析器，它强制异步方法的名称以‘Async’作为后缀；在这种情况下，覆盖这条规则(例如用一个`.editorconfig`来覆盖)是可以接受的，这样你的方法名就可以继续描述应用程序的行为，我们没有像`public async Task My_descriptive_method_name_async()`这样命名的测试。虽然没有最终用户会接触到这些代码，但是你的开发伙伴们肯定会，并且只有在代码库可读和可理解的情况下才会愿意贡献。他们看到的`var stuff = ...`和`public void Does_the_thing()...`越多，他们这样做的可能性就越小。**

# **一致的测试方法**

**在这篇文章中，我们介绍了编写和维护单元测试的最佳实践。这里提出的所有观点都不是一成不变的规则，每一点肯定都会有警告。为不太熟悉单元测试的开发人员定义最佳实践，可以实现一致的测试方法，并降低单元测试在以后成为更多障碍的可能性。**

**在 Audacia，我们坚持高水平的单元测试，并不断分享新的方法和技术来帮助我们做到这一点。**

**本文由 Audacia 首席顾问欧文·莱西撰写。Owen 曾作为一名开发人员在多个行业工作过，包括制造、汽车维修和无代码开发。除了开发，他还监督许多项目的交付，并参与更高级功能的咨询，如机器学习和[谷歌或工具](https://audacia.co.uk/technical-blog/problem-solved-implementing-or-tools-routing-part-1-of-3?utm_source=Medium+&utm_medium=BacklinkSubmission&utm_campaign=Tech_Blog+)。**

**[Audacia](https://audacia.co.uk/) 是一家总部位于英国的软件开发公司，总部位于利兹。在我们的[技术洞察博客](https://audacia.co.uk/technical-blog?utm_source=Medium+&utm_medium=BacklinkSubmission&utm_campaign=Tech_Blog+)上查看我们的顾问、业务分析师、开发人员和测试人员团队的更多技术洞察。**