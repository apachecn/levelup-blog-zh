# 黑仔神经网络模型的 3 个关键组件

> 原文：<https://levelup.gitconnected.com/3-crucial-components-for-a-killer-neural-network-model-81dca0fa9c01>

## 人工智能并不适合所有人

## 如何开始构建神经网络

![](img/982aa9efc0b476a925f663cf45371aa2.png)

人工智能背后的嗡嗡声是什么？科技和非科技公司都投入了大量资源，将人工智能融入他们的产品和业务运营中。许多公司试图使用客户服务机器人、[交互式语音应答(IVR)](https://www.ringover.com/guides/interactive-voice-response) 和电子邮件自动化来优化他们的运营方式。对于任何想要在竞争中领先并优化资源利用的公司来说，自动化的想法本身就有着巨大的吸引力。

我的公司[center field Media-Science and Technology](https://medium.com/u/e5f4b7431c6f?source=post_page-----81dca0fa9c01--------------------------------)，也不例外。作为一家端到端的客户获取公司，我们始终希望确保我们的销售代理能够推动收入和转换率。我们需要能给我们的代理商增加销售和保持销售的工具的系统。我的经理、首席数据科学家和我被赋予了帮助创建成功系统的任务。

经过大量研究，我们的团队决定建立一个神经网络。对于那些好奇的人来说，神经网络是一种试图模仿我们的神经元如何做出决定的人工智能。我们的神经网络将利用语音数据来生成有根据的代理性能分数。

当我们试图建立我们的神经网络时，我们经历了许多成功，也面临了一些障碍。我将与你们分享促成我们的神经网络模型成功的三个关键因素。你将带着构建一个杀手神经网络模型的钥匙离开，以及你如何自己开始一个杀手神经网络模型。准备好了吗？让我们开始吧。

**确定你的商业目标**

![](img/081c1eac814664351a6364599a462e70.png)

科技界有句谚语:“你能做到，并不意味着你应该做到”。技术人员和工程师在为他们各自的公司考虑新技术时都使用这种哲学。如果新的软件、工具和技术能给你的企业带来合法的价值，它们就是伟大的。但是如果你使用这些东西是因为这是一件很酷的事情，那么你就是在浪费宝贵的资源。神经网络完全符合这个类比。许多公司希望建立神经网络，因为他们知道这将优化他们的运营或增加他们的收入。但许多其他公司希望建立神经网络，而不了解它对他们的组织到底有什么作用。

我们的数据科学团队有一个简单明了的目标:创建一个解决方案，准确无误地自动化代理评分。我们的需求非常微妙和具体，所以我们知道通用的解决方案不会帮助我们-我们需要一个定制和简化的方法来评分我们的代理人的表现。

我建议你弄清楚你的商业目标是什么，以及神经网络模型将如何帮助你。请随意探索和创建概念证明。享受学习的过程。但是你应该到达一个点，在那里你确切地知道你正在试图完成什么，以及你期望神经网络产生什么。

**获取大样本数据**

![](img/7136bb0c42fda2231a0ffbb1a99eaed7.png)

在构建神经网络时，数据将是你最好的朋友。让我们后退几步，考虑一下神经网络是如何工作的。还记得我提到过神经网络试图模仿我们的神经元如何做出决策吗？我们的大脑试图挖掘尽可能多的过去经历，以便做出明智的决定。以在停车标志前停下来为例。当你考虑是否应该停车的时候，你的大脑会在所有你没有闯停车标志的时候运行。神经网络以非常相似的方式工作，除了你是给它提供数据的人。神经网络需要你给它输入数据或“训练”它，让它尽可能做出明智的决定。

对于我们的神经网络模型，我们需要输入尽可能多的干净数据。我们给它输入了数百份演讲记录，这些记录产生了数百万的数据输入。字数、焦虑、通话时长，应有尽有。这些数据输入将训练我们的神经网络在一个清晰明确的模式下运行。最后，我们的模型对一组测试人员的依从性进行了分级。该模型的等级与我们的质量保证团队手动执行的 90%以上的等级相匹配。

你给你的模型提供的数据越多，它的结果就越准确和全面。我强烈建议您找到一个尽可能多变化的干净数据源。随着时间的推移，您的模型将学会预测和识别模式。结果呢？一个更明智、更准确的模型，只会提高贵公司的效率。

## **留出充足的训练时间**

![](img/6cff56b82a885c1962514a680092f87d.png)

还记得我说过数据会是你最好的朋友吗？时间将是你第二好的朋友。神经网络的价值只会随着时间的推移而增加。为什么？时间意味着数据的更大可变性。如果你给你的神经网络输入上个月的一百万个数据，你只能看到一个月的变化。但是，如果你给你的模型输入一年的数据，你就可以获得更大范围的数据。一个伟大的神经网络将有能力作出二阶和三阶决策。模型能够执行这些类型的决策的唯一方式是它是否有正确的数据。如果你想要正确的数据，你需要更多的时间。

我们经历了惨痛的教训。我们接收数据的应用程序编程接口(API)将我们限制在最后三个月。在一个理想和完美的世界里，我们会有年复一年的数据。但是我们不断调整和建设。我们找到了访问额外几个月数据的方法，并用这些数据训练了我们的神经网络。

有时你在时间的紧要关头产生结果。但是如果你可以选择是否花更多的时间来训练你的模型，选择花更多的时间。你的神经网络只会受益于更大的数据广度和可变性。

**说到底，都是数据的问题**

![](img/8935ff5f78dd96772daa30111ce00698.png)

神经网络，以及更大的人工智能技术套件，是难以置信的工作。对于人类可以利用人工智能做什么，我们只是触及了表面。公司正在继续寻找新的和创新的方法来集成人工智能。聊天机器人、IVR 和电子邮件自动化变得越来越普遍。

不知道从哪里开始构建神经网络？确定你的商业目标。一旦你找到一个有价值的商业目标，定位你的数据所在的位置。确保数据是干净的、可用的和可访问的。最后，确定你的时间门槛。你在赶时间吗？你的模型的卓越操作需要超过它的准确性吗？如果其他条件相同，多花点时间。

你现在有了构建杀手神经网络模型的三个关键要素——不要让它白白浪费掉。您现在就可以开始构建，可能性和应用是无穷无尽的。你只需要找到一个建造的理由。