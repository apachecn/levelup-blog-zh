# 如何构建你的围棋应用程序，也就是在围棋项目中保持理智

> 原文：<https://levelup.gitconnected.com/structuring-your-go-applications-aka-staying-sane-with-go-projects-7d5bb38ff6af>

![](img/c4edcac0537da8db96eeea870bad19d5.png)

演职员表:【https://unsplash.com/photos/TPixIUNcQ7I 

## 因为我们都看到了“一步到位”的项目，没人敢靠近

正如所有的知识一样，在适当的时候肯定会有更好的方法，但在大约三年的职业和个人任务写作之后，这里是*对我起作用的*。当然*起作用*是主观的，所以我说*起作用*是指我进入一个 6 个月前的仓库，并且仍然设法找到我周围的路。我想这也算是“可维护”吧？😃

# 解决方案的来源

如果你在谷歌上搜索 Go 项目布局，你很可能已经看到了这个库:

[](https://github.com/golang-standards/project-layout) [## GitHub-golang-标准/项目-布局:标准 Go 项目布局

### 翻译:这是 Go 应用程序项目的基本布局。这不是核心 Go 定义的官方标准…

github.com](https://github.com/golang-standards/project-layout) 

这是一个很好的起点，因为了解这些标准有助于导航更受欢迎的 Go 代码库，如 [Kubernetes](https://github.com/kubernetes/kubernetes) 或 [Terraforms](https://github.com/hashicorp/terraform) ，但继续到`README.md`，您会发现:

> 是`not an official standard defined by the core Go dev team`；然而，它是 Go 生态系统中一组常见的历史和新兴项目布局模式

在我看来，这只是对已有内容的简单汇总。虽然它有助于传播对通用模式的认识(这最终会成为*惯用的*)，但是存储库并没有宣称它是*最好的/唯一的做事方式。*

*于是，我开始了寻找适合我的结构的旅程。接下来的文章将对此进行更深入的探讨。*

# *解决方案的前提*

*有许多考虑代码库的模型。取决于许多事情，如组织惯例、语言限制和业务领域，了解一些心智模型通常是有用的，以便能够看出什么可行，什么不可行。根据应用程序的目标类型，大多数都大致遵循与模型-视图-视图模型(MVVM)或模型-视图-控制器(MVC)模式相似的架构原则。*

*这些通用模型通常定义 3 层。一层访问实际数据(想想 DAOs)，另一层执行计算处理(控制器/视图模型/后端)，最后一层公开接口/视图(APIs 视图/前端)。*

*在这里，我意外地发现了一个与 Go 兼容的模型:*

*[](https://www.goodreads.com/en/book/show/51109185) [## 扶正软件

### 没有星级，因为它将被视为“方法”的评级，而不是书本身(这不是如何 GR 是…

www.goodreads.com](https://www.goodreads.com/en/book/show/51109185) 

ju val lwy 所著的《扶正软件》一书提出了一个模型，该模型的基础是[](https://www.informit.com/articles/article.aspx?p=2995357&seqNum=2)*(书中提出的一种模式)。非常适合需要跟上不断变化的需求的现代商业应用。该模型将组件分为五类:*

1.  ***实用程序** —水平有用的组件。日志和认证机制是潜在实用组件的一些例子。*潜在的*因为它取决于您的日志和认证组件的确切范围*
2.  ***资源访问器** —负责数据检索的组件。想想文件系统数据检索、从外部服务获取数据的 API 和 DAOs。*
3.  ***引擎** —负责将业务逻辑封装到不应该经常改变的基本处理单元中的组件。想象一下将一个`*.docx`文件解析成不同的部分(与将同一文件解析成表单中的字段相比[区别在于，与业务定义的表单相比，`.docx`格式不太可能改变])*
4.  ***管理者** —负责协调引擎组件以产生与交付价值更直接相关的结果的组件。在前面解析一个`*.docx`文件的例子中，管理器将是提取各种解析部分并把它们放入业务定义的表单中的组件。*
5.  ***客户端** —消费数据或在用户界面的情况下呈现数据的组件。通常是客户或其他系统使用数据的系统前端*

*就控制流而言，实用组件可以在任何地方使用。对于其余组件，只有当组件 A 比组件 B 高一级或与组件 B 同级时，才能从组件 A 调用组件 B。这意味着引擎组件应仅调用资源访问器，管理器组件应仅调用其他管理器或引擎组件。*

*我在这里发现的有用区别是 MVC 中的控制器概念进一步分裂为引擎和管理器类型的组件，前者处理不经常改变的更一般的计算，而后者处理通常与业务相关并且可以预期经常改变的数据的合成/协调(因此*易失性驱动的分解*)。*

*随着代码的增长和组织的成熟，这种差异也很容易使通用引擎类型的代码作为库被提取，而管理器类型的代码作为服务被提取。*

*与任何类型的抽象一样，会有一些漏洞，但总的来说，我发现这种模型非常适合 Go。*

# *Golang 标准项目布局中的有用部分*

*我已经尝试了这个存储库中几乎所有的目录结构，以寻找做事的“最佳方式”。不出所料，从来没有一个*最好的*，但是有一个结构我觉得对于我的环境来说已经足够好了*——CLI 工具、glue 服务和中等规模的类似 SaaS 的项目的开发。假设客户端/前端位于独立的存储库中，这是理所应当的。**

*这是我相对于项目根的结构:*

```
*/repo-root
  /bin
  /cmd
  /configs
  /deployments
  /docs
  /internal
  /pkg
  /tests
  Dockerfile
  Makefile
  main.go
  go.mod
  go.sum*
```

*`**/bin**`。这包含二进制文件，并且应该包含一个简单的`.gitignore`文件，用于除自身之外的所有内容*

*`**/cmd**`。它包含命令包装器——cobra/ur fave/others——并包含反映命令结构本身的子目录结构。例如，如果您能够运行`app get templates`，那么 Go 文件的相关目录结构应该是:*

```
*/repo-root
  /cmd
    /app
      /get
        /templates
          command.go
        command.go
      command.go
    command.go
  main.go*
```

*上面的结构应该可以让你在开发的时候运行`go run . get templates`。*

*`**/configs**`。这包含与应用程序构建过程相关的静态配置。我发现这仅适用于在引入`go:embed`和`go:generate`之前为 CLI 项目提供构建时配置。我相信可以通过切换到`go:embed`并使用本地嵌入来废除这个目录。*

*`**/deployments**`。其中包含与部署相关的文件，比如 Ansible playbooks、Docker Compose manifests、Kuberntes manifest/kutomizations 或 Helm charts。同样有争议的是，特别是对于 Helm，图表也可以在根级别`/charts`中，通过在根级别添加一个`Chart.yaml`来简化存储库到 Helm 存储库的发布。*

*`**/docs**`。我希望你记录你的代码。将您的文档放在这个目录中使您能够设置 GitHub/GitLab 页面从这个目录创建一个静态站点，而不是您的`README.md`或者更糟的是一个单独的文档分支。如果您将文档存储在单独的存储库中，则不需要(这对于使用 Gitbook 等外部工具很有用，这些工具提供了 WYSWYG 编辑器来管理您的文档，但也可以同步回 Git 存储库)*

*`**/internal**`。这包含了严格在代码库中内部使用的 Go 代码。请注意，有一个严格的标准，即此目录中的 Go 代码不能被另一个存储库中的 Go 代码引用，因此不要放置包含从另一个服务引用可能有用的`type`的代码(例如，当使用 gRPC 时，消费者通常使用来自提供者存储库的 Protobuf 定义——不要将您的 Protobuf 代码生成的文件放在这里，否则消费者将无法引用它们)*

*`**/pkg**`。它包含可以在内部使用的 Go 代码，但是其他存储库也应该能够作为依赖项引用这些代码。如果你在 gRPC 上使用 Protobufs，这是你可以放置你的`protoc`编码类型定义的地方。*

*`**/tests**`。这不包含测试。测试应该总是自包含在使用`*_test.go`符号的包中。相反，该目录包含测试可能需要集中引用的数据。这与最初的`/test`有所不同，主要是因为我喜欢运行`make test`来运行我的测试，根据您的偏好或组织惯例，可以随意坚持使用`/test`。*

## *文件上的其他注释*

1.  *`/scripts`目录不存在，因为我将脚本放入了`Makefile`中，并在 docker 文件中使用了`make`，这并不是常见的做法，因为从那时起，您将需要安装`make`。通过将构建映像与最终映像分开的多阶段 Docker 构建，在我看来这不是太大的问题，并且它通过只有一个中央脚本文件而简化了事情。*
2.  *也可以将`main.go`放在`/cmd`目录中，但是我发现在大多数情况下，作为一般的经验法则，将它放在根目录中会更好，因为对于缺乏约定知识的初学者来说，这样更直观，但是仅仅通过文件名就可以将它识别为入口点。另外，如果你正在开发一个库，`main.go`必须在根目录中，否则你的用户将不得不在他们的`import`语句中引用子目录。*

# *将心智模型付诸实施*

*冒着听起来太简单的风险，适合我的结构是:*

1.  ***实用程序和资源访问器组件进入** `**/pkg**` **。**当扩展到需要中央数据检索机制时，将它们提取到它们自己的存储库中。*
2.  ***发动机部件进入** `**/internal**` **。**当扩展到多个服务必须使用相同的引擎组件时，将这些组件提取到它们自己的存储库中。*
3.  ***非面向客户的管理器组件进入** `**/internal**` **。**这些组件应该相对特定于正在开发的服务。*
4.  ***面向客户的经理组件进入** `**/cmd**`。这些应该是也可以被视为视图的代码，或者是高度特定于您的服务的代码，除非通过 OpenAPI/AsyncAPI 或 SDK 之类的文档，否则不应该共享。*

*此外，我还遵循一些增强组件对变更的弹性的规则(新特性/变更请求应该导致尽可能少的变更):*

1.  ***在每一层实现依赖注入**。这意味着，如果 ResourceAccessor 组件需要 MySQL 连接，面向客户端的管理器组件必须启动连接实例，并通过所有组件向下传递，直到它到达 ResourceAccessor。这也有助于测试，因为它允许在每一级使用模拟来验证行为。*
2.  ***所有引擎组件都实现为** `**interface**` **s** 。这意味着所有引擎组件都将导出一个`interface`及其实现。这在*可处置性*(我认为这是任何组件最重要的属性)方面对**有很大的帮助，它使开发人员能够在不修改现有实现的情况下重写实现，然后能够通过用新的实现替换以前的实现来对其运行相同的测试。这也使 Go 中的性能基准测试变得容易。***

*通过执行上述操作:*

1.  *当业务增长时，添加是在现有代码的基础上单独完成的，只需对管理器组件进行最小的修改来添加引擎组件调用*
2.  *当业务需求改变时，修改很大程度上被封装到管理器组件中*
3.  *当上下文知识丢失时，任何组件类型的重写都可以很容易地完成，因为使用了`interface`类型*
4.  *升级核心依赖项时，更改大多封装到引擎和资源访问器组件中*

# *工具和流程*

*除了代码的结构之外，我发现工具在交流开发中常用的东西方面大有帮助，并且可以帮助理解代码库*

*就我个人而言，我使用我的`Makefile`来做这件事，但是如上所述，你也可以将脚本放在相对于项目根目录的`/scripts`目录中。对我来说，`Makefile`有一个好处，它是一个工具，可以在大多数机器上开箱即用，几乎在任何地方都一样。*

*使用一个`Makefile`还可以让其他开发人员(也就是 6 个多月后的你)能够在一个文件中了解所有的开发过程。*

*在我的一个项目中，一个典型的`Makefile`将会有如下内容，它可以让开发人员轻松地运行与存储库相关的任务(我知道，Make 并不打算成为一个任务运行器，但是嘿，它确实有效，并且现在已经成为 Go 项目中的一个惯例):*

```
*deps: # install dependencies
data: # runs go generate and/or other things like protoc
build: # builds the Go binary
image: # builds the Docker image
lint: # runs go vet or other similar tools
test: # runs tests
package: # packages the service/app
publish: # publishes the service/app*
```

# *结束了*

*希望这在某种程度上有所帮助——下次见！*

*如果你已经读到这里，请考虑给一些👏鼓励我继续创作这样的作品。去吧，祝你有美好的一天！**