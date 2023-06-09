# 数据科学最重要的两项研究:受控组与变量

> 原文：<https://levelup.gitconnected.com/2-most-important-studies-for-data-science-controlled-group-vs-variable-ed4ccd46a34e>

简单解释它们之间的相互作用以及如何在人工智能中应用它们

![](img/0c6b52668406113bd6dbb2754d76face.png)

来自 Pexels 的懒惰艺术家画廊

这些概念不仅仅是一大群人的面孔——学习它们来增加你的理解，永远不要担心如何再次掌握它们。

**如果你从事任何分析工作，学习受控组和受控变量的一般原理是至关重要的。**

底线(BLUF):让我们开门见山。

在实验中，一组没有接受独立变量[2]的受试者被称为控制组。这使得研究人员能够通过维持现状来区分因变量和其他变量的影响。对照组有几个不同的名称，包括对照组和基线组。

在科学研究中，“受控变量”指的是任何可以以某种方式改变的因素。通过控制变量，科学家可以评估研究结果是否归因于他们对因变量的操作的影响，或者它们是否仅仅是由其他因素驱动的，如偶然事件或混杂变量[1]。

实验组和安慰剂组是可用的两种类型的对照组。参与实验的一组受自变量影响，而另一组，即安慰剂组，则不受自变量影响。安慰剂对照用于将个体暴露于潜在危险的治疗(如新药)是不道德的试验。

在进行科学研究时，使用受控组是必不可少的。没有它们，就很难区分各种因素的影响并恰当地解释数据。仅使用一个对照组或不使用对照组的实验可能经常导致无法重复的错误发现。

![](img/319ed74afa07a5315f4ac56b51d0cb2b.png)

来自 Pexels 的懒惰艺术家画廊

# 哲学——相互影响是什么？

受控组是在相关方面相似的一组个体，而控制变量是在测量标准中保持不变的独立变量。**在哲学的背景下，**这些术语可以用来指思想实验和人工智能(AI)系统的理论构建。

哲学家有时会从事进行思维实验的实践，以便在不依赖于实际事实的情况下调查假设场景或检验概念。例如，一个人可以通过围绕黑洞做一个思维实验来试图更深入地理解因果关系的本质。有效的思维实验的最重要的特征之一是创建受控组，假设参与者之间的所有其他因素都相同，这为关于因果的更直接的推断铺平了道路。相比之下，人工智能系统通常包含大量关键变量，很难查明特定的原因和后果(例如，在维数灾难的背景下)。

![](img/f2fa28cf36f4d5b2703a99fe152a8a95.png)

来自 Pexels 的懒惰艺术家画廊

# 在数据科学中如何应用？

在进行数据分析时，受控变量是隔离单个变量或元素影响的有用工具。例如，如果您想评估各种营销方法如何影响消费者的行为，您可以控制各种特征，如年龄、性别、收入水平等。这样，你就可以在不受其他因素影响的情况下，检查每种营销技术是如何影响顾客的，这些因素可能会影响你的判断。同样，在比较两组(例如，治疗组和对照组)的实验中控制参与者特征确保了组之间的任何差异是实验干预的结果，而不是组之间存在的一些其他差异。

# 人工智能应用

数据科学中受控变量的一个潜在用途是在回归分析的上下文中使用它们来挑选出某个预测变量的影响。如果你想发现各种营销方法是如何影响销售的，你需要控制诸如经济、公司规模和其他类似方面的特征。关于营销，以下是几个进一步的例子:

1.如果你想评估替代定价技术如何影响消费者的行为，你需要控制各种参数，如年龄、性别和收入水平。

2.如果你想研究产品质量对顾客满意度的影响，控制价格和交付时间等因素可以让你把注意力集中在质量的影响上。

3.如果你进行了一项调查，以了解人们对税收的看法，控制年龄和收入等特征将使你能够评估各种税级如何影响人们的看法。

4.如果你想调查员工流动与工作满意度之间的关系，控制像补偿和津贴这样的因素会让你专注于工作满意度的影响。

![](img/db06f9e6e20baf1032083fd65587898a.png)

来自 Pexels 的懒惰艺术家画廊

# 在数据科学中，对于受控变量 vs 受控群体，如何使用机器学习？

您可以使用机器学习来开发一个只包含感兴趣的预测变量(即受控变量)的预测模型。这种方法将允许您隔离每个变量对感兴趣的结果的影响。这里有几个例子:

—如果您想要预测客户是否会购买产品，您可以开发一个仅包含与产品相关的预测变量(例如，功能、价格等)的模型。)，而不是年龄或性别等其他变量。

—如果您想要开发一个模型来预测人们对其工作的满意程度，您可以创建一个只包含与工作相关的预测变量(例如，报酬、工作量和发展机会)而排除年龄或婚姻状况等无关因素的模型。

—一家保险提供商希望开发一种方法来预测哪个客户更有可能提交索赔，以便更准确地指导其营销工作。企业创建了两种不同类型的预测模型:一种使用客户的人口统计信息(如年龄和性别)，另一种使用客户的行为驱动历史信息。保险公司可以通过比较这两个模型的准确性并分析结果来确定每组预测变量与预测目的的相关程度。

# 受控变量与受控组的无监督学习应用

受控变量可用于隔离特定因素的影响，而受控组允许在不同干预对象之间进行比较。在数据科学中，可在聚类算法中使用受控变量将相似的示例分组在一起，受控组可使用两步聚类方法[4]，该方法涉及初始分配步骤，随后是顺序搜索程序。

# **离别的思念**

如果你对这篇文章有任何建议或拓宽主题的建议，我将非常感谢你的来信。

如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑报名成为一名媒体成员。一个月 5 美元，你可以无限制地阅读媒体上的所有报道。如果你注册使用我的链接，我会赚一小笔佣金，不需要你额外付费。

[](https://medium.com/@AnilTilbe/membership) [## 通过我的推荐链接加入 Medium-Anil til be

### 阅读阿尼尔·蒂尔贝(以及媒体上成千上万的其他作家)的每一个故事。你的会员资格直接支持作家…

medium.com](https://medium.com/@AnilTilbe/membership) 

## 下面是我写的一个帖子，大家可能会感兴趣:

[](/deductive-inference-vs-bias-in-artificial-intelligence-simplified-74774e65393a) [## 演绎推理与人工智能中的偏见，简化

### 人工智能如何从哲学中学习，以改善现实世界人工智能应用的算法

levelup.gitconnected.com](/deductive-inference-vs-bias-in-artificial-intelligence-simplified-74774e65393a) 

```
Also, here is my newsletter; I hope you will kindly **consider subscribing**.[https://predictiveventures.substack.com](https://predictiveventures.substack.com/)
```

**参考文献:**

1.通过体验教育创造成果:混杂变量的挑战。[https://journals . sage pub . com/doi/ABS/10.1177/105382590803100305](https://journals.sagepub.com/doi/abs/10.1177/105382590803100305)

2.库恩等人发展科学思维都是为了学会控制变量吗？
[https://journals . sage pub . com/doi/ABS/10.1111/j . 1467-9280 . 2005 . 01628 . x](https://journals.sagepub.com/doi/abs/10.1111/j.1467-9280.2005.01628.x)

3.蒂尔贝，阿尼尔。(2022 年 8 月 18 日)。演绎推理与人工智能中的偏见，简化。升级编码。[https://level up . git connected . com/deductive-inference-vs-bias-in-artificial-intelligence-simplified-74774 e 65393 a](/deductive-inference-vs-bias-in-artificial-intelligence-simplified-74774e65393a)

4.无监督学习的贝叶斯聚类计数准则。(未注明)。IEEE Xplore。[https://ieeexplore.ieee.org/abstract/document/8443157/](https://ieeexplore.ieee.org/abstract/document/8443157/)

阿尼尔·蒂尔贝