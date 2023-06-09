# 如何利用 Xcode 的构建配置

> 原文：<https://levelup.gitconnected.com/how-to-leverage-xcodes-build-configurations-5516ac3743e4>

## 为不同的构件类型更改 iOS 应用程序图标

![](img/b4854a53c1fe981287a366dd60658a01.png)

在本教程中，我们将学习如何构建 iOS 应用的三个版本——调试、alpha 和发布。我们还将为每个应用程序使用不同的图标，以便更容易区分它们。

这是您在本文结束时将学到的内容:

*   如何在 Xcode 中创建构建配置？
*   如何在构建配置中引用三组应用程序图标。
*   如何在您的设备上安装同一应用程序的多个版本类型。

事不宜迟，我们开始吧。

# 我们开始吧

我们从一个名为“App”的空项目开始:

![](img/17f0d9c5ac817206e926848b08215b0d.png)

我们的第一步是点击“项目”标题下的“应用程序”:

![](img/fe5a3fcd7023a8b4bb036078fbba8d9e.png)

这里我们看到 Xcode 已经为我们提供了“调试”和“发布”配置。我们的任务是创建一个“阿尔法”配置:

![](img/2c2b18e9210e3e704483f58859685dac.png)![](img/b0617aad6ee55a9761d386141021c20c.png)

正如我们所看到的，我们创建了一个“发布”配置的副本，并将其命名为“Alpha”。接下来，我们需要在`Assets.xcassets`目录中添加应用程序图标集。

首先，让我们为应用程序图标创建一个新文件夹:

![](img/892f4ebb9dce26859e53956c3c0c2c2f.png)![](img/4ab04de6044d273f0b9f8e9341bfc5b7.png)

让我们将现有的“AppIcon”映像集移动到文件夹中(我们稍后将在“发布”构建配置中使用它):

![](img/31ace7cc2e4f4182c29286fcd0a01a59.png)

我们需要再创建两个图标，一个用于“调试”，一个用于“阿尔法”:

![](img/0c17322e5ba4043a91ae6d442e72bef0.png)

创建图标后，将它们命名为“AppIcon.dev”和“AppIcon.alpha ”,并将它们移动到“AppIcons”文件夹中，我们得到以下内容:

![](img/30bc42a0251b517b78d97b47de02cb91.png)

接下来，我们将具有相应分辨率的实际图像添加到每组图像中:

![](img/b151c1b12fac30ded050c8f24afebbcd.png)![](img/18452ec28d72d9cb2c85061526ca85ff.png)![](img/350eb1a6bb5420ac0efc4e56a14cdaf2.png)

是时候学习如何为每个构建配置引用所需的图标集了。

# 引用应用程序图标

首先，我们需要点击“目标”下的“应用程序”,然后选择“构建设置”,如下所示:

![](img/f928858645d376d49dab00a7d8c35a9b.png)

接下来，我们在搜索字段中键入“应用程序图标”,并展开找到的“资产目录应用程序图标集名称”类别:

![](img/65ad3b3f815cbd7261315a664c99fb03.png)

在这里，我们需要引用每个构建配置所需的图标集。让我们将名称调整如下:

![](img/67b013b07e23bc94853e0b8fc2cd2f09.png)

现在，如果我们构建、运行并最小化应用程序，我们将看到它使用“调试”构建配置:

![](img/0d475d0042fd54b0e47feced3a608cc0.png)

现在的问题是:我们如何运行不同的构建配置？答案是调整*方案*，这样我们每次运行应用程序时，它都会使用*不同的*构建配置。

# 运行不同的生成类型

要调整方案，我们需要点击这个按钮:

![](img/a7a685483eed79ba3a6fe171188ece42.png)

接下来，选择“编辑方案”,将出现以下弹出窗口:

![](img/16cd038417392a380456e5a5afd068a4.png)

如果我们展开“构建配置”类别，我们将看到所有三个可用的构建配置:

![](img/2bda3c447ed1326e3be35a1e82cb113f.png)

让我们选择“发布”，关闭弹出窗口并再次运行应用程序。当我们最小化应用程序时，我们会看到它正确地使用了“释放”图标集:

![](img/1163a889a204ed80c3eb578953d9c7d0.png)

太好了！然而，我们希望在同一台设备上安装三个版本的应用程序。让我们接下来处理这最后一项任务。

# 安装几种生成类型

实现这一点的方法是为每个构建配置使用不同的包标识符。就像我们对应用程序图标所做的一样，让我们在目标的构建设置中搜索“包标识符”:

![](img/c7920ef1a4180534e321de028164d461.png)

我们看到应用程序目前对每个构建类型使用相同的包 id。这就是为什么如果我们简单地改变构建类型并重新运行应用程序，它将更新现有的应用程序，而不是创建一个新的。让我们像这样更新包标识符:

![](img/143e044adc34a8b40be6257f55af926d.png)

现在，让我们尝试运行该应用程序的发布版本。将构建配置更改为“Alpha”:

![](img/511fa30686db638511993067d6858dbc.png)

在构建、运行和最小化应用程序之后，我们看到我们实现了我们想要的:

![](img/dac7497e2774b0471879609c2325801b.png)

# 资源

该示例项目可在 [GitHub](https://github.com/zafarivaev/build-configurations) 上获得。

# 包扎

希望这篇教程对你有用，感谢阅读！