# 这就是开发人员走捷径的结果

> 原文：<https://levelup.gitconnected.com/this-is-what-happens-when-developers-take-shortcuts-244b8d09f11d>

## 你了解软件缺陷的真实成本吗？

![](img/8a69a11045f647fe2b7bcefad55a2ba2.png)

信用:Canva

几周前，我们的团队在生产中部署了一个新代码，作为平台移植工作的一部分。这是一个已经存在多年的现有功能。不幸的是，随着用户的第一次点击，新代码就在生产中崩溃了。

这是一个尴尬的局面。

参与实现的开发人员花了几个小时来确定根本原因。用户对产品中出现的以前正常工作的功能变得不耐烦了。

最终，我们发现执行一个特定的 SQL 查询需要 15 到 20 分钟。该团队根据成本优化分析快速修复了它，并将其部署到生产中。更新后的查询非常有效。

后来我们发现在开发阶段没有对代码进行分析。该团队还跳过了性能测试，因为它“T0”只是“T1”一个平台工作，而不是新功能开发。

新代码仅仅基于系统集成测试结果就被提升到生产阶段。

问题在于，该查询会对生产中的数十亿条记录进行全表扫描。在 SIT 中，我们的数据库只有几十万(1 十万= 100K)条记录用于功能测试。

这个事件提出了一个软件缺陷的真实成本的问题。

软件缺陷的真实成本超出了修复 bug 的成本。事实上，大多数人会认为，绝大部分成本是在错误被发现之前很久就产生的。这包括重现 bug 所需的时间和精力。

当团队试图追踪根本原因时，我们还应该考虑调试时间和生产力损失。

此外，经常会有与缺陷相关的间接成本。例如，如果在生产中发现了一个严重的错误，它可能会中断正常的业务运营。在某些情况下，有缺陷的软件会导致公司承担法律责任。

在我们的案例中，生产中的缺陷使我们付出了代价:

*   该功能需要几个小时的停机时间
*   工程师、经理和业务用户在电话中浪费的时间
*   将质量代码部署到产品中的团队的可信度
*   暴露了团队遵循的糟糕的开发实践

如果团队没有选择走捷径，所有这些都是可以避免的。

*   他们忽略了对查询的分析——这是每一个投入生产的代码所必须的
*   他们跳过了性能测试阶段

这里有一些每个软件开发团队和他们的工程师必须学习的教训，以避免承担软件缺陷的成本。

*   **在开发阶段花更多的时间比在生产中修复缺陷要好:**在实现阶段，团队可以花时间分析缺陷，而不会影响生产。没有来自商业用户的压力。开发人员可以采取所有必要的步骤来验证功能，并对他们的代码进行性能测试。
    团队可以为测试阶段的任何问题提供完整的解决方案。他们不必急于获得补丁来使该功能可用。由于代码尚未部署，因此对他们的业务没有影响。
*   **一个软件缺陷的代价不仅仅是金钱:**在某些情况下，一个缺陷可能会导致重大的经济损失、名誉受损和法律诉讼。在其他情况下，一个缺陷可能会导致一些小的不便或烦恼。然而，即使是一个小小的软件漏洞也会耗费公司的时间和金钱来修复。此外，每次在匆忙中发现并修复一个 bug，都会给代码中引入其他问题创造新的机会。因此，团队仔细跟踪缺陷并采取措施在第一时间防止它们是很重要的。通过这样做，从长远来看，团队可以为自己节省时间、金钱和头痛。
*   **软件缺陷可能会导致客户不满，甚至业务损失:**虽然一些缺陷看似简单，但它们可能会产生连锁反应，影响公司及其用户。有时，缺陷可能会导致公司失去潜在客户，甚至迫使他们取消订阅。在其他情况下，软件缺陷会导致数据丢失或损坏，从而导致业务损失或公司声誉受损。
    无论哪种情况，尽快解决软件缺陷以防止对业务的进一步影响都是至关重要的。
*   **软件缺陷的成本超出了直接影响:**当发现缺陷时，软件开发团队通常会感受到直接影响。他们需要从日程中抽出时间来解决问题，这可能会影响项目的整体时间表。然而，软件缺陷的成本不仅仅是直接的影响。如果不快速修复，缺陷可能会产生长期的后果，修复的成本可能会高得多。
    例如，会计系统中的一个小缺陷可能导致产生不正确的财务报告。如果不及时发现并纠正这一问题，可能会导致重大的合规性问题和经济处罚。因此，首先采取措施防止它们发生是至关重要的。
*   **质量没有捷径:**质量保证(QA)应该是软件开发过程中不可或缺的一部分。通过在产品和服务发布给客户之前对其进行测试，团队可以在问题导致客户满意度问题之前识别并修复问题。
    QA 可以在内部完成，也可以外包给第三方提供商。内部 QA 通常更昂贵，但是在开发过程的早期识别缺陷更有效。外包 QA 可能更便宜，但如果供应商没有经验或不可靠，也会导致问题。
    最终，避免缺陷成本的最佳方式是投资质量保证测试。

# 最终想法

软件缺陷的实际成本通常比修复缺陷的初始成本高得多。当考虑间接成本时，很明显防止缺陷应该是组织的首要任务。

谨慎的开发和彻底的测试可以帮助公司避免与缺陷相关的巨大成本，并确保他们的产品符合最高标准。

团队应该将质量保证视为投资，而不是成本。

下次当你试图在编码时走捷径或者跳过一些测试用例时，提醒你自己一个缺陷的真实成本。无论您的更改有多小，都应该经过适当的分析和测试过程。

这可能需要更多的前期时间，但从长远来看，你的勤奋肯定可以为你和你的团队省去很多麻烦。

谢谢你的阅读。如果你喜欢这篇文章，[查看我在媒体上最成功的故事](https://lokajit-tikayatray.medium.com/my-most-viewed-stories-398607ebc257)阅读更多。你也可以通过访问这个推荐链接来支持我的写作[成为一个媒体成员。](https://lokajit-tikayatray.medium.com/membership)

**你可能也喜欢阅读:**

[](/top-6-hybrid-working-mistakes-to-avoid-34e46ff77fed) [## 要避免的 6 大混合工作错误

### #5.没有意识到潜意识的偏见

levelup.gitconnected.com](/top-6-hybrid-working-mistakes-to-avoid-34e46ff77fed) [](/5-signs-of-a-highly-mature-software-developer-a23285e5cf1b) [## 高度成熟的软件开发人员的 5 个标志

### 这些特征很容易识别，但很难实践

levelup.gitconnected.com](/5-signs-of-a-highly-mature-software-developer-a23285e5cf1b) 

# 分级编码

感谢您成为我们社区的一员！在你离开之前:

*   👏为故事鼓掌，跟着作者走👉
*   📰查看[升级编码出版物](https://levelup.gitconnected.com/?utm_source=pub&utm_medium=post)中的更多内容
*   🔔关注我们:[Twitter](https://twitter.com/gitconnected)|[LinkedIn](https://www.linkedin.com/company/gitconnected)|[时事通讯](https://newsletter.levelup.dev)

🚀👉 [**加入升级人才集体，找到一份神奇的工作**](https://jobs.levelup.dev/talent/welcome?referral=true)