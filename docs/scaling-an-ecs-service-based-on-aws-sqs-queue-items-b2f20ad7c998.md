# 基于 AWS SQS 队列项目扩展 ECS 服务

> 原文：<https://levelup.gitconnected.com/scaling-an-ecs-service-based-on-aws-sqs-queue-items-b2f20ad7c998>

## 本文将帮助您根据 AWS SQS 项目中的项目数量来扩展 ECS 服务。

![](img/a0d819d43c85033347c73f073a8c71c5.png)

照片由[詹姆斯·哈里逊](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

当您有一个脚本或服务处理一个必须处理高峰时刻的队列时，扩展 ECS 服务可能是必要的。您可能希望有更多的进程并行地从队列中挑选项目，这样队列的处理速度会更快。

这是我最近不得不做的事情，并不是没有斗争，希望你在读完这篇文章后会少一些麻烦。毕竟这并没有那么难。

我将在本文中使用 Terraform，但是您当然可以在 AWS 控制台中手动创建这些资源。如果你还不熟悉它，Terraform 是一个基础设施即代码(IaC)软件工具，允许你定义和设置你在云环境中需要的所有资源作为代码，而不必点击特定云提供商的控制台。

## 先决条件

*   您想要扩展的 ECS 服务
*   SQS 队列

# 我们要做什么

我们将根据队列中的项目数量来扩展我们的服务。

*   如果队列中有 0 个项目，则任务数必须设置为 0。
*   如果队列项目数> 0 且≤ 500，则任务数必须设置为 1。
*   如果队列项目大于 500 且小于等于 1000，则最多可扩展到 2 个任务。
*   如果队列项目超过 1000 个，最多可扩展到 3 个任务。

# Terraform 脚本

从现在开始，我将讨论我们地形脚本的不同部分。您可以在文章末尾找到我完整的 Terraform 脚本，其中还包括任务定义、ECS 服务等资源。

## 自动缩放目标

您必须添加一个指向现有 ECS 服务的自动扩展目标。如前所述，这个服务也可以使用 Terraform 来设置，但是也可以使用 AWS 控制台手动创建。

在自动缩放目标中，您可以提供想要缩放的维的最小和最大容量。在我们的例子中，我们想要扩展`ecs:service:DesiredCount`,它指示在我们的服务中应该运行多少任务。如果正在运行的任务数量没有达到预期数量，ECS 将启动所需数量的任务。

## 自动缩放策略

设置自动缩放目标后，我们可以开始定义我们的缩放策略。

**向上扩展的策略** 在向上扩展我们服务的自动扩展策略中，我们定义了当一个特定的指标满足某些条件时，我们希望调整`DesiredCount`的`ExactCapacity`(我们指的是上面定义的自动扩展目标的可扩展维度)。

当队列中有 1 到 500 个项目时，我们希望期望的计数为 1；当队列中有 500 到 1000 个项目时，期望的计数为 2；当队列中有超过 1000 个项目时，期望的计数为 3。**请注意:**下限为‘大于’，上限为‘小于或等于’。

**缩减策略** 当队列中没有项目时，我们还希望将所需计数缩减为 0，因此我们还添加了一个自动缩减策略。

## CloudWatch 度量警报

我们现在已经定义了我们的策略，但是还没有这些策略的触发器。我们必须通过 CloudWatch 指标警报来触发策略。在我们的例子中，这些度量警报不断地查看队列中的项目数量，并在超过我们定义的阈值时发出警报。

我们可以在此指标警报触发时设置一个操作，它会将指标值传递给该操作。我们正在观察的度量是我们的 SQS 队列的`ApproximateNumberOfMessagesVisible`度量。这是 AWS 在您创建 SQS 队列时自动提供的度量。

**横向扩展** 我们创建了一个横向扩展指标警报，当队列的`ApproximateNumberOfMessagesVisible`为 1 或更大值时，该警报就会发出警报。警报操作是我们的向上扩展策略，它将根据价值决定要做什么。

**Scale In** 我们对 Scale In 做了同样的操作，我们希望当队列中的项目数为 0 时触发我们的 scale down 策略。

# 差不多就是这样！

这就是我根据 SQS 队列中的项目数量来扩展 ECS 服务所做的工作。我没有解释每一个设置，你可能需要调整脚本来满足你的需求。你也可以动态地创建`step_scaling_policy_configuration`，这样你就不必在自动缩放策略中提供一个完整的步长调整列表。

# 问题、建议或反馈

如果您对本文有任何问题、建议或反馈，请告诉我！

# 最后的话

我要感谢 Redditor [JohnPreston72](https://www.reddit.com/user/JohnPreston72/) ，他非常好心地提供了一些[云形成脚本](https://github.com/EWS-Network/s3tosftp)。基于 u/JohnPreston72 提供的脚本，我能够自己设置缩放并编写自己的 Terraform 脚本(参见下面的完整脚本)。