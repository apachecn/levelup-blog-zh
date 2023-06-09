# Git & GitHub 初学者教程

> 原文：<https://levelup.gitconnected.com/git-github-beginner-tutorial-b5885882a380>

刚开始编码的时候，总听人说 GitHub 有多棒，掌握 Git 技能有多重要。我不知道的是 Git 和 GitHub 是两回事。一方面， **GitHub** 是一个托管和存储我们编写的库(文件和代码)的网站，每个人都可以查看和协作这个项目。而另一方面， **Git** 是一个版本控制系统，用于在软件开发过程中跟踪源代码的变化。它是为协调 [p](https://en.wikipedia.org/wiki/Programmer) 程序之间的工作而设计的，但是它也可以用来跟踪任何一组 [f](https://en.wikipedia.org/wiki/Computer_file) 文件中的变化。它的目标包括速度、数据完整性和对分布式非线性工作流的支持。( [Git 维基百科](https://en.wikipedia.org/wiki/Git))。现在的软件开发公司非常重视 Git & GitHub，主要在软件开发周期中使用它们。今天，我们将深入 Git & GitHub，看看它们是什么以及如何使用它们。

让我们先来看看 [GitHub](https://github.com/) 。这是一个网站，可以查看和存储我们的文件，像大多数网站一样，我们需要创建一个用户来启动。创建用户后，我们可以通过单击右上角用户图标旁边的按钮来创建存储库。当我们创建一个新的存储库时，GitHub 会要求我们给这个存储库起一个名字，公开或者私有，用一个 Readme 初始化它。Readme 顾名思义，是对这个回购是什么的说明和解释。

![](img/55eea723598f07b76753ed6b3fd54338.png)

创建存储库后，我们将被带到存储库所在的页面，如果我们创建了带有 Readme 的存储库，那么 repo 页面将在页面上显示 README.md 文件。如下所示，如果我们单击“branch”选项卡，我们可以查看该回购有多少个分支机构。最初创建回购时，默认分支始终显示为主分支。顾名思义，branch 是帮助版本控制的最佳工具。比方说，如果其他人有兴趣参与这个回购，他们会在这个回购上克隆并创建另一个分支，这样这个人就不会自动干扰这个回购的主分支。很多时候，作为一名软件工程师，我们需要灵活并与其他程序员在一个项目上合作，这是当我们每个人单独工作在自己的分支上时，然后将文件合并到主分支中，以最小的冲突。

![](img/ed9272fa351d777d0600f4b89654547d.png)

如上面的存储库示例所示，我们可以看到这个回购上有三个分支。主分支是文件的当前版本所在的位置，也是我们创建这个存储库时的原始分支。这个回购有另外两个分支，Sam 的分支和 Brinda 的分支，这意味着目前有两个合作者在这个回购上，每个人都创建并使用自己的分支来构建功能，最终，Sam 和 Brinda 会将他们的工作合并到主分支中(拉请求)。

在我们更深入地研究 GitHub 以及如何将两个合作者的作品结合在一起之前，让我们先看看 Git 是什么。Git 基本上是一些终端命令，我们可以利用它们来帮助我们在本地计算机上工作，并将我们的文件推送到 GitHub，以建立版本控制系统的效果。Git 的安装会因我们所用的操作系统而有所不同，如下所示:

![](img/216d5ccb5a21fcf85fbc79f0649435fd.png)

[https://Git-SCM . com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

一旦 Git 安装在我们的计算机上，我们就可以运行终端命令，如:`git add, git commit, git push, git pull`等。在我们深入研究这些命令之前，让我们看一下创建回购的另一种方法。如前所述，我们在 GitHub 网站上创建了一个 repo，但还有一种方法可以用 Git 命令创建 GitHub repo。下图显示了几个不同的命令，我们可以使用它们在本地计算机上创建 GitHub repo，而无需通过 GitHub 网站。

![](img/f6b2467b005de61207bbb928c845f4b4.png)

我们仍然需要为要创建的这个 repo 创建一个 GitHub 用户名

命令`git init`实质上是在我们的本地计算机上启动一个 repo，`git add`是添加文件的命令，在我们上面的特定示例中是添加 README.md 文件。一旦文件被添加/暂存，`git commit`将是下一个命令。顾名思义，我们致力于添加这些文件，但是第一次，我们还需要向 GitHub repo 添加一个远程控制，这是下一个命令`git remote add origin`。注意，在命令后面有一个 GitHub 链接，它实际上是告诉 git 我们正在尝试访问哪个 GitHub repo。一旦创建了回购，就可以在 GitHub 网站上找到该链接。`git push`是我们输入和推送文件到 GitHub 的最后命令。由于我们刚刚创建了一个远程访问并添加了“origin”上游，我们可以使用`git push -u origin master`推送至该上游，并且我们直接推送至主分支。(ps:这些命令可以根据不同的用途进行修改，例如:`git add .`将根据我们所在的分支添加我们所做更改的所有文件，`git commit -m "this is our second commit to this repo"`该命令帮助我们提交并在 GitHub 上给出一条消息，以确定我们在哪里以及对我们的 repo 做了什么更改。`git push`一旦 git 知道什么是回购，我们在哪个分支，就可以简单地使用。)

有关更多信息，请查看该网站的 git 命令列表:

 [## 基本 Git 命令

### 下面是一些基本的 Git 命令列表，可以帮助您使用 Git。要了解更多细节，请查看 Atlassian Git…

confluence.atlassian.com](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html) 

我们可以简单地使用 git 命令在 repo 上创建并切换到不同的分支。(GitHub 上也有办法)`git checkout -b sam` 这个命令将帮助我们创建并切换到一个名为 sam 的新分支。一旦我们创建并切换到分支，我们总是可以使用`git branch`进行双重检查。这个命令将告诉我们这个回购上有多少个分支，以及我们当前在哪个分支上。

![](img/e2601ea7ebf8d5041dc91214c8fc1475.png)

我们总是可以使用命令`git checkout "branch name"`切换到另一个分支。在我们的例子中，我们可以使用 git 命令`git checkout gh-pages`，它将把我们带到“gh-pages”分支。一旦我们在自己的分支上，我们就可以通过使用一系列 git 命令`git add .` `git commit -a` `git push`来修改一些代码和分支。对 Sam 分支的更改不会影响分支“gh-pages”。

既然我们做了大量的修改，并使用 Git 命令将文件推送到 GitHub，我们可以返回 GitHub，看看 pull 请求是如何工作的。如前所述，当我们与其他程序员一起工作时，我们希望创建自己的分支，并将我们的工作保存到该分支，然后当需要汇集每个人已经完成的所有工作时，为了确保每个程序员构建的不同功能之间的冲突最小或没有冲突，我们使用 GitHub 上的 Pull 请求。pull request 本质上做的是，它会检查两个分支之间的代码差异，主要用来检查我们个人分支和主分支之间的差异，确保 pull 请求之前没有冲突。一旦拉请求继续，我们可以将我们的分支合并到主分支中，所有的工作都将保存到主分支中。其他程序员可以使用 git 命令，比如`git pull origin master`来删除我们在整个项目开发过程中所做的所有更改和构建的特性。如果我们的分支和主分支之间有冲突，最好的做法是与另一个同行程序员协商和评审，以确保我们保留了所有的更改和我们构建的特性，并且这些特性是功能性的，并且与其他人一起很好地工作。

还有很多其他 git 命令和 GitHub 特性，我们在本文中还没有探讨。但这是一个初学者教程，让我们开始使用 Git 和 GitHub，随着时间的推移，我们将通过使用 Git 和 GitHub 的经验了解更多。请随意检查并为我的开源项目[诗歌世界](https://haihuanchen.github.io/poems-website/)做贡献，该网站是通过 GitHub 托管的！

感谢您的宝贵时间！要了解更多信息，请查看我在下面提供的关于 Git & GitHub 的详细信息和指南的链接。

[](https://github.com/haihuanchen/poems-website) [## 海焕晨/诗歌-网站

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/haihuanchen/poems-website) [](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners) [## 针对初学者的 Git 和 GitHub 介绍(教程)

### 今年 8 月，我们在 HubSpot 举办了一个女性程序员会议，并为初学者举办了一个关于使用 git 和 GitHub 的研讨会。我…

product.hubspot.com](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners) [](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) [## Git -安装 Git

### 在开始使用 Git 之前，您必须让它在您的计算机上可用。即使已经安装了，也是…

git-scm.com](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 

编码列车 YouTuber 有一系列关于 Git 和 GitHub 的有用视频

 [## GitHub.com 帮助文档

### 面向软件开发人员、设计人员和项目经理的文档、指南和帮助主题。使用 Git 覆盖，拉…

docs.github.com](https://docs.github.com/en/github)