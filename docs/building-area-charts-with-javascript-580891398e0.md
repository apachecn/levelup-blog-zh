# 用 JavaScript 构建面积图

> 原文：<https://levelup.gitconnected.com/building-area-charts-with-javascript-580891398e0>

![](img/7d15312eb2d55d1caf561d91fc33c901.png)

如果您对数据可视化感兴趣，您可能经常需要做的事情之一就是表示一个变量随时间的值。或者，您可能需要比较多个数据集在特定时期内的变化情况。这就是面积图有用的地方。

不确定如何构建优雅的面积图？现在你将掌握一个非常简单的方法！在这个循序渐进的教程中，我们将使用 JavaScript 在交互式区域图表中可视化美国和俄罗斯过去二十年的军事预算数据。上船啦

# 什么是面积图？

面积图是数据的图形表示，显示一个或多个数据集的数值相对于第二个变量(通常是时间)的变化情况。

面积图类型是由威廉·普莱费尔于 1786 年引入的，他也被认为是折线图、条形图和饼图的发明者。它由一条线条组成，底层区域用一种颜色填充。在多系列面积图中，可以想象，有几条线带有阴影面积。

# 将创建的面积图

在本教程中，首先，我们将绘制美国从 2000 年到 2020 年的军事预算。然后，我们将通过添加俄罗斯联邦的同类数据，将单系列 JS 面积图转换为多系列。

看看最终的基于 JavaScript 的面积图会是什么样子，它显示了两国在过去二十年中为国防目的花费了多少亿美元:

![](img/0e43bced7feab0c614f93c26fee5dd6b.png)

面积图 JS 多系列最终

# 如何建立一个基本的 JS 面积图

从头开始构建交互式面积图可能会令人生畏且耗时。但是有很多有用的 [JavaScript 图表库](https://en.wikipedia.org/wiki/Comparison_of_JavaScript_charting_libraries)会很有帮助。实际上，无论您使用哪一个，创建任何基于 JS 的图表的整个过程，包括我们的面积图，都可以分为四个基本步骤:

1.用 HTML 创建一个基本的网页。

2.添加所需的 JavaScript 文件。

3.加载数据。

4.写一些 JavaScript 代码来画图表。

作为本教程中的一个示例，我选择了 [AnyChart](https://www.anychart.com/) 。这个 JavaScript 库看起来不难上手，因为有相当全面的[文档](https://docs.anychart.com/)和许多[示例](https://www.anychart.com/products/anychart/gallery/)，并且对于任何非商业用途都是免费的。

虽然这不是必需的，但是 HTML、CSS 和 JavaScript 的一些背景知识将有助于更快地理解这些概念。但是即使你是一个完全的初学者也不用担心。我们将详细介绍每个步骤，到本教程结束时，即使您是一个编码经验有限的新手，您也已经学会了构建 JS 面积图。

## 1.用 HTML 创建一个基本网页

我们需要做的第一件事是为面积图创建一个基本的 HTML 页面。我们将其命名为“JavaScript 面积图”

在这个页面上，我们添加了一个 HTML 块元素，`<div>`。我们给它一个惟一的 id 属性“container ”,这样我们可以在后面的代码中引用它。

我们还在`<style>`块中添加了一些 CSS 规则，以在整个屏幕上显示我们的图表，并将`width`和`height`属性定义为 100%,将边距和填充定义为 0。你可以根据自己的需要随意定义。

## 2.添加所需的 JavaScript 文件

接下来，我们需要在`<head>`部分添加图表库的 JavaScript 文件。我们既可以在本地下载，也可以使用 CDN(内容交付网络)。

对于本教程，让我们从 [AnyChart CDN](https://cdn.anychart.com/) 添加必要的脚本文件。AnyChart 有一个模块化的结构，这使得只连接我们目前需要的图表类型和特性变得很容易，减少了运行 JavaScript 代码的大小。

例如，对于面积图类型，我们可以只包含一个[基本](https://docs.anychart.com/Quick_Start/Modules#base)模块。

我们的 HTML 现在可以看起来像这样。

## 3.加载数据

如前所述，我们将可视化军事预算数据，并从美国的 JavaScript 面积图开始。我在 [Statista](https://www.statista.com/statistics/272473/us-military-spending-from-2000-to-2012/) 上找到了一个合适的数据集。

为了正确地将数据加载到图表中，我们创建了一个[数组](https://docs.anychart.com/Working_with_Data/Data_Sets#array_of_objects)，其中数组的每个元素由两个元素组成。第一个是年份，第二个是美国的军事预算，以十亿美元计。

例如，在 2000 年，美国的军事预算是 3200.9 亿美元。所以，我们的第一个数组变成了`[“2000”, 320.09]`。

## 4.写一些 JavaScript 代码来绘制图表

现在，只需几行 JavaScript 代码就可以启动并运行我们的区域聊天。

我们在这里做的第一件事是添加`anychart.onDocumentReady()`函数，它将包含面积图的全部 JavaScript 代码。这确保了在页面完全加载之前不会执行代码。

接下来，我们添加步骤 3 中的数据。

然后，我们创建图表，将图表类型指定为“area ”,并添加数据。

最后，我们添加一个标题，将图表放入之前定义的`<div>`容器中，并使用`draw`命令显示它。

找到了。我们的面积图准备好了。

![](img/83647b938f8a409e13c29e7856c8d80d.png)

对比图

可以在 [AnyChart 游乐场](https://playground.anychart.com/dcAQZsCK/)找到这个基本 JavaScript 面积图的交互式版本及其完整代码。你可以随意摆弄它。

为了您的方便，我把完整的代码放在下面。

实际上，这只是面积图的一个基本的单系列版本。现在，让我们添加第二个系列。

# 如何创建多系列 JS 面积图

用 JavaScript 构建多序列面积图也没什么大不了的。对我们来说，只需要三个简单的步骤就可以将我们的单系列面积图变成多系列面积图。

## A.添加数据

首先，让我们将俄罗斯的军事预算数据添加到数组中。同样，我们使用来自 [Statista](https://www.statista.com/statistics/1203160/military-expenditure-russia/) 的数据集。现在，每一行将由三个元素组成:年份、美国的值和俄罗斯的值。

例如，2000 年，美国和俄罗斯的军事预算分别为 3200.9 亿美元和 92.3 亿美元。所以，我们的第一个数组变成了`[“2000”, 320.09, 9.23]`。

## B.映射数据

其次，让我们利用 AnyChart 的便利的[数据集](https://docs.anychart.com/Working_with_Data/Data_Sets)特性:我们将从数据中创建一个数据集，然后为每个系列映射它:

## C.配置系列

最后，我们用映射的数据创建系列，并给它们命名。

就这样，一个很酷的基于 JavaScript 的多系列面积图已经准备好了，提供了美国和俄罗斯在同一地块上的军事预算的长期视图。

![](img/1854ea005a7ab497a6049d8370e1a754.png)

面积图 JS 多系列

在 AnyChart 游乐场上探索它的完整代码。

我们的面积图已经很不错了。但是有时候，好是不够的。而且，有时您可能需要调整图表的功能和美观。现在，让我们做更多的工作，看看如何定制这样的图形，使它们看起来更好。

# 如何自定义 JavaScript 面积图

幸运的是，AnyChart 支持的 JavaScript 图表可以很容易地修改，以满足您的需求和偏好。

我将向您展示如何进行一些快速定制来增强我们的图表:微调 X 刻度、添加十字准线、更改区域的颜色、添加图例和轴标题，以及配置悬停模式。

## 微调 X 标尺

从一个快速的调整开始会很棒——去掉这个区域左右两边的空白。我们只需为 X 标尺设置“连续”模式。

![](img/8438b4e575a3fe784a1979241ba7ea3e.png)

面积图 JS 多系列刻度

## 添加十字准线

十字线有助于快速理解悬停数据点的 X 和 Y 值。在我们的例子中，让我们只留下一个垂直的十字准线。

![](img/77b3fcd7528ec840e10eca11520e5684.png)

面积图 JS 多系列十字准线

短短几行 JS 代码，就有了我们的十字线，让面积图更有美感。

## 更改区域的颜色

根据我记得的一项研究，在一个十人小组中，每四个人都有蓝色作为他们最喜欢的颜色。但这并不意味着我们要保留图表的颜色，默认情况下是蓝色。

让我们把美国系列涂成红色，把俄罗斯系列涂成棕色。

这里，我们添加了`fill`和`stroke`方法来改变面积图的颜色。还有许多其他的[外观设置](https://docs.anychart.com/Appearance_Settings)，可以应用到你可视化的不同[状态](https://docs.anychart.com/Common_Settings/Interactivity/States)。

![](img/472bd5736d85c8f6ed49259c3e0449e5.png)

面积图 JS 多系列十字线定制

该面积图的互动版可在 [AnyChart 游乐场](https://playground.anychart.com/FfFrlNXs/)获得。随意换颜色看看:“*蝴蝶，蝴蝶，你喜欢哪种颜色？”*

## 添加图例和轴标题

我们可以用一行代码为 JavaScript 面积图添加一个图例。

类似地，我们可以很容易地为轴提供标题。在我们的图表中，X 轴是年份，Y 轴是以十亿美元为单位的军事预算数字。

这就是我们基于 JS 的面积图现在的样子，带有图例和轴标题。

![](img/b4f10765d5543bc0de921babcec58134.png)

面积图 JS 多系列坐标轴标题

## 配置悬停模式

目前，当我们将鼠标悬停在图表上时，对应年份的两个系列的数据点都用标记突出显示。但是如果我们想把他们分开呢？

让我们启用“单个”悬停模式，然后当您悬停在某个区域上时，将只显示该特定系列的标记。

当我们处于“单个”悬停模式时，十字准线没有多大意义。因此，为了配置悬停模式，我们可以删除或注释掉我们在本教程的“添加十字准线”部分中编写的代码。

![](img/0e43bced7feab0c614f93c26fee5dd6b.png)

面积图 JS 多系列最终

查看下面这个最终的交互式 JavaScript 区域图的全部代码，也可以在 [AnyChart 游乐场](https://playground.anychart.com/XzGpeUU6/)上查看。请随意尝试一些实验。

# 结论

厉害！我们已经构建了 JavaScript 面积图。过程很简单，不是吗？继续构建您自己的基于 JS 的区域图可视化。

请不要犹豫，看看[面积图文档](https://docs.anychart.com/Basic_Charts/Area_Chart)，还有成吨的其他[图表类型](https://docs.anychart.com/Quick_Start/Supported_Charts_Types)，你可能想看看。

最后，请随意问我任何问题或提出建议。迫不及待地想看到您将构建的 JavaScript 面积图。