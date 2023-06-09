# 微服务架构的原则

> 原文：<https://levelup.gitconnected.com/principles-of-the-microservice-architecture-785a7f88c993>

## 如何用微服务设计一个应用？

# 介绍

微服务架构是一种设计范式，其中大型复杂应用程序被分解为一套小功能组件服务，这些服务具有以下特征:

*   松散耦合
*   高度可维护和可测试
*   独立开发、部署和维护
*   围绕业务能力组织
*   由一个小团队拥有

![](img/75018320d659ecfebf1ddb842db7d2d3.png)

上图(承蒙:Edureka。co)展示了整体式、面向服务和微服务架构之间的主要区别。整体架构由封装应用程序的单个大型组件组成。面向服务的架构(也称为 SOA)将服务分成粗粒度的模块，而微服务架构将它们分成非常小的粒度。

# 微服务架构的原则

本节将深入探讨微服务架构良好运行所需的七个核心原则。

# 领域驱动设计

一个典型的应用程序通常面向一组业务领域。领域是问题空间中的一个独立区域，它有丰富的上下文，强调用一种共同的语言来讨论问题。

![](img/31d0cd1397b7150519dfdd9056454be4.png)

让我们以一个典型的信用卡处理应用程序为例。在这样的应用程序中，支付处理工作流主要有三个不同的领域。这些措施如下:

*   商户子域:处理财务参数和商户受理工作流。
*   会计子域:处理日终交易处理、清算和对账。
*   支付子域:处理在线交易处理。

给定上述子域，应用程序可以分解成多个微服务，从而可以建立关注点的分离。

因此，微服务是围绕封装的业务功能组织和构建的。业务能力代表业务单位在特定领域中的功能。合并域驱动的设计允许架构将系统能力隔离到不同的域中。

# 自动化文化

在一个高度分解的生态系统中，将一个单一的应用程序分割成一套组件服务，自然有助于独立部署单元。采用微服务架构的组织应该采用导致微服务自动化的实践。一些可以自动化的功能包括构建、测试、部署、警报等。，跨微服务。

# 基础设施自动化

[基础设施即代码(IaC)](https://www.nexastack.com/en/blog/infrastructure-as-code) 通过描述性模型配置和管理基础设施。就像对待应用程序源代码一样对待您的基础架构配置和供应。在过去的十年里，IAAC 取得了显著的进步(基础设施作为一个代码)。Terraform、Ansible、AWS CloudFormation、Azure Resource Manager、Google Cloud Deployment Manager 等工具。，提供基础设施(服务器、负载平衡器、缓存、数据库等)。)天衣无缝。

# 测试自动化

考虑到分散的模型，微服务架构需要严格的测试，以确保系统在发布时是稳定的。这需要许多不同工具的投资，以确保微服务在发布前经过充分测试。这些工具包括 Apache JMeter、Gatling、Jaeger、Cypress 等。这些工具帮助团队编写可伸缩性、端到端测试，并在测试运行时监控和观察系统行为。

# 连续交货

连续交付是一种软件工程方法，其中团队在短周期内生产软件，确保软件可以在任何时候可靠地发布，并且在删除软件时，无需手动完成。它旨在以令人难以置信的速度和频率构建、测试和发布软件。为了实现无缝和低开销的应用交付，有必要通过连续交付模型部署每个微服务。在这种模式下，团队需要投资测试自动化和交付平台，如 [Harness](https://staging-devharnessio.kinsta.cloud/) 、 [Spinnaker](https://spinnaker.io/) 、 [Jenkins](https://www.jenkins.io/) 、 [Gitlab](https://about.gitlab.com/) 等。

![](img/e082e52deccbca1bd557d2592b644144.png)

# 封装:隐藏实现细节

封装的原则表明，服务只能通过标准化的 API 使用，并且不应该公开其内部实现细节(业务逻辑、授权实现、持久性逻辑等)。)给它的消费者。让我们考虑采用以下两种策略的系统设计:

# 设计 1

多个服务访问的单个共享数据库。

# 设计 2

每个服务拥有自己的数据库模式，并通过 API 公开交互。

在 design 1 中，对数据库模式的更改，比如删除列、更改列的数据类型和添加新列，很可能需要对许多不同的服务进行上游更改。这可能会导致未知的连锁反应，引入错误并需要大量维护。因此，采用设计 2 更有意义。

# 如何进行封装设计

我们将讨论两个重要的概念，即 API 和有界上下文，以更好地理解封装和关注点分离的思想。

# 应用编程接口

应用程序编程接口，或通常称为 API，是在组件之间定义的接口，用于基于特定动作交换信息。通常，API 被设计成遵循 CRUD(创建、读取、更新和删除)模型。API 只公开有限的一组信息，并且在标准契约中隐藏了底层数据模型、持久层、网络架构等的复杂性。

# 有界上下文

有界上下文是一类共享概念理解的组件。它们是领域驱动设计(DDD)的核心模式。DDD 通过将大型模型划分为不同的有界环境并明确它们的相互关系来处理它们。

![](img/309f6bada2a4db762ebfe88643d42e5e.png)

我们参考上图。有两种不同的有界上下文。这是销售环境和支持环境。销售上下文专门处理机会、渠道、区域和销售人员等概念。客户和产品等概念在销售和支持上下文之间共享。类似地，支持上下文以共享的方式理解标签、缺陷、产品版本和客户、产品等概念。

# 为什么考虑有界上下文很重要

重要的是要理解，相同的概念，如客户，根据其上下文可能有不同的含义。我们举个例子。在销售上下文中，客户可能指的是我向其销售产品的客户，而在支持上下文中，它可能指的是提出支持请求的客户。在设计 API 时，必须考虑哪些信息应该共享，哪些信息应该隐藏。逐步共享机密信息比隐藏已经共享的信息更容易。如果支持上下文只需要关于客户过去提出的票据的信息，那么共享完整的客户对象可能不是一个好主意。

# 分散

让我们首先理解为什么在微服务架构中需要去中心化。为了构建高度可伸缩和弹性的系统，单个组件所有者需要*自主权。自主就是给人们尽可能多的自由去做手头的工作。构建分散体系结构时要遵循的一些通用原则如下:*

# 自助服务

自助服务的理念包括为团队提供调配资源(如虚拟机、服务实例、存储单元等)的能力。).传统上，获得任何资源供应的周期需要团队筹集票据；该票证可能需要经过 IT 部门的批准。这将大大减慢整个过程，并使软件开发过程变得缓慢。随着 DevOps 模型的出现，以及 AWS、GCP、Azure 等超大规模云平台的出现。，团队自助服务和管理变得更加容易。

# 共享治理

集中式治理面临着用同一把锤子解决所有问题的问题。他们致力于在单一技术平台上实现标准化的理念，尽管从来没有一种适合所有工作的方法。将一个整体分割成几个松散耦合的微服务，允许在构建每个微服务时有意识地定制技术堆栈选择，通常是按照最适合手头工作的方式。

[Gilt 团队的这篇文章](https://gilt-tech.tumblr.com/post/102628539834/making-architecture-work-in-microservice-organizations)谈到了共享治理架构，他们解散了一个“中央架构团队”在这种模式下，每个微服务团队都有自己的“架构师”它们组成了一个“架构板”他们的一般目的是确保最佳实践的共享，并确定我们需要治理的极少数标准——主要是在技术跨越团队边界的地方(例如，一个团队构建的软件如何与另一个团队构建的软件对话)。

# 智能端点和哑管道

微服务架构假定业务逻辑应该封装在微服务中。通信媒介(比如消息总线)应该是无声的。这与 SOA 的企业服务总线(ESB)模型非常不同，后者包括消息路由、数据转换规则、对业务上下文的理解等复杂特性。，在消息总线中。使管道变得智能的主要缺点是，业务逻辑的变化将需要微服务、消息总线和其他微服务的下游变化。这可能导致系统中的重大错误，并增加增量更改和维护的成本。

# 参考

1.  [最大化微服务架构第 1 部分:什么和为什么](https://kwahome.medium.com/maximizing-microservices-architecture-part-1-introduction-37e2753f53e9)
2.  [最大化微服务架构第 2 部分:原则](https://kwahome.medium.com/maximizing-microservices-architecture-part-2-principles-5b8004b0ed09)
3.  Sam Newman 的[微服务原理](https://www.youtube.com/watch?v=PFQnNFe27kU)
4.  [服务架构的领域驱动设计](https://www.thoughtworks.com/insights/blog/domain-driven-design-services-architecture)
5.  [作为提高生产力的代码工具的 10 大基础设施](https://www.nexastack.com/en/blog/best-iac-tools)
6.  [马丁·福勒的有界语境](https://martinfowler.com/bliki/BoundedContext.html)