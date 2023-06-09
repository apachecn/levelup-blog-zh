# SMTP 运行状况、发送操作和组件

> 原文：<https://levelup.gitconnected.com/smtp-health-sending-operations-and-components-ada8b13b9caf>

![](img/7dd682ea81f92b1ec55e9b36cf22630f.png)

埃内科·乌鲁内拉在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

电子邮件作为一种沟通机制已经存在了近 40 年，它仍然被认为是公司的一个关键组成部分，也是今天几乎所有事情的细节。电子邮件作为身份证明文件、护照甚至信用卡都很重要。照顾它是至关重要的。

在更进一步之前，我们需要确定，所有这一切都是可能的，因为互联网，这个著名的设备之间的网络，可以使每个人共享数据成为可能。还有，互联网中涉及的元素，比如 IP 地址、**、DNS 服务**、**、VPS** 、 **SSL** 方式等等。

所有这些部分都有一定的功能，使一切都变得生动起来。借此机会，我将对电子邮件技术进行一个高层次的概述，它涉及哪些内容，当然，还有如何称赞健康的环境和声誉。

我们需要开始谈论一下 **DNS** ，这是因为它执行域和 IP 地址之间的转换，这让我们很容易记住域名，而不是记住 IP 地址。这不是很好解释，你可以把一个 DNS 服务器比作一个电话簿，它将映射名称和 IP 地址。

免责声明:有很多直接涉及电子邮件操作的术语需要深入理解。在这节课中，我会简单地提到它，确保它不会对所有内容都公平。

## 电子邮件发送操作

你有没有问过自己，你的电子邮件客户端是如何收发邮件的？

这是一个激烈的过程，但可以分成非常小的和一般的步骤。为此，我们需要讨论一下**发送者**和**接收者**。

假设您打开了 Gmail 或 Outlook 客户端，该软件配置为接收和发送操作。为了发送邮件，我们将使用**SMTP**协议(简单消息传输协议)，因此:

1.  在这里，**发送者**撰写并发送一封电子邮件(通过 **SMTP** 协议)。这里的 SMTP 就像一个邮局，评估是否一切正常
2.  一旦是好的，它就被重定向到一个 **DNS** 服务器(那个地址簿)来解析发送者的 IP 地址。
3.  **DNS** 再次将消息发送到 **MTA 服务器**(邮件代理传输)，后者选择合适的收件人收件箱，将消息发送到该收件箱。
4.  信息被发送到收件箱。

然后，它来到了操作的**接收者的**侧。

在这一点上，在 MTA 和收件箱之间，有一些协议用于客户端的输入/输出通信。这些是 POP 和 IMAP 协议。

涉及的其他组件有一个通用的 **VPS** 和 **SSL** ，第一个是一个私有服务器，其中一个服务器将绑定到一个 IP 地址以进行正确处理*(此处需要额外的软件)，*也是最推荐的一个 **SSL** 连接，其中所有发送和接收的流量都将被加密(非常有利于保护流量)。

如果你是一名开发人员，也许你可以做一点研究，让自己托管自己的电子邮件服务器，像 **Cpanel 邮件服务器**、 **Webmin** 这样的流行工具，或者如果你是一名 **AWS** 粉丝，你可以实现一个 **AWS 邮件服务器。**这取决于你，几乎在所有情况下，你都需要为你的服务器配备操作系统，执行完整的 **DNS** 管理，设置电子邮件创建、 **SSL** certs、 **MX** 记录，以及更高级的东西，如 **DNSSec** 、 **SPF** 、 **DKIM** 和 **DMARC** 记录(稍后再说)

对于 VPS 选项，任何知名的云计算提供商都可能是它的合适人选，可能是 DigitalOcean 的一个小水滴，也可能是 AWS 的实例

## 我们都准备好了。让我们热身

这个热身的概念是关于创造和产生一个可接受的流量来提高我们的声誉。电子邮件以一种不确定的状态开始，所以很多时候，你的邮件会被放入垃圾邮件收件箱，而实际上并不是一封预期的垃圾邮件。

这也是像 Google 这样的 ISP 进行身份验证的评估。如果你的信誉很好，那么优先发送。

评估非常简单，它将取决于您的邮件列表、内容和许多其他因素，因此，为了健康，您需要注意您的收件人参与度、主题行，并生成有价值的内容以避免垃圾邮件问题

## 避免垃圾邮件

垃圾邮件问题可以很容易地解决和防止，如果你使用 Gmail 或 Outlook 这样的解决方案，有很大的机会不出现这种行为，谷歌的 IP 是完美的，但是，对于公司帐户来说，这可能是一个挑战，所以，请确保这一点。

1.  避免不健康的电子邮件服务器，只需收集电子邮件，无需上网或购买邮件列表
2.  在 DNS 方面，你应该有 SPF 和 DKIM 记录集，这使你的服务器更加安全
3.  邮件正文很重要，内容很关键，你应该避免垃圾邮件。
4.  获得良好的知识产权声誉

## 高级 DNS 设置

为了改善您的电子邮件健康状况，您可以对电子邮件服务器应用更多规则。如今，几乎所有云提供商都需要这些新类型的记录，以便更好地工作和提高安全性。

让我们从 **SPF** 或**发件人策略框架**开始，这一特殊功能让您可以识别哪些域被允许使用您的服务器域来发送邮件。因此，如果有人损害你的电子邮件信用，并试图用你的电子邮件帐户发送电子邮件，它将不会被发送。

换句话说，当发送一封电子邮件时，你将输入'**到'**和'**从'**标题信息，对吗？如果电子邮件包含垃圾邮件内容，收件人会认为您发送了一封**合法的恶意电子邮件**

SPF 将帮助您识别允许发送电子邮件的 IP 地址。

这里有一个例子:

`TXT`记录:@(在`host`)，并为`TXT Value`添加要发送的可用 IP。可以为`1 hour`设置`TTL`

继续前进，到 **DKIM** 或**域密钥标识符**

该密钥是标识您的域服务器的签名。就是这样。

因此，当您发送电子邮件时，收件人将检查您的签名，并验证邮件是否来自该域。

这里有一个例子:

`TXT`记录:为`host`添加适当的标识符，为`TXT Value`生成一个长文本，`TTL`也被设置为`1 hour`

最后， **DMARC** 或**域消息认证报告和一致性**(听起来很吓人，但事实并非如此！)

该记录是针对 SPF 和 DKIM 的报告服务，主要用于部署，其唯一目标是报告两个记录都配置良好。

该示例遵循一个预定义的模板，该模板形成一个操作，因为 DNS 记录将如下所示。

`TXT`记录:对于`host`，您将拥有一个带有可选附加信息的`_dmarc`前缀，一个带有特定模板的`TXT Value`和一个用于`1 hour`的 TTL

DMARC 模板如下所示:

`v=DMARC; p=none; fo=1; rua=mailto:dmarc@davidlares.com; ruf=mailto:dmarc@davidlares.com`

这看起来很复杂，但有一个解释:

1.  `v=DMARC`是版本
2.  `p=none`声明不需要任何操作
3.  `fo=1`我很确定那是用于报告控制标志的
4.  `rua`是您希望接收汇总报告的电子邮件地址
5.  `ruf`是发送法医报告的邮件。

还有更多的内容要讲，我只是在解释最基本的东西。我写这篇文章的目的是分享一个健康的、配置良好的电子邮件系统有多重要的概述。你的很多业务都是通过你简单的电子邮件账户来完成的。

保持简单、实用、安全。

快乐写作:)