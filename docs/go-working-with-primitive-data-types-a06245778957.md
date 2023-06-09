# go-使用原始数据类型

> 原文：<https://levelup.gitconnected.com/go-working-with-primitive-data-types-a06245778957>

![](img/0de9547034ba97fbf9a5b3e685c75a13.png)

现在是我们开始深入研究 Go 语言的时候了，简单谈谈所使用的原始数据类型。我们将把这次讨论分成三个部分。

1.  Go 中的变量声明和可用的原始数据类型
2.  围棋中的指针及其特点
3.  常数以及它们与其他语言的不同之处。

如果你来自任何其他编程语言，每一个都将与你所知道的不同。让我们详细看看它们，并试着理解这些特性。

# 变量声明:

与大多数语言不同，Go 有多种声明变量的方式。

要在 Go 中声明一个变量，我们指定关键字`var`，后跟变量的名称和变量的数据类型。需要提醒你的是，Go 是一种静态类型语言。

```
//classic variable declarationvar age int
age = 35
```

如果您来自任何其他静态类型的语言，这可能对我们大多数人来说很熟悉，因为我们可能经常使用这种类型的东西。然而，这种声明是相当冗长的，仅仅为了一个声明就要举行许多仪式。

我们可以将声明和赋值压缩到下面的语句中，这也是完全有效的。

```
var age int = 35
```

但是，声明仍然冗长。

大多数时候我们只想声明一个变量并初始化它。我们不想要键入`var`关键字和数据类型的所有仪式。这是我们在做编译器在大多数情况下应该能够为我们做的工作。

Go 也为我们解决了这个问题。我们不是以`var`开始声明，而是以变量的名字开始，后面跟着一个`:`，紧挨着`=`符号。

```
age := 35
```

这个`:=`将触发 Go 来允许我们使用我们的隐式初始化语法，这意味着 Go 将根据我们赋予它的内容来暗示`firstName`的数据类型。这可能是所有 Go 代码库中最常用的语法。

这里还要注意的一点是，与任何其他编程语言不同，你声明一个变量而不在代码中使用它们会抛出一个编译时错误`declared not used`。这是一个维护的事情，所以，如果你有一个变量数据类型在本地初始化，那么你必须使用这个变量。

# 指针及其功能:

还有一种数据类型叫做**指针**。我们之前看到的数据类型是值类型。所以当你声明一个变量`i`并赋值`4`时，这个变量指向内存中保存值`4`的位置。

指针正如你可能已经知道的那样，它不是保存变量中的实际值，而是保存存储该值的内存位置的地址。指针变量的声明有点独特。

```
var firstName *string
firstName = "dan"
```

与普通值类型不同，打印指针变量不会给出值。相反，你会看到变量中的内存位置，比如存储值的`0x40e020`。

**解引用:**解引用一个指针可以让我们访问指针所指向的值。

```
var firstName *string
firstName = "dan"
fmt.Println(firstName) // this prints 0x40e020
fmt.Println(*firstName) // this prints dan
```

相同的星号操作符用于表示指针变量和取消引用。

# 常数

在很多方面，常量和变量在 Go 中的作用是一样的。唯一的区别是，我们不能改变它被初始化后的值。

```
const pi = 3.14
const pi float32= 3.14
```

常数不能改变它的值，所以你不能声明常数，然后在以后初始化它。这里我们需要注意的另一件事是常量的数据类型需要在编译时可用。所以不能将函数的返回值赋给常数，因为函数只在运行时计算。

```
package mainimport(
 "fmt"
)func main(){
  const c = 6
  fmt.Println(c + 3) //Prints 9
  fmt.Println(c + 1.3) //Prints 7.3
}
```

在上面的代码片段中，我们没有指定`const` `c`的数据类型，所以在第一个`Println`中，常量`c`被计算为整数，而在下一行中，它被解释为浮点类型。这就是所谓的**隐式类型常量**。编译器会在每次遇到该类型时将它解释为适当的类型。

# 结论

Go 的设计和开发秉承了简单的理念。简单，我指的是我们从中获得的极端复杂。非常冗长的语法是在非常特殊的情况下使用的，但是我们最终使用的一定是比较简单的语法。指针在其他语言中更难理解和使用，当然，它带来了额外的好处，但是这些好处被简单性超过了。此外，要注意复杂的实现和细节需要非常陡峭的学习曲线。

如果你还没有读过我之前关于设计 Go 的想法的博客，这种语言是根据今天的问题构建的，我推荐你在这里阅读。

Go 中的下一个集合数据类型实现。