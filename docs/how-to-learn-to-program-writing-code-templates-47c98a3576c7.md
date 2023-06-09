# 如何学习编程:编写程序模板

> 原文：<https://levelup.gitconnected.com/how-to-learn-to-program-writing-code-templates-47c98a3576c7>

## 编程专业知识需要了解和使用数百种模板

![](img/76f74982ce8b774813e83d4c9323b484.png)

本文是关于教授计算机编程的顺序教学方法的系列文章中的第四篇。该序列中的步骤是:1)学习如何阅读代码并理解它做什么；2)从清晰的指令中学习如何编写代码；3)学习如何阅读解决常见计算机编程问题的程序模板；以及 4)学习如何编写程序模板来解决编程问题。

你可以通过阅读 Benjamin Xie 和他在华盛顿大学的同事所写的《编程入门技巧指导理论》 来了解更多关于这种方法的知识。

# 什么是程序模板？

程序模板是一种常见的代码使用模式，可以应用于编程问题。例如，在排序算法中使用的交换两个变量值的技术是一个程序模板，因为它可以在任何需要交换变量值的时候应用。

处理数组(或向量或列表)的所有元素是程序模板的另一个例子。为了成为专业程序员，初学者需要学习很多很多的程序模板。编程专业知识需要了解和使用数百种模板。

# 专业程序员在程序模板块中思考

正如我在关于阅读程序模板的文章中所解释的，程序模板代表了程序员在解决编程问题时需要能够几乎瞬间获取的“大块”知识。你可以把程序模板想象成国际象棋大师学习的象棋比赛中的棋盘位置，以便用它们来赢得比赛。

国际象棋大师不会通过玩很多很多的国际象棋比赛而达到这种境界，尽管他们需要玩很多比赛才能成为专家。他们所做的是花数小时研究过去著名国际象棋比赛的棋盘位置，以了解什么位置有利于赢得比赛，以及如何进入这些位置以击败对手。

对于初级和中级计算机程序员来说，程序模板就像这些棋盘位置块。通过了解应该使用哪些模板来解决最常见的编程问题，程序员可以很容易地从内存中访问模板，而不是将他们的脑力用于更具创造性的目的。

# 在理解程序模板之后编写程序模板

使用项目模板解决问题之前的第一步是了解可用的不同项目模板。程序模板是基于您当前正在学习的程序结构而学习的。

如果您刚刚开始学习变量赋值，学习变量交换的程序模板是合适的。如果您正在处理分支语句，那么学习 min/max 模板来确定数据集中的最大值或最小值是合适的。如果您正在学习循环，那么“读取一个元素然后处理它”模板已经成熟，可以进行探索了。

我在最近的一篇[文章](https://thelearningprogrammer.com/how-to-learn-to-program-reading-program-templates/)中讨论了如何学习阅读程序模板，如果你只是来看这篇文章而没有阅读那篇文章，回去读一读，我会在这里等你回来。

# 如何学习编写程序模板

正如我所说的，你不能开始写程序模板，除非你练习阅读它们，理解它们的语法和逻辑。然后你可以开始应用程序模板来解决问题。

让我们看看一些问题和解决这些问题的模板。这些例子中有许多摘自我在本文开头引用的 Benjamin Xie 的论文。

我们将从一个变量交换问题开始:Cynthia 有两个鼠标，她在她的笔记本电脑上使用，但其中一个更适合她的手，她需要使用那一个来完成她将要做的长期项目。不幸的是，那只鼠标的电池快耗尽了，而她的另一只鼠标的电池更强。Cynthia 要求我们为她编写一个 JavaScript 程序来交换她的两个鼠标中的电池，这样她就可以使用更好的鼠标工作更长时间。

程序是这样的:

`let mouse1_battery = 1; // number indicates the battery charge
let mouse2_battery = 10;
let temp_mouse = mouse1_battery;
mouse1_battery = mouse2_battery;
mouse2_battery = temp;`

要理解的关键概念是两个交换两个电池，当一个鼠标没有电池时，必须使用一个临时鼠标来容纳电池。

我还通过让两个学生走到教室前面，把一只手放在背后，用身体证明了这个概念。然后，我给他们每个人一个不同颜色的记号笔，让他们交换记号笔，不要用另一只手，也不要掉记号笔。当然，他们做不到，必须请第三个学生(临时变量)到前面来帮助他们。编程教师应该花更多的时间来创建计算机编程抽象概念的物理演示。

# 求最小值/最大值

下面是一个分支模板的例子(使用 Spidermonkey shell 的 JavaScript):在用户输入的一组三个等级中找到最小和最大等级。

程序如下:

`putstr("Enter the first grade: ");
let grade1 = parseInt(readline());
putstr("Enter the second grade: ");
let grade2 = parseInt(readline());
putstr("Enter the third grade: ");
let grade3 = parseInt(readline());
let max = 0;
if (grade1 > grade2 && grade1 > grade3) {
max = grade1;`


对于这个模板，关键的概念是每个元素必须与其他两个元素进行比较，并且必须对所有的可能性进行比较。在这种情况下，有三个变量需要比较，但是模板适用于任意数量的比较元素。

# 输入—过程—输出

我们要看的最后一个模板是“输入-处理-输出”。我通常在给新程序员上课时告诉他们，这个模板实际上是每一个计算机程序的精髓，它肯定适合编程的前几节课，在这几节课中，学生们将学习如何给变量赋值，并使用算术或一些简单的字符串处理(例如，连接)来操作变量。

我用来测试我的学生识别这个模板的能力的问题类型就像 C++中的这个:用一个提示提示用户输入三个测试分数。定义一个代表测试分数的常数。将变量相加得到总数，然后将总数除以测试分数得到平均值。使用适当的输出向用户显示平均值(不仅仅是一个简单的数字)。

为了展示他们对模板的了解，我让他们对模板的每个部分进行注释。

以下是学生对该问题的解决方案:

`// input
int grade1, grade2, grade3;
const int NUM_GRADES = 3;
cout << “Enter three test scores, separated by a space: “;
cin >> grade1 >> grade2 >> grade3;
// process
int total = grade1 + grade2 + grade3;
double average = total / NUM_GRADES;
// output
cout << “The average of the test scores is: “<< average << endl;`

除了精确计算平均值之外，这个解决方案什么都做对了。原因是 C++做整数除法，所以因为变量 total 是一个整数，常量 NUM_GRADES 是一个整数，所以除法的结果也是一个整数。

我已经教过他们整数除法，但通常需要两三个程序才能让他们记住这个概念，所以我提醒他们必须将平均计算中的一个操作数转换为浮点类型。这一行代码变成了:

`double average = static_cast<double>(total) / NUM_GRADES;`

# 程序模板在计算机编程中无处不在

当然，还有更多的程序模板，我已经在这里演示过了。据我所知，最好的，也是唯一的，基于模板的计算机编程入门教材之一，由 Michael Clancy 和 Marcia Linn 所著的 *Designing Pascal Solutions* ，确定了应该学习的 20 个模板。还有更多更高级的计算机编程概念，如面向对象编程的设计模式，用于搜索和排序数据的许多算法，以及用于图形和树等高级数据结构的算法。

# 通过分块程序模板成为专家

正如国际象棋选手通过“分块”过去著名的国际象棋比赛的棋盘位置来提高他们的发挥一样，学生程序员应该学习程序模板，以便它们在程序员的头脑中成为块。你是怎么做到的？首先，你必须了解不同的程序模板是什么，以及何时何地适合使用它们。然后，你需要练习在编程问题上使用它们，直到它们的使用成为第二天性。

最后，您必须继续扩展您对程序模板的掌握，转向更新的、更具挑战性的编程问题。尝试在你不熟悉的领域解决问题。如果你习惯使用命令式和面向对象的语言，花几个月时间学习一门函数式语言。如果您对使用关系数据库过于自满，请尝试在您的下一个项目中使用 NoSQL 数据库。在所有这些新领域中，尝试使用您已经学习的程序模板来解决问题，如果这些模板不适用于该领域，您将学习可以添加到工具箱中的新模板。

记住，专业知识是一个旅程，而不是目的地。

*原载于 2020 年 2 月 23 日*[*【https://thelearningprogrammer.com】*](https://thelearningprogrammer.com/how-to-learn-to-program-writing-code-templates/)*。*