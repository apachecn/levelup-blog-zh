# 使用 Yarn 更新 npm 依赖关系的分步指南

> 原文：<https://levelup.gitconnected.com/step-by-step-guide-to-updating-your-npm-dependencies-with-yarn-115dc7f5e4b7>

![](img/1bc13025c8d092dc0c70a574ed4c326e.png)

菲利普·埃斯特拉达在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

对于您维护的任何活动代码库，保持您的依赖关系最新是至关重要的。通过保持最新，您可以访问您使用的每个第三方软件包中的所有最新功能和错误修复。提前更新到一个主要版本(如从 v2 到 v3)也比提前更新到几个版本(如从 v2 到 v7)容易得多。掌握依赖项更新有助于避免同时处理几个重大变更的混乱局面。

我倾向于每两周更新一次我所拥有的项目中的依赖项，也就是每个 sprint 更新一次。这看起来像是花了很多时间来更新依赖项，但事实是，如果你勤于掌控一切，这根本不需要很长时间。15-30 分钟是你需要的全部时间。

下面是我使用的过程。这对你来说应该也不错。

# 第一步

在您的终端中运行`yarn upgrade-interactive --latest`。这将打开一个交互式 CLI，允许您挑选此时要更新的软件包。选择所有次要版本和补丁版本更新，然后按回车键。

# 第二步

再次在您的终端中运行`yarn upgrade-interactive --latest`。这一次，选择你想要解决的任何主要版本更新。根据定义，主要版本意味着重大的变化，比如删除了代码可能正在使用的特性或 API。这意味着您应该访问该包的 GitHub repo，查看 changelog 或发行说明，然后根据需要更新您的代码。有时你可能很幸运，发现这个突破性的改变并不适用于你正在使用的任何功能，所以不需要额外的工作。

# 第三步

在您的终端中运行`yarn outdated`，查看所有剩余的过期依赖项。为什么？因为有时`yarn upgrade-interactive`不能正确处理更新，你必须自己手动更新。

例如，`yarn upgrade-interactive`无法升级不在 [Lerna monorepo](https://github.com/lerna/lerna/issues/2477) 内的根级`package.json`文件中的依赖项。

如果您使用`package.json`文件中的`resolutions`字段来使用任何给定包的特定版本，这个命令也不能正常工作。[命令会无声的失败](https://github.com/yarnpkg/yarn/issues/5413)并且不会更新包版本或者解析版本。

因此，相反，您必须手动更改在`package.json`文件中为您想要更新的任何剩余依赖项指定的版本，然后运行`yarn install`来安装这些新版本。

# 第四步

既然您已经更新了您想要的所有依赖项，那么是时候验证您的代码库中的所有内容是否仍然正常工作了。如果您的 repo 中没有格式化程序、linters 或测试，祝您好运！您将依靠对您的应用程序进行手动抽查来检查回归情况。

如果您已经安装了有用的工具，现在是运行格式化程序、linters 和测试的时候了。我用[更漂亮的](https://prettier.io/)进行格式化，用 [ESLint](https://eslint.org/) 进行林挺，用 [Jest](https://jestjs.io/) 进行单元测试。如果发现任何错误，请继续解决这些问题。

注意:虽然我把这个检查留在了步骤 4 中，但是您可能会发现在步骤 1 和 2 之后运行这些检查也很有用。这取决于你。

# 第五步

添加、提交和推送您的代码。审查并合并您的合并请求，然后您就可以开始了！

# 结论

就是这样！我已经遵循这个过程很多年了，结果令人惊讶。不再陷入阻碍开发工作的旧版本的依赖关系中。只要花一点时间维护你的回购协议，你就可以把剩下的时间花在开发令人惊叹的新功能上。