# 使用频道编排您的围棋套路

> 原文：<https://levelup.gitconnected.com/orchestrate-your-go-routines-using-channels-c4b9f246cc4b>

通过使用通道在 Go 例程之间交流和传递信息来提升您的 GoLang 并发技能！

![](img/4aaa4784fa1498aeadb83ea98534750d.png)

来自[中央文化省](http://www.cencultu.com.ar/evento/cierre-temporada-la-sinfonica-santafesina/)

Go 之所以出名，很大程度上是因为它干净高效地处理了并发性。我们可以使用 Go 例程在主程序的后台运行多个线程，从而大大提高效率。但是，我们如何在我们的围棋程序之间进行通信，或者在它们之间共享资源呢？我们准备好惊讶于 Go 中简单而强大的通道特性。

这里没有历史课，让我们直接进入代码！

## 一个简单的渠道示例:

虽然通道极大地简化了并发编程，但是我们仍然需要小心我们如何建立对它们的理解。在下面的程序中，我们只执行四个操作。

第一步是在第 7 行创建我们的通道。我们将该通道的输入定义为类型`string`。接下来，我们在第 9 行到第 11 行创建一个匿名函数，我们获取字符串`"ping"`并将它发送到通道 `messages`。

> 当使用通道时，您可以认为`<-`操作是根据箭头的方向从通道向或**发送信息。**

第三步是从消息通道**向**msg 变量请求存储的字符串`"ping"` **。最后一步是将消息打印到控制台。**

## 通道将等待发送信息:

例如，go 中的通道被*阻塞*——假设我们同时执行两个 Go 例程。如果一个 go 程序通过通道向另一个请求信息，它将*阻止*执行，直到另一个 go 程序将信息传递到连接通道。

通过下面的代码，我们可以看到通道是如何阻塞的。使用我们在上一篇文章中学到的内容，`sync.WaitGroup`将确保我们的 go 例程在退出主程序线程之前完成。

首先，我们在第 13 行初始化一个新的通道`messages`。

接下来，在第一个匿名函数中，我们休眠一秒钟，然后在退出之前将字符串`"Echo"` **发送到`messages`通道**。在下面第 26 行的匿名函数中，我们请求从`messages`通道到`msg`变量的输入**。这是一个*阻塞*操作，此功能不会继续，直到我们从`messages`获得输出。**

如果我们运行上面的程序，我们将得到以下输出:

```
Starting second anonymous function...
Starting first anonymous function...
Echo!
Exiting first anonymous function
I hear an Echo!
Exiting second anonymous function
```

同样，注意我们的 go 例程是如何*不确定的*。您无法知道这些功能将按什么顺序开始或停止，但您知道当等待发送信息时，通道将会阻塞。在第一个`Echo!`和结果打印语句`I hear an Echo!`之间有第二个延迟，因为接收通道等待输出。

## 防止渠道出现死锁:

如果通道在等待资源时阻塞，如果资源从未被发送会发生什么？这种情况会导致死锁，Go 只会在运行时检测到死锁，而不会在编译时检测到死锁。让我们看一个例子。

在作为 go 例程执行的第一个匿名函数中，无论`i`的值是什么，我们都向消息通道添加三次。当我们跳出这个循环时，我们关闭通道来通知我们已经完成了附加，以防止死锁。

在第二个 go 例程中，我们从`messages`通道获得`msg`和`open`。`open`参数是一个布尔值，表示通道是否关闭。如果通道没有打开`!open`，那么我们使用`wg.Done()`跳出循环并退出我们的 go 程序。简单，但是有效！

您还可以利用 Go 的一些语法来简化第 16 行的第二个 for 循环。然后你甚至不需要检查通道是否关闭，Go 会为你处理这些。

```
for msg := range messages {
    fmt.Println(msg)
}
```

您也可以将**容量添加到您的频道**中，如下所示:

即使我们在第 8 行创建了一个容量为 2 的通道，我们也能够发送和接收总共三个字符串，因为通道像队列一样工作。只要频道中的项目不超过 2 个，您就在容量限制范围内，不会收到错误。

最后，如果您的通道在时间限制上相互阻塞，您可以在 Go 中使用`select`表达式来执行任何准备好的通道。

这里我们有两个通道，它们在两个 go 例程中被无限追加。第一个 go 例程每秒追加到通道`c1`中，而第二个 go 例程每两秒追加到通道`c2`中。如果您只是试图从这些通道打印，`c2`通道会阻塞，您将每两秒钟获得两个输出。

然而，使用`select`语句将不断地检查一个准备从中提取信息的通道。执行此语句将允许来自通道的信息流不受任何阻塞。

通道提供了一种简单而强大的方式在你的围棋程序之间进行交流，甚至只是以一种更有意义的方式控制信息流。考虑死锁的风险是很重要的，因为它在 Go 的编译时不会被识别，但是跟踪一个通道何时应该打开或者增加通道的容量是一个很好的开始。

我希望你在这篇文章中学到了一些新东西。如果你看到了一些你想要进一步解释的东西，我鼓励你在下面留下评论。感谢阅读！