# 让您的数据项目走向成功的 5 个步骤

> 原文：<https://levelup.gitconnected.com/5-steps-to-set-your-data-projects-up-for-success-87b85fa3343e>

## 数据项目

一步一步地加强数据关系

![](img/e326625374f0c1bf0f86818d5a4d5b20.png)

米卡·鲍梅斯特在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

建立关系是复杂的。等等，什么？为什么我们要在这篇文章中谈论关系？和我一起坚持住！

你花了多长时间和你的朋友建立关系？信任怎么样？这通常需要时间、精力和坚持。

同样，我们需要与数据建立关系。我们中的许多人没有意识到，由于糟糕的软件实践或资源不足，我们与数据的关系受到了污染。而且，很难鼓励高层管理人员投资一个与数据无关或已被证明无效的项目。

很自然地，这让我们想知道我们是否能与这些数据保持健康的关系。我相信我们能做到。具体来说，时间、努力和一致性可以修复数据关系。

我将讨论这五种方法，它们将为您建立与数据的关系提供垫脚石。

1.  **一段感情需要强大的基础**

与数据建立关系的第一步是将所有数据管道和转换放在一个位置。

当一段关系开始时，我们需要建立一个坚实的基础。我们通常通过花时间在一起，弄清楚我们是否有共同爱好等等来建立这种关系。你和数据的关系也是如此。我们需要弄清楚我们的数据管道在哪里，它们在拉什么数据，等等。这些初步调查将为我们提供坚实的基础。

我很惊讶有多少次我看到到处都是数据管道。我是说任何地方。有些会在办公室的 mac 上运行的旧数据库中运行，有些会在 Azure Data Factory 上运行，有些会在虚拟机上运行。每个位置的代码都有不同的变化，所以我不确定哪一个是真实的。如果这些数据管道中需要发生变化，我们会手动更新它们*。结果，在我与数据的关系中，我遇到了一大堆棘手的问题。*

当我将所有代码都转移到 Github 中时，结果令人吃惊，这样我们现在就有了一个确定的事实来源，并且可以跟踪版本。

**2。关系需要多种经历**

与数据建立关系的第二步是提供一种氛围，在未知的环境中进行测试之前，我们知道会发生什么。

每当我第一次或第二次见到某人时，我倾向于选择一个我感到舒适的地方。我知道会发生什么。在同样的情况下，我们需要首先选择一个我们感到舒适的地点。在我们的区域中，这个区域将被称为暂存区域，本质上是没有最终用户的生产副本。这个临时区域不会处理所有可能的问题，但它会限制我们在生产中获得的数量。

这将限制由我们的转换导致的错误数量，建立我们与数据的关系。

**3。平衡你的注意力**

第三步是限制数据库查询中的转换次数。

建立关系需要专注和用心。如果任何一方在关系中做得太多，关系就不会成长。这通常会导致重新确定优先顺序或自我检查。

随着关系随着数据的增长而增长，并且建立了第一个初始数据仓库，数据仓库可以处理转换和为报告提取数据。然而，随着产品和数据的增长，转换将变得更加突出，并占用更多的资源，导致数据库超负荷工作和查询失败。

为了在转换和查询之间建立健康的平衡，我们需要限制数据库中转换的数量。在这种情况下，您的团队最清楚，但这里有一些建议。如果您有大量的数据，使用 Spark 之类的工具来运行这些转换会很棒。与此同时，Python 代码可以快速处理小型数据集。

我将 SQL 中的转换转移到 AWS Redshift 和 Tableau 中，将它们翻译成 Python，将这些管道容器化，并使用 AWS Fargate 连续运行它们。

**4。审视你的关系**

第四步是看你的数据模型。

你想从这段关系中得到什么？是否有零件丢失？你可以问什么样的问题来发展这种关系？

这基本上就是您在分析数据模型时所做的事情。数据建模捕获数据库中数据的语义和结构。它包括识别表示数据库中的信息所需的实体、属性、关系和约束。

一个好的数据模型应该易于理解、维护和使用。此外，它的结构应该对需要使用它的人有意义，并建立在反映业务需求的可靠的数据库设计上。

有一些迹象表明您的数据模型需要更新:

1.  数据库中的 SQL 查询超过了一页。
2.  您的 SQL 查询运行时间超过一分钟。

重新分析数据模型需要定期进行——这是一个迭代过程。随着您对数据的了解越来越多，您的关系也越来越密切，您的数据模型将会得到改进。

**5。定期签到**

在每一段关系中，大多数人都会定期查看对方的情况。那么，我们为什么不用我们的数据来做这件事呢？

第五步，定期检查自己的数据。在所有步骤中，这一步是最耗费精力和时间的，因为它需要定期重复，就像建立关系一样:)。

首先，我们需要对数据进行数据分析。与流数据相比，查看批量数据相对简单。您可以“扫描”您的数据，并返回空值的数量、列的平均值和中值以及类似的指标。

每当我们将这些指标运行到一个指标存储库时，我们都需要保存它们。

最后，我们需要根据历史价值来分析这些价值。异常值将出现在数据中，我们可以使用 z 得分或异常检测快速识别。一旦确定了这些奇怪的值，就会发送一个通知。

使用类似于 [flyte](https://dutchengineer.medium.com/processing-data-using-flyte-778cafd70d6e) 或 [prefect](https://dutchengineer.medium.com/airflow-theres-a-new-competitor-in-town-d59b48a642ff) 的东西，我们可以批量计算这些指标，并得到 Slack 或 PagerDuty 的结果。同样，我也设置了类似于 [re_data](https://dutchengineer.medium.com/get-ahead-by-monitoring-your-data-quality-with-this-free-package-2553bdc26f77) 或 [deequ](https://medium.com/codex/how-to-check-data-quality-in-pyspark-8a882e45bc95) 的东西。

我还在学习如何检查流数据源的数据质量。你可以说我对速配数据没有任何经验。哈。

**结论**

发展关系需要时间、精力和一致性，尤其是在数据方面。建立这种牢固的关系需要强大的数据管道基础，各种经验，平衡你的重点，检查当前的关系，最后，定期检查。你会发现，实施这些步骤会让你们的关系更加牢固。最终，这种牢固的关系会让你有成功的项目。