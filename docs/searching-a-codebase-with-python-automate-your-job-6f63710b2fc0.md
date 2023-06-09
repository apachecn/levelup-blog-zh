# 使用 Python 搜索代码库—自动化您的工作

> 原文：<https://levelup.gitconnected.com/searching-a-codebase-with-python-automate-your-job-6f63710b2fc0>

![](img/fff0ecb628162502bb85a6a898151587.png)

[亚历山大·奈特](https://unsplash.com/@agkdesign?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

就在上周，我被分配了一项任务，在工作中检查我们的一个代码库，找出不受支持的代码。我们正处于向云迁移的过程中，需要识别与云不兼容的代码。通常这意味着在试图更新之前，要花数小时筛选代码来找到关键词并记下来。

但不是今天！借助 Python 的强大功能，我将向您展示如何搜索整个目录来查找文件中的关键字。一旦我们发现含有恶意代码的文件，我们将创建一个列表，以便我们可以找到最具攻击性的文件，并重点关注这些文件。

# 迭代文件树

首先，我们将收集我们感兴趣的文件的路径。这里我们在顶部定义了要搜索的目录。此外，我们还创建了一个排除列表。排除列表确保我们不会获得与我们的平台无关的文件。node_modules 文件夹是我们不想包含的一个主要例子。

我们在循环之外初始化文件路径，因为我们稍后将迭代它。

将帮助我们完成迭代每个目录的艰苦工作。它返回根目录名(当我们迭代时，我们得到一个更新的根目录)。此外，它会给我们一个子目录名称和文件名的列表。

我们忽略子目录名称，因为我们只需要文件的路径。收集它们意味着遍历目录中的文件名列表，检查以确保它具有适当的扩展名，并确保它不存在于我们的排除列表中。

# 对文件进行分类

接下来，我们将检查我们找到的所有文件，看看它们是否有任何攻击性代码。我们创建了一个数组，其中包含了我们想要搜索的所有方法。这些事件需要在以后更新。

我们将访问上一步中找到的每个文件。当我们访问它们时，我们将打开并统计任何攻击性代码的出现次数。如果我们找到一个事件，我们将把路径、不支持的代码和它出现的次数添加到事件数组中。

# 结果

使用这种脚本让我不必打开 150 多个代码文件。相反，它发现了 26 个带有攻击性代码的文件，所以我可以专注于这些文件。此外，我能够在几分钟内让我的经理对项目的范围有一个更好的了解，而不是几天。

对于那些查看代码并指出使用 map、filter 和 reduce 可以用更少的步骤来完成的人来说，您是对的！然而，并不是每种情况都需要完美的代码。这是一个很好的例子，说明相对较少的 Python 经验，任何人都可以节省工作时间。