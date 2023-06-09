# 查找您的联系人:使用 WebRTC 进行视频通话步骤 4

> 原文：<https://levelup.gitconnected.com/find-your-contact-videochat-with-javascript-step-4-4d527576b8cf>

![](img/0f295a813fd8b5bc14eec50a03b44f9e.png)

萨姆·曼恩斯在 [Unsplash](https://unsplash.com/s/photos/friends?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

这是我们用 WebRTC 创建视频聊天系列的第四篇文章。

*   [第一步:来自网络摄像头和麦克风的数据流](/data-stream-from-your-webcam-and-microphone-videochat-with-javascript-step-1-29895b70808b)
*   [第二步:通过 WebSocket 建立连接](/set-up-a-connection-over-websocket-videochat-with-javascript-step-2-f78c307c4fd3)
*   [第三步:建立 WebRTC 连接](/establishing-the-webrtc-connection-videochat-with-javascript-step-3-48d4ae0e9ea4)

在前一篇文章的结尾，我们已经在两个对等体之间建立了一个 WebRTC 连接。这种连接只能在对等体之间通过信令机制交换消息之后建立。这种机制不是规范的一部分，可以自由选择。我们使用 WebSocket，但直到现在，我们的信令非常简单，可以将用户的任何消息广播给所有其他连接的用户。这意味着 WebRTC 连接是在用户之间随机建立的。

这可能不是您在实际应用程序中想要做的事情。在本文中，我们将修改我们的 WebSocket 服务器和客户端代码，让用户通过使用代码找到他们的联系人。只有输入了相同代码的用户才会被联系。因此，如果你至少没有读过上一篇文章，那么这篇文章就没有什么意义。

在我们的示例中，对等体在实际进入聊天室之前，需要在聊天的起始页中输入代码

# 将代码添加到信令消息中

我们首先需要修改起始页，以便用户可以输入他的代码:

![](img/2128956eb5c7fec2a4d0dd158150e536.png)

开始按钮被禁用，直到输入代码。代码长度至少应为 9 个字符。

输入代码并点击按钮后，该视图被隐藏，聊天室被显示。代码保存在变量中，与所有信令消息一起发送。

HTML 有两个部分:一个是 id 为 *start* 的起始页，另一个是 id 为 *videos* 的聊天室。

我们改编了前一个示例的客户端代码:

首先我们创建一个变量 *code* 来保存代码。监听输入上的*输入*事件，一旦代码至少有 9 个字符长，我们就启用按钮。像以前一样，点击按钮，我们开始聊天，这意味着隐藏起始页，显示聊天室，并开始信号过程。我们还需要调整在此过程中发送的消息。我们创建了一个函数 *sendMessage* ，在发送消息之前在其中添加代码。

这里是完整的客户端代码:

# 建立与代码的联系

我们现在需要修改信令机制，以便只在给出相同代码的对等体之间交换消息。为此，我们创建了一个对象 *peersByCode。*在这个对象中，代码将是键，值将是连接数组，如下所示:

```
{
  123456789: [
   { id: 1234, connection: ... },
   { id: 5678, connection: ... },
  ],
  789012345: [
   { id: 4321, connection: ... },
   { id: 8765, connection: ... },
  ],
}
```

当一个对等体通过信令机制发送消息时，他用。我们首先检查代码是否已经是 *peersByCode* 对象*中的一个键。*如果没有，我们补充一下。我们还检查对等体的连接对象是否已经在该代码的连接数组中。如果没有，我们添加它。最后，我们将消息发送给所有拥有该代码的对等体，当然发送消息的对等体除外。

我们在两个给定的对等体之间建立了连接，而不是在随机的对等体之间。在真实的应用程序中，用户将从第三方获得这些代码。例如，假设您的目标是允许雇主和申请人通过 WebRTC 组织面试。雇主会在你的申请中创建一个会议，雇主和申请人会收到一个聊天室的链接。在这种情况下，代码可能会在邀请电子邮件中给出，或者直接包含在他们收到的链接中。

[在下一篇文章](/share-your-screen-with-webrtc-video-call-with-webrtc-step-5-b3d7890c8747)中，我们将允许同事共享他们的屏幕。