# 对不小心使用 git 的惩罚

> 原文：<https://levelup.gitconnected.com/punishment-for-not-being-careful-using-git-f9e132797b91>

## 响应性地使用版本控制

特征标志为我节省了大量时间

这是一个真实的故事。

![](img/addac33591a802325e1272962f267857.png)

来自 [Pexels](https://www.pexels.com/photo/man-wearing-the-joker-makeup-3078404/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 的照片 [Jhefferson Santos](https://www.pexels.com/@diiefao?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

如果不小心的话，这很容易发生在任何人身上，因为这个问题非常简单，并且可能导致破坏性的后果。

# 方案

我当时正在开发一个受控的功能，非常敏感。**我们应该通过一次在不同的地理位置展开来实现它**，并且由管理层决定何时在哪里部署。

这一变化不是很大也不复杂，但却是至关重要的，因为它为一些符合条件的客户提供了内容。

**我进行了更改，并将我的更改直接合并到主/主分支中。因为我只参与了那个项目，所以我相信除了我自己，没有人会碰那个代码。**

我开始在较低的环境中测试代码，从开发到测试，然后验收，预生产…

我有 3 天假期，加上周末，一共是 5 天假期。我去度假了。

当我回来的时候，在 scrum 电话中，我听说有人正在对我的代码进行紧急 bug 修复，必须立即投入生产。

我的天哪，我完全忘记了我的变化是在主和这个紧急错误修复它也得到了部署。

我一个月都没注意到有什么变化。

一个月后，**我听说了一个错误，我们正在向一些没有资格获得免费频道的客户提供免费频道。**

> 我想，这可能是一个计费问题，我没有任何关系。

***但作为一种不可避免的罪过，它降临到了我的头上*** ，当我随意检查一些账户的数据时，我发现有一部分数据本不应该在生产中，但它们却在这里。

我立即召集了一次会议，并描述了所发生的事情，但幸运的是，我的功能受到了一个**功能标志**的保护，该标志限制了大多数帐户，但无法阻止一些具有典型用例的帐户。

我立即删除了该功能，并在白天以循环方式重新部署。

我真的很幸运，因为这些原因:

## 快速部署设置

由于我们的数据中心和灾难恢复设置具有真正可靠的故障转移和回切功能，我们可以灵活地进行日间部署。

## 特征标志

我的功能被一个功能标志保护着，限制了大部分账号。事实并非如此，我们已经失去了一百万美元的免费服务。

## 经验

我能够修复和重新部署由我维护的代码。如果由新来的人来处理，周转时间就不会这么短。

# 外卖:

## 使用分支

从那以后，我对树枝有些尊敬。每当我做一个改变时，无论是小的还是大的，我都是在一个单独的分支中做，并在部署完成时合并到 master，而不是在此之前。

## 如果可以的话，使用特征标志

我也开始尊重特色旗帜。他们真的救了我一命..如果不是这样，我会有一个很糟糕的伤疤。

## 不要自信，要负责

我们永远不知道谁将在何时做什么工作。在这个竞争激烈的行业里，在任何情况下都保持谨慎是不可或缺的。

如果你喜欢这个帖子，请分享或评论这个帖子。任何形式的互动都是非常受欢迎的。如果你想支持我，并获得所有伟大的事情，请加入并成为会员。这是我的推荐链接:

[](https://susamn.medium.com/membership) [## 用我的推荐链接加入媒体

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

susamn.medium.com](https://susamn.medium.com/membership)