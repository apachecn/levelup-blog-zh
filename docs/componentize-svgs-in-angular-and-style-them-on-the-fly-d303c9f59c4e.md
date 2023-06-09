# 在 Angular 中将 SVG 组件化，并动态地设计它们的样式

> 原文：<https://levelup.gitconnected.com/componentize-svgs-in-angular-and-style-them-on-the-fly-d303c9f59c4e>

![](img/d4a445fc42be93ca2ca610fd51f48afc.png)

图片鸣谢:字体超赞

你可能知道，如果你使用简单的艺术作品，如图标，SVGs 或可缩放矢量图形是必不可少的。但是你知道你可以把它们做成有角度的组件吗？事实上，我使用最多的两个库是我为 SVG 和 buttons 创建的。

# 为什么应该使用 SVG？

我开始使用 SVG 是因为它们能够在不损失分辨率的情况下进行缩放，并且我可以通过 CSS 对它们进行着色。(这对于我开始的游戏化[互动课程](https://yokoishioka.com/what-is-a-website/)的一部分很有用，你可以选择一个角色，让它变大或变小。)

**注意:**只有用路径和轮廓制作的 SVG 才能无限缩放。用图像制作的 SVG 会变得模糊。

SVG 也是超级轻量级的，因为它们是用 XML 表示的，您可以避免 http 请求来获取它们！

# 将自己从 SVG 库中解放出来

我没有意识到的是，我心爱的[字体令人敬畏的库](http://fontawesome.com/icons?d=gallery)花费了我将近 20 个 Lighthouse 点，并且我不需要它们的大型 Javascript 文件通过将它们转换成有角度的组件来使它们成为整齐的组件(而不是难以管理的文本块)。

**注:**我仍然订阅字体牛逼，因为他们无与伦比的选择。事实上，我制作的网站/应用程序上的所有图标都要感谢他们出色的插画师。

如果您最终使用他们的 SVG 或使用 Illustrator 制作自己的 SVG，请确保删除属于 SVG 的任何样式/注释，以便您可以正确地覆盖它们。

# 有角度的组件不必使用 HTML 模板

如果您想要自己的 Angular SVG 库，可以通过将组件的 templateUrl 参数链接到资源库中的 SVG，轻松地将它们转换为组件。(Font Awesome 提供了一个库来访问他们的 SVG，但是你可以通过这条途径来避免不必要的依赖和应用程序的重量。作为一个额外的好处，这种方法允许你一次声明你的 SVG，而不是必须在每个使用它们的应用程序中单独声明它们。)

**SVG-宇航员.组件. ts**

**注意:**最初，我将资源直接存储在我的 Angular 库中，但随后将 SVG 移动到我的应用程序的[共享资源文件夹](https://cloudengineering.studio/articles/trick-angular-into-thinking-all-apps-share-the-same-source-folder)，这样我就不必修改我的 angular.json 文件来使用资源，这样我就可以在库外访问 SVG。

这个决定的缺点是，除非您包含 assets 文件夹，否则库将无法在工作区之外工作。如果你有更好的解决方法，请告诉我。

# 小心你如何链接到你的 SVG

您不能使用常见的“src/assets”或“/assets”快捷方式来链接 SVG，因为它们需要到应用程序源文件夹的直接相对路径。这就是为什么我不得不使用一个长得离谱的相对路径。(同样，我确信有更好的方法来实现这一点。)

# 对所有的 SVG 使用相同的 CSS 文件

我还将 SVG 链接到同一个 CSS 文件，因为它们都需要相同的样式，这需要能够通过使用它们的父对象动态地对它们进行样式化。通过这样做，我只需要更新一个文件，以便在将来影响所有的组件。

**svg.component.css**

**注意:**不要忘记在你的模块的导出部分包含组件，以便你的应用程序可以访问它们。并将 SVG 库导入到使用它们的应用程序中。

# 清理未使用的文件

您可以删除组件附带的 HTML 和 CSS 文件，因为您的组件不会使用它们。

# 使用您的新组件

现在，如果我想使用 SVG，我只需使用组件的选择器:

```
<ces-svg-astronaut></ces-svg-astronaut>
```

因为我遵循相同的命名约定，例如 prefix-svg-description，所以我通常不必查找我是如何命名它的。

# 如果您想动态选择 SVG，该怎么办？

对于一些用例，您无法提前知道想要选择哪个 SVG。因为您不能使选择器的一部分成为动态的，所以这个特性需要设置一个单独的通用组件。

**svg .组件. ts**

注意:这就是为什么我在上面的 CSS 中包含了“img”的样式。要更改 SVG 图像的颜色，您需要在元素上使用这些样式:

```
mask: url('/assets/svgs/astronaut');
background-color: orangered;
```

# 自动添加“alt”标签和动态添加“title”标签

我包含了“alt”属性来自动获取带有单词“icon”的图标类型，这样我就不必单独指定它们了。然而，我将“title”属性设为变量，以防我想要添加悬停时显示的帮助文本，这将根据使用情况而变化。

# 使用通用 SVG 组件

现在，您可以使用同一个选择器，并通过传入图标类型来指定您想要使用的图标。您只需要设置这个组件一次，即使您添加/删除 SVG 到您的库中。

```
<ces-svg type="astronaut">
```