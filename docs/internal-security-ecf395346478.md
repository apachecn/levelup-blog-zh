# 国内治安

> 原文：<https://levelup.gitconnected.com/internal-security-ecf395346478>

![](img/607bf291f2d1959534303a84f590d0fc.png)

60%的安全漏洞来自组织内部，然而当我们想到安全性时，我们通常会想到漏洞、利用等。一直以来，60%的黑客攻击都是来自于一个人，他只是登录系统，然后拿走他想要的任何东西。我最近一直在思考这个问题。我花了大量的时间为我即将出版的书中的一章研究安全相关的问题，不幸的是，在强化内部系统方面发现的很少。

是的，也有这方面的材料。但似乎绝大多数是针对外部威胁，而不是内部威胁。我明白了。内部保护很难，但这可能是我们能做的最重要的事情，而且可能没有我们许多人想象的那么难。我想先声明我不是安全专家。我写这篇文章的原因是因为我们大多数人都不是。那么我们这些“典型的程序员”能做些什么来减轻安全风险呢？

我们可以做很多事情，但大部分工作都由开发人员或安全团队负责。还有关于编写安全代码的要点，这方面也有很多。我想谈谈我们这个领域特有的一些东西，这些东西并没有被过多地涉及。几十年前，一名当地妇女从当地银行偷走了 10 亿 NIS(当时大约 7000 万美元)。这个偷了一段时间，十几年……没人注意到！

一家银行怎么会错放 7000 万美元？他们没有制衡机制吗？他们当然知道。系统改变了那个女人。她是回应系统警报的人。她没有请一天假或休假，如果她有她的替代品会注意到所有的违规行为。这不是技术入侵。不是我们想象中的黑客。但是概念是一样的，我们锁好门窗但是里面…对所有人都是免费的。

这个故事很重要，因为那个女人不是坏人。我们不应该用怀疑的眼光看我们的同事。她被当地的有组织犯罪勒索，这引发了整件事。因此，我们需要尽可能地限制我们的风险，避免依赖于单点故障。

# 工作/安全平衡

内部安全有许多好处:

*   用户有隐私权。即使我们公司不在乎这一权利，隐私也受到世界各地法律法规的保护。重大疏忽会导致责任诉讼。
*   知识产权盗窃是一个真正的问题，例如谷歌起诉优步知识产权盗窃。
*   在外部攻击的情况下，内部保护将使获取任何有意义的信息变得更加困难。

内部安全至关重要，主要由管理员处理。作为程序员，我们经常忽略我们工作的特定方面。在这方面，我们可以做一些事情。具体来说:不要打开漏洞，确保我们记录一切，应用访问限制和支持良好的密码。

我们不想做的事情是让我们的生活变得困难。我们已经有足够多的事情要做了，而像密码轮换这样的公司政策对组织的安全毫无用处。它们是安全剧场，事实上危害安全。用户将这些密码写在便利贴上，然后放在办公桌上。有效地抵消了它们的价值。

我们需要提高安全性，同时尽量减少对日常工作的影响。这些是相互冲突的目标，但我们可以在这里找到一个平衡点。零信任是这些政策的关键词，这是一个有趣的话题，但我不想写它。

我是开发商，不是开发商。我也不是安全专家。因此，部署安全策略并保护它的责任不在我身上。也不应该。但是安全是一个团队的努力。最薄弱的环节是我们都失败的地方。一个人点击一个坏的电子邮件链接可以挫败最好的安全策略。作为开发人员，我们可以为我们的同事和使用我们产品的客户做很多事情。这就是我要讨论的。

# 不要开门

这可能看起来很疯狂。我们为什么要开门？我们是有安全意识的人。但是我们常常想都没想就打开了比喻的大门。你会让远程调试对生产服务器开放，只是为了检查东西吗？

那是一扇敞开的门。

即使您有防火墙规则。这还不够。它假设:

*   黑客无法绕过防火墙
*   入侵系统的人不在里面

两者都是有问题的概念。现在你可能会说:那是零信任。你完全正确。但是还是要说一下，因为有相当多的开发者是这样做的。网上这么多数据库开放扫描，很吓人。

如果你是团队中的开发人员，请注意这一点。向前沟通，并尝试改善情况。人们通常习惯于事物的本来面目，甚至没有注意到一个明显的洞就在他们面前。

# 使用审计日志

作为一个有安全意识的开发人员，你应该做的最重要的假设是:你可能会被黑客攻击。然后呢。开发人员是第一道防线。我们开发人员很少在这方面做太多。如果黑客真的进入了，有两件事落到了我们头上。首先是让他们更难造成伤害(见下一节)。第二种是后来。

黑客做了什么？他们去哪里了？他们得到了什么？这些都是我们应该能够回答的问题。我们需要一个系统，记录一切，但不仅仅是日志。我们需要[审计日志](https://www.baeldung.com/database-auditing-jpa)，默认情况下它内置于一些框架中，并且相对容易添加。有了它，我们就可以在事情发生后，或者在黑客攻击正在进行的时候进行跟踪，并减轻它。

说到日志，不要过分热衷于应用程序日志记录，并确保日志的安全。我与不少组织打过交道，他们对数据库进行了适当的加密和保护。然而，日志访问对所有人都是免费的。通过阅读日志，我们经常可以找到我们需要的一切。用户令牌有时直接写入日志，让我们模拟用户。想象一下，一个管理员登录时，不仅可以访问日志的恶意用户可以假冒其身份。这是完美的犯罪，因为看起来像是别人干的。同时我们应该检查日志，确保不记录任何有风险的内容。我们还应该保持日志较小，这样我们就可以注意到有问题的方面。此外，我们需要将生产日志的访问权限限制在需要知道的有限人群中。

# 访问限制

我们应该加密所有重要的东西。机密必须安全地存储在外部，以避免在服务之间跳跃，从而实现完全控制。不应使用相同的凭据或在服务器上存储源。一切都应该是只读的，没有 SSH 访问的准系统。

如果有可能进入生产环境，黑客就能找到进入的方法。通过取消对生产的正常访问，我们消除了这种可能性，并迫使恶意黑客找到非标准的方式进入。

# 支持好的密码

我至少在一个项目中失败了，并且没有充分意识到它的价值。许多安全专家相信密码管理器。那很好。但是作为一名开发人员，在密码方面我们需要支持两件事情:

*   特殊字符
*   非常长的密码

一些密码验证不允许一些特殊字符，这是不好的，虽然近年来越来越少。但是真正的问题是密码长度。我喜欢用密码。这些句子由 5 个以上的单词组成，对我来说有意义，因此容易记忆。但不可能随机猜测，也不可能暴力破解。例如，“幼儿园早上 8 点就挤满了人”是不可能猜出来的。即使一个人站在我的肩膀上看着我，输入他们也不会拼凑起来(不，那不是我的密码)。然而，一些系统将密码长度限制为 12 位。

# 最后

这是一个团队的努力。是的，大部分工作是在安全团队(如果你有他们的话)和 DevOps 上进行的。然后是做大量工作的工具，例如保持我们的依赖关系没有已知的漏洞，等等。

谈到安全性，所有这些都不够。尤其是如果问题出在公司内部的话。我不喜欢零信任这个词，尽管它背后的技术原理是可靠的。我认为我们需要作为一个团队来发现异常，并注意到事情并不像看起来那样的情况。但最重要的是，我们需要为入侵做准备。如果我们所有部门都做好了 100%的准备。它永远不会到来，这是一件好事。

我们需要在警惕性、安全性和生产率之间找到微妙的平衡。这不是一个简单的平衡。与仅仅将密钥提交到 git 或将属性文件放入映像相比，使用 secret vaults 这样的工具是很痛苦的。但是随着我们的成长，我们需要这样的实践。我同意，快速成长的创业公司不需要他们。但是正如推特提醒我们的。安全实践差的快速成长的创业公司成为安全实践差的成熟的上市公司。