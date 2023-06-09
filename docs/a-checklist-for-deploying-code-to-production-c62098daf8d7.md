# 将代码部署到生产环境的清单

> 原文：<https://levelup.gitconnected.com/a-checklist-for-deploying-code-to-production-c62098daf8d7>

![](img/74ebbdd7780d45be5186534c96167f53.png)

格伦·卡斯滕斯-彼得斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## 如何让您的部署更加可控

每个开发人员都知道，在开发了一些奇特的特性之后，是时候部署代码了。然而，将代码部署到产品中既令人兴奋又让人害怕。你当然不想打破任何东西。您可能对自己的工作很有信心，但是别人实现的那个特性呢？

为了确保一切顺利，你需要检查，检查，再检查。目的是让你的部署尽可能可控，这样你就可以限制可能出错的事情的数量。这就是为什么我们要查看这个清单的原因，您可以在将代码部署到产品时使用它。

# 知道你在版本控制中放了什么

我假设任何有自尊的开发人员或团队都使用某种存储库管理工具，如 GitLab 或 BitBucket。如果没有，你可能应该。它有很多优点，我现在甚至不想在这里列出来，因为优点列表太长了。

好了，回到正题。确切地知道您在版本控制中放入了什么是极其重要的。有些文件是您不想在版本控制中看到的，比如*。包含所有环境变量的 env* 文件。确保您屏蔽了密码，或者更好地将它们与环境变量一起放在您的文件中。不要忘记隐藏私钥。

影响较小但肯定不是您想要的是将 IDE 中的配置文件放在您的版本控制中。

# 测试

在部署任何一段代码之前，都应该进行彻底的测试。测试代码有不同的程度。尽管大多数开发人员不喜欢测试，但也不应该轻视测试。

代码审查应该是每个团队日常工作的一部分，以便有一双额外的眼睛来观察正在部署的东西。这将过滤掉最明显的错误，并确保代码满足一定的质量要求，比如格式正确。

在最好的情况下，编写代码应该与为同一段代码编写自动化测试齐头并进。自动化测试给了开发人员更多的信心，因为开发人员可以测试这些变化是否会导致其他问题。

# 管道

软件工程团队中的管道是一组自动化流程，允许开发人员和 DevOps 专业人员可靠、高效地编译、构建和部署他们的代码到他们的生产计算平台

管道在某种程度上是灵活的，你可以按照自己的意愿来配置它们，因为没有一成不变的规则来规定它应该是什么样子，应该做什么。然而，管道最常见的组件是构建自动化、测试自动化和部署自动化。

如果你正在使用 GitLab 或 BitBucket，拥有一个管道是一个真正的救命稻草。因为在大多数情况下，代码每天都会被集成到一个共享的存储库中几次，所以您希望通过自动化构建来验证代码，这样可以让您尽早发现问题。最重要的是，您希望确保对代码的每个更改都是可发布的，就像按下按钮一样简单。

管道允许您自动化所有种类的测试——从单元测试到代码格式是否正确的测试。

当一个管道被很好地实现时，它会使发布变得乏味，并增加你交付的频率。这导致了用户真正关心的快速反馈循环。

# 何时部署？

或者，最好问这样一个问题:何时不部署？这个回答大概就简单很多了。最好不要在下午晚些时候部署，因为这让你几乎没有时间来修复事情，以防事情变糟。在一天的早些时候将您的代码部署到生产环境中，让您有足够的时间来恢复更改或修复它们。

我也见过出于同样的原因而避免在周五部署的团队。一些团队甚至对他们的部署日更加极端——他们只在一周的前几天进行部署。

严格遵守您在团队中商定的关于何时部署的规则。您可能会发现自己处于这样一种情况，即在部署之后就需要修复一个关键的 bug，因为它会使应用程序的一个重要部分崩溃。您需要足够的时间来处理修补程序。

# 备份

虽然这一点听起来很明显，但最终实现备份的时候通常已经太晚了。一旦您需要备份，通常就会实施备份。你开始怀疑是否真的有备份。那时候你就太晚了。

如果您使用管道，您可以自动化这个过程。例如，您可以在每次部署到生产环境时创建一个数据库转储。您也可以选择不同的备份策略，比如每天一次。

# 重大时刻

终于！重要的时刻到了。该部署了！

你和你的团队所付出的所有努力都将投入生产。这一步本身不会给你带来任何麻烦。既然您已经完成了我们所经历的所有步骤，现在这应该是小菜一碟。

如果您通过管道进行部署，您应该可以获得测试是否通过以及代码格式是否正确的即时反馈。如果您没有使用管道，并且某些东西可能会出错，那么总是有恢复的可能性。一旦恢复成功，您可以更好地了解实际问题是什么。

# 在实时服务器上测试

现在您已经部署好了，一切都正常了，是时候进行最后一步了。该清单的最后一步是在应用更改后检查您的实时服务器是否有错误。尽可能彻底，因为让你的团队注意到一个 bug 并记录下来比把工作留给客户要好得多。

如果您发现了一个您无法忽视的关键 bug，甚至可能值得考虑回滚。希望，由于所有以前的检查，这不应该是这种情况。如果您使用某种敏捷方法，当在活动服务器上发现小错误时，它们可以作为新的用户故事来报告。

# 总结:清单✅

正如我们所经历的，清单看起来像这样:

1.  知道*什么*将被部署
2.  过度测试；优选地使用具有自动测试的流水线
3.  知道*什么时候*会被部署
4.  创建备份
5.  部署到生产环境
6.  在实时服务器上测试

当遵循这个清单时，部署应该不那么混乱，让它们更无聊——这是一件好事。

> 让你团队的部署变得无聊透顶，不要再为此感到压力——扎克·霍尔曼