# 我希望在开始时就知道的 8 个 Go 编码技巧

> 原文：<https://levelup.gitconnected.com/8-code-hacks-for-go-that-i-wish-id-known-when-i-started-56a6f4399acf>

![](img/395ce8626a268d273c2e399085dc02c0.png)

我使用 Go 已经很多年了，偶尔我会遇到一个小小的代码黑客，它让我的生活变得更好。所以我决定和你分享！

# 1.检查键是否在映射中

这可能是众所周知的，但我经常使用它，我觉得应该提到它。如果您想检查一个键是否在映射中，您可以调用:

```
_, keyIsInMap := myMap["keyToCheck"]
if !keyIsInMap {
  fmt.Println("key not in map")
}
```

# 2.在转换变量时检查。

有时你需要将变量从一种类型转换成另一种类型。不利的一面是，如果你输入错误，你的代码将会崩溃。例如，下面的代码尝试将变量“data”转换为字符串。

```
value := data.(string)
```

但是，如果“数据”不能被转换成字符串，代码将会出错。但是有更好的办法！类似于检查键是否在映射中，您可以在转换时获取一个布尔值来检查转换是否成功。

```
value, ok := data.(string)
```

在本例中,“ok”是一个布尔值，它告诉您转换是否成功。这样，您可以比直接死机更优雅地处理类型不匹配。

# 3.使用 append 时指定数组的大小。

如果需要向数组中添加项目，定位选项是“append”。例如:

```
for _, v := range inputArray {
  myArray = append(myArray, v)
}
```

然而，这在大型数组上可能会很慢，因为 append 将不断需要增加“myArray”的大小来容纳新值。更好的方法是先指定数组的长度，然后直接给每个值赋值:

```
myArray := make([]int, len(inputArray))
 for i, v := range inputArray {
  myArray[i] = v
 }
}
```

我更喜欢第三种选择，那就是将两者结合起来！对我来说，它的可读性稍微好一点，但是也没有速度上的损失，因为你在开始的时候就指定了大小。

```
myArray := make([]int, 0, len(inputArray))
for _, v := range inputArray {
  myArray = append(myArray, v)
}
```

在这里，您将数组的大小设置为 0，但是将最大大小设置为输入数组的长度。因此 append 不需要在运行过程中调整大小。如果您比较由 1 亿个整数组成的数组的时间，您可以看到速度差异:

```
normal array append took   3782.1423ms
presized array took        549.8333ms
presized array append took 685.9402ms
```

# 4.使用“追加”和**省略号**来连接一个数组。

有时你需要连接两个数组，一个很好的简单方法是利用“append”是一个变量函数的事实。因此，虽然一个普通的追加调用可能看起来像这样:

```
myArray = append(myArray, value1)
```

“追加”还允许一次追加多个元素:

```
myArray = append(myArray, value1, value2)
```

虽然这很有用，但这并不是真正酷的部分。最酷的是，在将数组传递给函数时，可以使用“…”来扩展数组。假设您想将“inputArray”连接到“myArray ”,您需要做的就是:

```
myArray = append(myArray, inputArray...)
```

这将扩展“inputArray”的所有值，并将它们传递给 append。

# 5.打印时显示参数名称和值。

这个方法花了很长时间才学会，但是现在我知道了，我一直在使用它。最初，当我想在结构中显示参数名和值时，我会封送到 JSON 并记录下来。然而，有一个简单得多的方法。当进行 Printf 时，在格式中添加一个+。例子

```
fmt.Printf("%+v \n", structToDisplay)
```

您还可以通过将+改为 a #，以 Go 语法表示将其打印出来。示例:

```
fmt.Printf("%#v \n", structToDisplay)
```

各种输出的比较:

```
Without params:       {first value 2}
With params:          {Value1:first value Value2:2}
As go representation: main.MyStruct{Value1:"first value", Value2:2}
```

# 6.枚举时将“iota”与自定义类型一起使用

在 Go 中枚举某物时，最好使用“iota”。“iota”是 Go 中的一个关键字，每次调用时都会分配递增的整数。你可以想象这对创造枚举来说是很棒的。然后，您可以将它与自定义整数类型相结合，这样编译器将确保您的代码的用户只使用指定的枚举。示例:

```
type PossibleStates intconst (
 State1 PossibleStates = iota
 State2
 State3
)func UpdateState(newState PossibleStates) error {
```

在这里，您创建了一个自定义类型“PossibleStates”，然后每个枚举都是一个“PossibleState”类型，其值由“iota”指定。然后，当任何人调用“UpdateState”时，编译器将确保只发送可能的状态，而不发送任何旧的 int。

# 7.模拟接口时，将与接口函数匹配的函数作为参数。

这是 Mat Ryer 提供的，它改变了我的游戏规则。假设您有一个想要模仿的接口:

```
type DataPersistence interface {
 SaveData(string, string) error
 GetData(string) (string, error)
}
```

这可能是几种不同类型的持久性的接口。您想要测试您的代码，所以您将创建一个可以在您的测试中使用的模拟 DataPersistence 结构。然而，不用编写复杂的模拟结构，您可以简单地创建一个带有参数的结构，这些参数是与接口函数匹配的函数。这是一个读起来令人困惑的句子，所以一个好的例子会有所帮助！您的模拟应该是这样的:

```
type MockDataPersistence struct {
 SaveDataFunc func(string, string) error
 GetDataFunc func(string) (string, error)
}// SaveData just calls the parameter SaveDataFunc
func (mdp MockDataPersistence) SaveData(key, value string) error {
 return mdp.SaveDataFunc(key, value)
}// GetData just calls the parameter GetDataFunc
func (mdp MockDataPersistence) GetData(key string) (string, error) {
 return mdp.GetDataFunc(key)
}
```

这意味着当您测试时，您可以设置函数在测试本身中做您需要的任何事情:

```
func TestMyStuff(t *testing.T) {
 mockPersistor := MockDataPersistence{}
 // here we set SaveData to just return an error
 mockPersistor.SaveDataFunc = func(key, value string) error {
  return fmt.Errorf("error to check how your code handles an error")
 } // now we can check how thingToTest handles it when 
 // SaveData return an error
 err := thingToTest(mockPersistor)
 assert.Nil(t, err)
}
```

这确实有助于可读性，因为您可以清楚地看到每个测试中的模拟内容。这也意味着您可以访问模拟函数中的测试数据，而不需要维护外部数据文件。

# 8.如果有人没有创建接口，就创建你自己的接口。

这个也是由[马特瑞尔](https://medium.com/@matryer)提供的。如果你正在使用另一个 Go 库，他们有一个 struct，但是从来没有使它成为一个接口，你可以只做一个来匹配它。假设他们的结构如下所示:

```
type OtherLibsStruct struct {}func (ols OtherLibsStruct) DoCoolStuff(input string) error {
 return nil
}
```

在你的代码中，创建一个可以实现的接口:

```
type InterfaceForOtherLibsStruct interface {
 DoCoolStuff(string) error
}
```

然后，您可以编写代码来接受这个接口。使用另一个库的结构时传入它。然后当你想测试它的时候，从上面开始做模拟接口的把戏。

# **奖励:实例化嵌套的匿名结构**

我在使用生成代码时遇到过几次这种情况。有时当代码生成时，你会得到一个嵌套的匿名结构。示例:

```
type GeneratedStuct struct {
  Value1 string `json:"value1"`
  Value2 int `json:"value2"`
  Value3 *struct {
    NestedValue1 string `json:"NestedValue1"`
    NestedValue2 string `json:"NestedValue2"`
  } `json:"value3,ommitempty"`
}
```

现在，假设您想要创建这个结构的一个实例来使用，您将如何着手呢？Value1 和 Value2 很简单，但是如何实例化一个指向匿名结构(Value3)的指针呢？我的第一个解决方案是用 JSON 编写它，然后将它封送到 struct 中，但是这样做很糟糕。事实证明，在实例化它时，您需要使用另一个匿名结构:

```
myGeneratedStruct := GeneratedStuct{
  Value3: &struct {
   NestedValue1 string `json:"NestedValue1"`
   NestedValue2 string `json:"NestedValue2"`
  }{
   NestedValue1: "foo",
   NestedValue2: "bar",
  },
 }
```

这似乎是显而易见的，但是要注意，它需要与*完全匹配*，甚至是 JSON 标签。虽然上面的代码可以工作，但是由于类型不匹配，下面的代码将无法编译:

```
myGeneratedStruct := GeneratedStuct{
  Value3: &struct {
   NestedValue1 string `json:"nestedValue1"`
   NestedValue2 string `json:"nestedValue2"`
  }{
   NestedValue1: "foo",
   NestedValue2: "bar",
  },
 }
```

看看你是否能发现不同之处！