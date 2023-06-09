# 后端开发人员的安全最佳实践

> 原文：<https://levelup.gitconnected.com/security-best-practices-for-backend-developers-46440afe7e69>

![](img/7fbaa7725930ae1c4b05f4a6c54e6f8e.png)

[约翰·卡梅隆](https://unsplash.com/@john_cameron?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

作为后端开发人员，我们有一项艰巨的任务。我们制作管理人们数据的应用程序，我们可以编写代码对他们做很多事情，不管他们是好是坏。

在本文中，我们将看看在开发后端应用程序时需要注意的一些最佳实践。

# 使用 Docker 沙盒应用程序

Docker 是一个让我们运行沙盒容器的伟大程序。因此，我们应该使用它们来托管和运行我们的后端应用程序。

这样，所有的应用程序都运行在它们自己的容器中，因此它们可以在自己的环境中运行。这意味着任何我们不信任的二进制文件都不能在 Docker 容器之外运行。

此外，如果我们重建 Docker 容器，我们对 Docker 容器所做的任何更改都将被删除，因此，如果我们或某些攻击搞乱了容器，我们可以重建它，并将其恢复到工作状态。

不同应用程序的库和依赖项不会互相干扰。

此外，在同一个 ost 上运行的多个容器将对其他容器和主机本身具有某种程度的访问权。

因此，我们应该保护所有的主机，并使用最少的功能运行容器。

如果需要的话，我们可以禁用对容器的网络访问。

# 绝不能通过公共网络发送未加密的凭据

我们永远不应该在不加密的公共网络上发送像 SSH 密钥和密码这样的凭证。

有很多方法可以保护它。我们可以加密，或者通过密码管理器之类的东西发送。

# 永远不要在源代码管理中存储秘密

秘密不应该被签入源代码控制。这很容易做到，如果它们停在那里，我们必须重置它们。

签入它们会增加暴露给恶意用户的风险，所以我们不应该冒这个险。

即使我们更改了秘密文件的文件权限，源代码管理系统通常会取消这些文件权限，以便它们可以再次对公众可读。

因此，我们应该把我们的东西放在一个不会被签入源代码控制的文件中。

不管名字是什么，都应该忽略。

# 登录限制

在我们的后端应用程序中，我们应该限制单位时间内用户可以尝试登录的次数。

如果用户在几次尝试后都没有登录，比如 10 次尝试失败，那么我们应该锁定他们一小段时间，比如 5 分钟。

这样攻击者就不能轻易进行暴力攻击。

# 用户密码存储

密码不应以纯文本形式存储。如果我们需要记录密码，那么它们应该存储在不显示密码的地方。

例如，我们可以使用密码管理器来存储我们的密码。

我们可以使用非对称加密来存储我们的密码，这样我们可以用公钥加密存储它们，然后用私钥将它们解密回纯文本。

在大多数情况下，密码应该以单向散列的形式存储，这样即使攻击者登录到我们的数据库，他们也无法被解密。

我们用安全散列和 salt 对每个密码进行加密，如果我们需要核对散列密码进行身份验证，只需核对散列密码。

![](img/c0fec06f37e7ffd249c7b4c1b6c29cab.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Austin Paquette](https://unsplash.com/@pqt?utm_source=medium&utm_medium=referral) 拍照

# 审计日志

我们的应用程序必须保留审计日志，以了解谁做了什么。活动越重要，我们需要做的日志记录就越多。

这样，如果需要，我们可以检查可疑的活动。

这样，人们可以知道人们在什么时间做了什么，改变前的值是什么，改变后的值是什么。

每个日志条目都应该包含时间、执行操作的用户、操作以及新旧值。

它可以作为单独的日志文件存储，也可以作为常规应用程序日志的一部分存储。或者它可以存储在应用程序数据库中，以便我们可以查询条目。

# 结论

我们需要一份审计日志来检查可疑活动。此外，我们需要限制登录尝试，使攻击者无法使用暴力攻击以授权的方式登录。

此外，我们不应该向公众公开密码。

最后，Docker 非常适合沙盒应用程序和最小化攻击面。