# SwiftUI vs UIKit

> 原文：<https://levelup.gitconnected.com/swiftui-vs-uikit-7824671c802d>

## 哪个更容易，你应该先学哪个

![](img/d9b36d34e23ee79b02edc6a66968fe47.png)

照片由 [Unsplash](https://unsplash.com/s/photos/learning?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的 [Dmitry Ratushny](https://unsplash.com/@ratushny?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄

## 哪个更容易，你应该先学哪个

尽管 SwiftUI 已经推出三年了，但它似乎仍然没有推出。初入编码界的人面临的一个挑战——还需要学习 UIKit 和 SwiftUI 吗，先学哪个，哪个最容易。

UIKit 已经存在了很长一段时间，我认为有理由说它是几乎 97%的商业应用程序的用户界面选择。所以很明显，如果你渴望加入 WhatsApp 这样的蓝筹应用开发者，那么你需要学习 UIKit。我认为，随着时间的推移，它也会变得有点像 Objective C，成为未来应用程序的附加值。

另一方面，SwiftUI 正在缓慢但肯定地走向成熟——从理论上讲，你可以在任何方面采用任何 UIKit 接口，只要后者仍然更优越。我还认为一些较小的参与者开始认真对待 SwiftUI，考虑将其用于较小的项目和他们认为可能可行的项目。

哪一个更直接——不容易直接比较——当你理解了基本语法之后，最显著的区别是布局方法。在 UIKit 中，您必须处理约束，这感觉像是您有更多的控制权——在 SwiftUI 中，如果您愿意，您必须更加努力地让一个更加定制的布局工作。这是一种不同的思维方式——这也是它的采用进展缓慢的原因之一。如果你认为这是一个安全策略，它是这样的。在 UIKit 中，您使用安全列表；你说什么都可以。在 SwiftUI 中，你使用 denylists，所以你说什么是不好的。布局动态是如此不同。

我觉得 SwiftUI 更容易上手——假设你没有或者有限的编码经验。这更容易，因为 SwiftUI 被设计为使用默认值来布局您的界面。这种模式类似于进入一辆装有自动变速箱的汽车。相反，UIKit 就像一个手动挡。这也更容易，因为苹果已经努力在 SwiftUI 中统一了许多框架的语法。统一意味着，当学习做不同的事情时，感觉像是对你现有知识的延伸。相反，UIKit 在过去的几年中有机地成长，新的框架引入了用自己的语法做新事情的方法。所以不同的事情，完全不同。

这种统一的一个例子是在动画世界。在 UIKit 中，有几个框架可以在 UI 中制作不同的动画。例如，在 UIKit 下，可以使用 CoreAnimation 或 CoreText 框架来动画化文本；他们有时可以做同样的事情，使用完全不同的语言结构。在 SwiftUI 中，您可以使用 withAnimation，或者实际上是 the。动画标签——就是这样。现在——等等——对不起，我说这不完全正确。

例如，在 SwiftUI 的最新版本中，他们引入了核心图形 Canvas 视图，去年我们获得了 SpriteKit 视图——苹果似乎已经引入了一些 UIKit 框架。所以使用它们的方式几乎和在 UIKit 中一样。也就是说，SwiftUI 的工作方式并不统一。

如果你从 SwiftUI 开始，你还会发现一个挑战，那就是它一直在变化，远远超过 ui kit——尽管有些人可能会说 Swift 到处都是。SwiftUI 1.0 与 SwiftUI2.0 略有不同，swift ui 2.0 与 SwiftUI 3.0 略有不同。它们差别不大，但足以打破东西，一个版本接一个版本。

谈到中断——嗯，SwiftUI 在调试视图时仍然有些无济于事。如果你使用过 SwiftUI，你就会明白我的意思。在第 20 行的 SwiftUI 视图中，一些代码有语法错误，SwiftUI 在第 2 行阻塞；告诉你这里有问题——我不知道是什么问题。

尽管 SwiftUI 更容易上手，但在学习细节方面，UIKit 可能仍然只是一个优势。更容易，因为它与 XCode 深度集成。当然，当使用不同的视图时，需要一段时间来理解不同选项的不同框的作用，但是这些框就在你的面前。相反，SwiftUI 是一个更加基于代码的范例，当然它有预览画布——但当涉及到数字时就不一样了，它不在你的面前——你需要花一半的时间去查找它。

但是，好吧，也许我说得够多了，我希望这足够清楚，你需要学习这两者，并且在未来十年需要这样做，好吧，也许少一点。如果我们回到驾驶对比，如果你想学习驾驶任何东西，你需要先学习手动档，所以 UIKit 人。当你感觉舒适时，你可以使用自动的 SwiftUI。也就是说，如果你没有转行的计划，或者确实在计划建立自己的帝国，那么从 SwiftUI 开始吧，它会更快地开始，你会在更短的时间内做更多的事情，我相信你会发现从大学里招聘程序员比你的项目基于 UIKit 更容易。[斯坦福现在教 SwiftUI，不是 UIKit]。引人深思的是，所有的墙上都写着。