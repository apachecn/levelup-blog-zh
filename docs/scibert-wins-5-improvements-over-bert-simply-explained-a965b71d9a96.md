# SciBERT 胜出:比 BERT 提高了 5 点，简单解释

> 原文：<https://levelup.gitconnected.com/scibert-wins-5-improvements-over-bert-simply-explained-a965b71d9a96>

SciBERT 与 BERT，及其应用程序、最佳实践，以及它如何超越 BERT。

![](img/0b06b3fde5ee6e42cd78342481311bcd.png)

你好，我是来自 Unsplash 的 Nik

我正在寻找实现一个基于科学领域见解的 NLP 管道，我偶然发现了 SciBERT，一个预先训练好的用于科学文本的上下文化嵌入模型[2]。在确认它是基于 BERT 的基础上，它变得更有吸引力。稍后会详细介绍。

它在计算机科学和生物医学领域见解的大型出版物语料库上进行训练，目的是为科学文本提供有根据的单词表示，可以应用于各种下游任务，如文本分类、信息检索和问题回答。

首先，需要强调的是，SciBERT 是由艾伦人工智能研究所(AI2) [7]开发的开源项目，艾伦人工智能研究所是一个以“高影响力人工智能研究和工程”而闻名的非营利组织[7]。

![](img/df93c5a3b521116c1d4e93e942db7a7e.png)

由来自 Unsplash 的[this engineering RAEng](https://unsplash.com/@thisisengineering)

# **其训练根源**

基于来自 ELMO [4]、GPT [5]和伯特[6]的语言模型[2]的无监督预训练，观察到 NLP 任务[2]的显著性能改善。为了将它与 SciBERT 联系起来，有必要强调训练 SciBERT 的内容的绝对规模(在一个大的计划中，这个陈述对于这种类型的 NLP 任务非常重要):

## 1.14M 纸，3.1B 代币[7]。

虽然 SciBert 是自然语言处理(NLP)算法方法的一部分，并且是专门为科学应用设计的，但它在核心上是 Bert 的变体:

> SciBERT 是一个预先训练好的基于 BERT 的语言模型，旨在执行科学任务。

为了了解 BERT，我将在底部简单地链接与之相关的研究论文[9]。

考虑使用它的搜索功能来分析相关的科学论文或查找任何研究任务所需的数据集。此外，SciBERT 可以帮助您开发假设，并根据可用数据对其进行测试。回想一下，BERT 是它的根，SciBERT 就是通过它建立的；因此，许多可以跨 BERT 实现应用的功能也适用于这种情况，比如使用它来创建结果的可视化。

![](img/564f323c74bd535011aedec060e44de4.png)

来自 Unsplash 的 Shane Rounce

# **为什么赛伯特会发光**

它提高了文本分类和信息提取任务的准确性。在科学任务的应用中，SciBERT 受到其概括能力的影响。也就是说，它可以从更少的训练样本中学习，但仍然可以在看不见的数据上获得良好的性能。

SciBERT 还提供了一些比其他语言模型更容易理解和解释的特性，因为它针对分析跨科学任务实现的特定任务进行了优化。

将自动化视为建立跨科学文献搜索的任务，整个人工智能社区正在努力开发专门用于从 PubMed 或 arXiv 等大型数字图书馆检索相关论文的神经网络模型。挑战并不明显(从技术上来说)，就像与长尾查询(即只有几个文档相关的查询)的斗争一样，因为从有限的数据中学习不同的概念很困难。像 SciBERT 这样的 transformer 模型的泛化能力在这一领域提供了潜在的前景，提供了一种在没有人工监督的情况下从零开始在任何给定的文本数据集上有效学习信息检索启发式的方法。

![](img/658d061a20cad10b300c36e04e6b5865.png)

来自 Unsplash 的 Alain Pham

最先进的性能是凭经验获得的(至少是为了在 AI 社区中使用它的目的)。在基于文献的发现[10]的背景下，基于文献的发现(LBD) [11]是通过读取和挖掘大量文本数据来发现实体之间新关系的过程。后一项工作传统上由专家研究人员手动执行，但近年来已经看到了基于机器学习和自然语言处理算法的自动化方法的兴起。这些方法，像 SciBERT 一样，有可能在简单的 LBD 任务中展示有希望的结果。SciBERT 处理长文档的机会和它从小数据集学习的能力使它成为一种可能的、有前途的处理更复杂的 LBD 任务的方法。

作为一项任务，科学问答可以结合机器学习的应用来回答关于文本(如研究论文或期刊文章)中存在的信息的问题。这是一个具有挑战性的用例，因为需要深入理解文本段落和问题，并且可用于解释的上下文通常有限。已经提出了几个神经网络模型来处理这项任务，但是像 SciBERT 这样的变压器模型可以很好地解决这个问题空间，特别是实现最先进的结果。

![](img/9b71a8ae31f8ddcc3f6c40f07f29a0f1.png)

这个工程来自 Unsplash

# **SciBERT 有哪些潜在的应用？**

让我们先详细列举这些(BLUF):

—最先进的文本处理:凭借其强大的文本处理能力，SciBERT 可以帮助最终用户从冗长复杂的文本(如研究论文或法律文档)中提取含义。当一项任务需要快速消化大量信息时，利用一项功能的机会，尤其是当它们是开源的时候，尤其有影响力。

—文本数据挖掘:凭借其在文本数据中识别模式的能力，SciBERT 可被实现用于各种与文本数据挖掘相关的任务(由于采用了 BERT 的能力和功能)。举例来说，它可以被构建成按照主题或流派对文章进行自动分类，或者识别科学文献中的新趋势。

![](img/ad197a0a7f15d1a3a102f16ee4d2c046.png)

由 Unsplash 的 this engineering RAEng

—进行大规模研究:SciBERT 快速处理大量数据的能力使其成为进行大规模研究的理想选择。例如，最终用户可以实现 SciBERT 来分析任何数据，显然是为了在科学源内容中应用它。

—支持基于证据的决策:数据的日益普及意味着越来越多的决策需要基于证据做出(基于数据的决策比基于数据的决策更多)。SciBERT 可以帮助管理者和决策者筛选堆积如山的信息，找到做出明智决策所需的真知灼见。

—增强人机交互:SciBERT 的自然语言处理能力可以在人类和计算机之间建立更好的界面。考虑如何部署它来开发聊天机器人，以提供与用户或虚拟助理更自然和有效的交流，从而更好地理解用户的需求并准确地满足他们的请求。

![](img/c76c153010a0ad52569c9973f0a7af05.png)

由来自 Unsplash 的[大卫王子](https://unsplash.com/@bravoprince)

# **离别的思念**

BERT 为我们在人工智能方面的许多能力奠定了基础，特别是基于自然语言处理和机器学习的开源方法的实现。此外，SciBERT 建立在 BERT 基础之上，允许进行专门的分析，这是我每天在科学任务中激活的一个用例(总的来说，这要感谢 BERT)。

如果你对这篇文章的编辑有任何建议，或者对进一步扩展这个主题领域有什么建议，请和我分享你的想法。

## 另外，请考虑订阅我的每周简讯:

[](https://pventures.substack.com) [## 产品。风险时事通讯

### 产品和人工智能交汇处的想法。点击阅读产品。投资时事通讯，作者安尼尔…

pventures.substack.com](https://pventures.substack.com) 

*参考文献:*

*1。安特吉尼，m .，德索萨，j .，桑托斯，V. A. P. M .多斯，&# 38；奥尔，S. (2020 年 9 月 16 日)。开放研究知识图中基于 SciBERT 的生物测定语义化。ArXiv.Org。*[](https://arxiv.org/abs/2009.08801)

**2。Beltagy，I .，Lo，k .，&# 38；Cohan，A. (2019 年 3 月 26 日)。SciBERT:科学文本的预训练语言模型。ArXiv.Org。*[*https://arxiv.org/abs/1903.10676*](https://arxiv.org/abs/1903.10676)*

**3。马赫什瓦里，h .辛格，b .，&# 38；瓦尔马，v .(未注明)。引文上下文分类的 SciBERT 句子表示。ACL 选集。检索到 2022 年 8 月 9 日，来自*[*https://aclanthology.org/2021.sdp-1.17/*](https://aclanthology.org/2021.sdp-1.17/)*

**4。马修·e·彼得斯、马克·纽曼、莫希特·伊耶、马特·加德纳、克里斯托弗·克拉克、肯顿·李和卢克·s·塞特勒莫耶。2018.深层语境化的词语表达。在 NAACL-HLT。**

**5。亚历克·拉德福德、卡蒂克·纳拉辛汉、蒂姆·萨利曼斯和伊利亚·苏茨基弗。2018.通过生成性预训练提高语言理解能力。**

*6。雅各布·德夫林、张明蔚、肯顿·李和克里斯蒂娜·图塔诺娃。2019.BERT:用于语言理解的深度双向转换器的预训练。在 NAACL-HLT。*

*7。阿莱奈。(未注明)。GitHub — Allenai/scibert:科学文本的 bert 模型。GitHub。检索到 2022 年 8 月 9 日，来自[*https://github.com/allenai/scibert/*](https://github.com/allenai/scibert/)*

**8。allenai/scibert _ scivocab _ uncased 拥抱脸。(未注明)。检索到 2022 年 8 月 9 日，来自*[*https://huggingface.co/allenai/scibert_scivocab_uncased*](https://huggingface.co/allenai/scibert_scivocab_uncased)*

**9。Devlin 等人 BERT:用于语言理解的深度双向转换器的预训练。*[*https://arxiv.org/pdf/1810.04805.pdf*](https://arxiv.org/pdf/1810.04805.pdf)*

**10。本施。(2021 年 1 月 1 日)。基于文献的发现的新方法。*[*https://elib.dlr.de/147246/*](https://elib.dlr.de/147246/)*

**11。基于文献的发现:模型、方法和趋势。(未注明)。生物医学信息学杂志，74，20–32。*[](https://doi.org/10.1016/j.jbi.2017.08.011)*

# **分级编码**

**感谢您成为我们社区的一员！在你离开之前:**

*   **👏为故事鼓掌，跟着作者走👉**
*   **📰查看[升级编码出版物](https://levelup.gitconnected.com/?utm_source=pub&utm_medium=post)中的更多内容**
*   **🔔关注我们:[Twitter](https://twitter.com/gitconnected)|[LinkedIn](https://www.linkedin.com/company/gitconnected)|[时事通讯](https://newsletter.levelup.dev)**

**🚀👉 [**加入升级人才集体，找到一份神奇的工作**](https://jobs.levelup.dev/talent/welcome?referral=true)**