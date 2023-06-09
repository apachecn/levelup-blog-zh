# 这是一个很酷的效果！—使用 HTML 和 CSS 构建卡片翻转效果

> 原文：<https://levelup.gitconnected.com/thats-a-flippin-cool-effect-ff6e5c3d24c0>

我们将制作一个卡片翻转效果。有助于吸引用户并增加一些交互性。一种在个人资料图片后面显示信息的创造性方式。

![](img/03df47d3688be95ac1f59a0b55c06d95.png)

照片由[弗瑞迪·卡斯楚](https://unsplash.com/@readysetfreddy?utm_source=medium&utm_medium=referral)拍摄

这张照片可能是你，背面的信息也可能是你的。我目前将这种效果用于我的投资组合的个人资料图片，但它也可以应用于其他事情，例如为产品或服务提供附加信息，翻转抽认卡应用程序，或您的创意思维能想到的任何东西。

![](img/2016061f5644747b6fd1d2164eeab540.png)

我将以海绵宝宝为例向你演示如何制作出你所看到的效果，但你也可以随意使用你自己的个人资料图片和信息！

我将使用 [*BEM 方法*](/the-bem-methodology-explained-4ca416f929cd?sk=0cd1adac1479f76b00e213faaea4310c) 来命名我所有的 HTML 元素，并使用 [*SCSS 来设计*](/sass-y-beauty-crafty-67616688b4da?sk=0efbadc799eb53adca407f8010fba757) 。如果你对这两个都不熟悉，可以看看我的博客！

**HTML 设置**

我们从一个简单的包含所有内容的 div 容器开始。这是基本元素。在容器中，我将为卡片本身创建一个 div。在卡片 div 中，我将为卡片的正面和背面制作两个 div。前面的 div 将有一个图像元素，后面将有一些段落和文本标题。在用一些数据填充这些元素之后，它应该看起来像这样:

![](img/4712e70ed3ce90bc9da859897b2899b8.png)

**SCSS**

我首先向容器添加一些样式。我将把容器的高度和宽度指定为 200px，并添加 perspective 属性给翻转一个 3D 效果。然后我将背景颜色设置为透明。

![](img/32479dd5a9e842409d5a1d2066888550.png)

然后，我将在容器内处理实际的卡。我将位置设置为相对位置，高度和宽度设置为 100%，这将是 200 像素，因为其父容器的 100%是 200 像素。我希望卡片中的所有文本都与中心对齐，通过将变换样式设置为保留 3D，并将所有变换过渡设置为 0.8 秒，这将指卡片翻转效果持续时间，确保所有子元素都保持其 3D 位置。

![](img/b5f3efee283a208c743d9699791654b1.png)

我现在将同时在卡片的正面和背面应用一些样式。我希望它们的高度和宽度继续继承卡片的大小，所以我会再次将它们都设置为 100%。这次我将把位置设置为绝对，因为我希望正面和背面相互重叠而不移动。下一步是让整件事成功的关键。我将使用背面可见性，并将其设置为隐藏。这使得元素的背面在面对用户时完全不可见。为了 safari 的兼容性，我还将添加 webkit 版本。

![](img/d2eedd74a8234a10ac5e0226d1e16209.png)

我现在将分别设计卡片的正面和背面。我首先设置背景颜色为海蓝色，因为海绵宝宝生活在海底。我将所有文本的颜色设置为黑色。然后，我调整正面的实际图像，使其高度为 200 像素，宽度可以自动调整，而不会扭曲图像。移动到背面，我应用相同的背景颜色，但这一次，设置文字颜色为白色。我确保通过在 Y 轴上旋转 180 度来变换背面。这意味着，最初，背面的背面将面向用户，并且由于我们之前的背面可见性属性而不可见。不要忘记用一个右括号将整个卡片部分括起来。

![](img/9fed931cf209ebe4b992d0978c48185b.png)

最后，这是奇迹发生的地方。我将应用一个只有当您将鼠标悬停在整个容器或卡片元素上时才会出现的样式，使其在 Y 轴上变换并旋转 180 度。这将向用户显示卡的背面。

![](img/8fc222c6c85d7efd77a4ee9b5b994d8f.png)

就是这样！大概有 50 行代码，你得到了一个翻转卡片的效果。通过一些额外的设计，你可以创建一些非常酷的个人资料卡片。想象一下，如果你把它设计得更时尚，那会是什么样子！

![](img/029c9403c59400ab8a2b06b6f5d990f3.png)

我希望这个教程是有帮助的。如果您有任何问题或意见，请随时联系我。感谢阅读！