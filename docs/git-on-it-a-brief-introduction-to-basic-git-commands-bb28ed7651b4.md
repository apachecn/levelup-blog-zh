# 赶紧的。基本 Git 命令简介

> 原文：<https://levelup.gitconnected.com/git-on-it-a-brief-introduction-to-basic-git-commands-bb28ed7651b4>

![](img/4ca52305b904b3907fea532ce8d91e91.png)

你是编码新手，对项目的版本控制感兴趣吗？您希望能够与其他编码人员共享您的项目吗？在这第二篇关于 git 初学者的文章中，我将介绍一些在项目中使用 git 可能需要的基本命令。

关于如何建立一个远程 git 存储库并将其与本地计算机上的一个项目相连接的说明，请参见我以前的一篇关于建立您的第一个 git 存储库的文章:[您的第一个 Git 存储库的简要指南。](/a-brief-introduction-to-your-first-git-repository-afc3f72d902a?source=friends_link&sk=46f1ab278cd290c69156db4fc12059a7)

您还需要熟悉使用[命令行](https://medium.com/@lynn8542/commanding-the-command-line-dd005e888cc2?source=friends_link&sk=d590bdfffe5269321c3a422d291673dd)的基础知识。

# 让我们开始吧！

您刚刚创建了一个非常引以为豪的项目，您渴望将它发布到一个很多人都可以看到的 git 存储库中——但是您还不是 git 专家，您的项目还没有做好 git 准备。没关系。在项目的根目录(整个项目的“home”文件夹，通常是文件结构中的顶层文件夹)中，只需在命令行中键入`git init`。

## 常见的 git 命令:

所有这些命令都应该输入到命令行中。

然后，`git init`将用一个`.git`目录为您的项目初始化文件夹，该目录包含所有必要的 git 函数的元数据。这个命令在您的计算机上创建一个本地 git 存储库。

`rm -rf .git`将从你的项目中删除 git 文件夹和 git 使用的所有元数据，因为迟早你会 git 初始化一些你不想要的东西。有一次 git 初始化了我的整个桌面(还好没有推上去)，修复起来是个庞然大物。不过这是一次很好的学习经历——我现在非常警惕我要初始化什么，以及我想要初始化的东西在哪里。

`-r`的意思是“递归”，这意味着文件夹中的所有文件都将被删除。`-f`的意思是“强迫”,它会强迫 git 不先问你是否真的想做就去做。

`git status`将告诉您项目的状态；例如，如果您有已被修改的代码或已被提交但未被推送的内容。

`git add`告诉 git 开始跟踪文件或目录中发生的事情。

`git add <name_of_folder>`将添加一个特定的文件夹进行跟踪。

`git add <name_of_file.extension>`将跟踪一个特定的文件。

`git add -A`将添加您当前目录中的所有文件和文件夹。

`git add .`还会添加你当前工作目录中的所有东西。

`git commit -m "Message"`允许您提交自上次提交以来目录中添加的所有更改。`git commit`将修订添加到您计算机上的本地 git 存储库中。`-m`意味着描述变更的提交消息将被添加到日志中，并且该提交消息在`-m`之后的引号之间。

`git reset`将重置——即撤销——任何未被*推送到远程源的提交。*当工作被推送到远程源时，看起来好像从来没有进行过重置提交。

`git revert`将创建一个新的提交，撤销之前的提交。它让你回到上一次提交之前，而不破坏任何代码或版本。

`git push`是将本地 git 存储库中提交的变更发送到远程存储库的命令。“Origin”表示原始的远程存储库,“head”表示您当前正在处理的提交。因此，`git push origin head`会将变更发送到远程存储库的当前工作分支的负责人。

`git pull`将把远程存储库中的变更下载到您的本地 git 存储库中。`git pull origin head`将把远程原始存储库中当前工作分支的代码下载到本地存储库中。

`git fetch`将在您当前工作的分支中检查远程原始存储库的代码，以查看自您上次下载代码以来是否有任何更改。`git fetch`实际上不会删除任何代码——你需要用`git pull`来完成。不过，在删除代码之前了解变更是有好处的，因为这些变更可能会与您正在处理的代码发生冲突。在下载新代码之前，你可能需要`git stash`。

暂时将你当前正在处理的代码放在一边，允许你从最后一次拉取中获得干净的代码。如果您的分支中的代码在您最后一次拉下它之后已经被更改，您现在可以拉下那些更改，而不会中断或丢失您对该代码所做的更改。然后，您可以使用`git stash apply`或`git stash pop`从 stash 中取回您对代码所做的更改。

`git clone`将从远程原始存储库克隆整个现有存储库到您的本地计算机上。为了克隆存储库，您需要有一个存储库的地址，您可以使用 SSH 密钥或安全的 URL 来访问该地址。例如，要从我在 GitHub 上的远程存储库中克隆出`my_repository`,我需要结合一个 SSH 密钥或者从一个安全的 https URL 运行`git clone git@github.com:LynnAmsbury/my_repository`。

`git remote add origin <name> <URL>`将允许您在指定的 URL 上用自己选择的名称建立一个远程 git 存储库。

`git remote`将让您看到给定原始存储库的所有其他远程存储库的名称。当几个开发人员远程处理同一个项目时，这可能会很方便。

`git branch <new_branch_name>`将在本地存储库中为您创建一个新的分支。这很重要，因为主分支应该只包含正常工作的可用代码。如果你在主分支中从事项目的某个方面，事情变得一塌糊涂，那么对项目中的每个人来说都是如此，不仅仅是你。

会将你从当前的分公司调到另一个现有的分公司。

`git checkout -b <branch_name>`会创建一个新的分支，同时将你移入其中。

`git checkout .`将清除一个分支中的所有改变，回到最后一次提交。

`git checkout <folder_name or file_name.extension>`将清除一个分支中单个文件夹或文件中的更改，恢复到上次提交。

这并不是现有的每一个 git 命令的详尽列表，但它是我最常用的命令的简明列表。希望对你的编码之旅有所帮助！