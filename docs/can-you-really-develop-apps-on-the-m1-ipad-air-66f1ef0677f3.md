# 你真的能在 M1 iPad Air 上开发应用吗？

> 原文：<https://levelup.gitconnected.com/can-you-really-develop-apps-on-the-m1-ipad-air-66f1ef0677f3>

## 裁决出来了。我尝试建立一个 iOS 和一个 web 应用程序…

![](img/67b5f357bb62d73749f11cb38853eea1.png)

每次我看到与苹果应用程序开发相关的教程或课程，大多数学习者的最大障碍似乎是苹果设备的成本。此外，还有一些网络开发者更喜欢使用苹果公司生产的设备，而不是竞争对手的产品。我想它确实带有一些*【声望】*，一种虚荣的表现，当你开始工作时，在咖啡馆里拿出一个有苹果标志的东西。我不能说我不明白这一点，还有一个额外的好处是，与老掉牙的联想或戴尔相比，苹果设备本身往往是灵感的来源。

所以，考虑到所有这些，当然毫不奇怪**当有人声称可以在比现有任何设备都更便宜的苹果设备**上进行编程时，我总是很好奇，我觉得这需要独立验证。

我爱苹果，但在努力成为一个务实的人和魔鬼的拥护者时，我知道除了他们制造的伟大设备，他们真正闪耀的是营销。大多数人在看完他们谈论他们正在推出的最新产品后，几乎每个人都想要一个，即使他们完全知道他们要么不需要它，它真的没有那么特别，它的性价比很差，等等，如果他们有无限的财力，他们至少仍然会为了新奇而得到它。

今年春天，苹果公司对 2022 年的 iPad Air 进行了另一次大胆的营销宣传，该产品现在配备了 M1 芯片，与 iPad Pro、MacBook Air、Mac Mini 和 13 英寸 MacBook Pro 拥有的 M1 芯片相同！不，它一点也不慢也不慢！这使 iPad Air 与 MacBook Pro 处于同一联盟，尽管是入门级的，但我可以肯定的是，MacBook Pro 可以在上面编码。我这样做了将近一年，没有遇到任何大问题。在 iPad Air 中拥有同样的魅力绝对不容小觑！但是…因为总有“但是”…

## 真的能在上面编码吗？

你猜怎么着经过大约十年的软件工程，使用苹果设备进行工作，从 2010 年的 MacBook Pro 到现在你可以买到的最新的 M1 Max，拥有至少三个版本的 iPad、iPad Minis 和 iPad Airs，**我已经意识到 M1 的加入虽然是故事的关键部分，但真正需要测试的是这个特定硬件外壳中的 iPadOS** 。

为什么 iPad Air 是一个如此有吸引力的选择，为什么我努力做这个实验，显然是因为它提供的价格价值。下一个最便宜的苹果新机器是 799 欧元的 Mac Mini。只有一个问题。就其本身而言，是没有用的。没有屏幕，是它最大的缺点，没有外设，第二。

iPad Air 支持蓝牙和 USB-C，这意味着如果你已经有了无线外设，你可能已经准备好了。如果没有，花 20 美元你就能买到一个便宜的罗技套餐，那就足够了。还有屏幕…嗯，技术上来说你不需要，因为你有 10 英寸的 iPad Air 屏幕，事实上，这是一个非常好看的屏幕，与我在 waybackwhen 的旧 11 英寸 MacBook Air 相比，我在那个小东西上做了一些体面的网络开发付费合同工作！理论上和规格上，它拥有入门级开发机器所需的一切。

## 测试 iOS 开发

苹果 100%声称你可以在 M1 iPad Air 上开发 iOS 和 iPadOS 应用。我对此进行了测试。我试图构建一个中等复杂度的应用程序，将 AR 作为其功能之一。

我承认，使用最新的 **Swift Playgrounds 是一种足够流畅的体验**，它绝对允许人们不仅学习编码，还可以开发和发布应用程序。设置项目、导入库和处理代码并不困难，而且与 Xcode 相比，这是一种更加简单直观的体验。

由于即时错误突出显示和代码建议，解决编译问题很容易。**如果你对 Swift 有一点点熟悉，你真的可以在几个小时内构建一个小应用程序，甚至可以提交给 App Store 进行内部测试。但是有一点需要注意。您只能构建某些应用程序。**

在 iPad Air M1 上编码不到一个小时，这变得非常明显…

> iPad Pro 有很多限制，M1 iPad Air 有更多限制。

有些应用程序类型你肯定无法在 iPad 上开发。

*   **使用 AR** 的应用，因为它没有激光雷达传感器。试图开发 AR 应用是徒劳的，因为你几乎无法在开发时测试它们。
*   **中度到高度复杂的应用程序。看，我已经开发了小到企业规模的应用程序。知道一个应用程序的大小可以在很大程度上决定你工作的开发环境，M1 iPad Air 根本不具备处理这种情况的能力，无论硬件配置如何。**

**上述例外使得 M1 iPad Air 不适合进行严肃编码。**它确实允许学习 Swift 和苹果应用发布流程。就这一点而言，它非常合适，但与 MacBook Air 相比，这是一项昂贵的投资。

> 任何认真对待苹果应用程序开发的人，都将在不到一年的时间里超越 M1 iPad Air。

## 测试 web 开发

完全公开——这不是我第一次尝试在 iPad 上开发网络应用。当时我在 iPad Mini 上使用 Coda 的所有东西！而且成功了。算是吧。对于非常基本的网站来说，它完成了任务。如果你所要做的就是开发静态网站，把它上传到像 GoDaddy 这样的网络服务器上，这是可行的。

不过，从那以后事情发生了变化，但我认为没有人们希望的那么多。虽然 Blink Shell 确实能在 M1 的 iPad Air 上运行终端和 SSH 客户端，但这并不能使它成为一台开发者机器。绝不可能。人们至少需要一个像样的代码编辑器，但最好是一个 IDE 和一个本地服务器。即使运行一个简单的开箱即用的 React 应用程序也需要它，更不用说整个 MERN 堆栈了。

自从我上一次尝试以来，确实发生了变化的是像 **Play.js** 或 **CodeSandbox 项目**这样的工具的发布，后者仍处于测试阶段。当然，Play.js 也是一个 CodeSandbox 产品，这并不奇怪，很快就变得很明显，它是一个在浏览器中模拟他们在线提供的大多数内容的客户端。在这方面，**M1 的 iPad Air 在技术上是一个足够强大的设备，可以满足网络开发的需求**，尽管只支持一些框架和库，Angular 不在其中。如果你更喜欢 Vue、React、Node 或 Svelte，那么你很幸运，但话说回来，你不需要在平板电脑中安装 M1 SOC 来运行这些功能。你可以在普通的 iPad 上做到这一点——你知道——你能找到的最便宜的全新的 iPad。

如果我非常务实和诚实——基本上我只是做我平常的自己——**在 M1 iPad Air 上开发网络应用不是一个可行的想法**。

> iPadOS 在网络开发方面的局限性是无法被一个强大到令人抓狂的处理器所克服的。

当然，某些较小类型的项目可以开始，甚至可能从 GitHub 中提取并即时编辑，但这非常不可靠，我没有看到任何专业人士自愿选择 iPad Air(或任何 iPad)作为他们日常网络开发的驱动力。

对于那些希望学习 web 开发的人来说，这与我对 iOS 应用程序开发的想法非常相似。**不到一年的时间，你很可能就无法使用 M1 的 iPad Air 了**，如果你正在学习训练营式的在线课程，这根本不是一个适合学习和发展的环境。如果你想认真对待网络开发，又买不起 Mac Mini 或 MacBook Air，那就买一个树莓派(Raspberry Pi)、一些便宜的键盘鼠标组合和一个二手显示器，即使是最便宜的新 iPad，价格也只有它的一半。

## 判决

苹果制造好的产品。我不能否认。苹果也做了非常好的营销。不可否认的是。但是，声称人们可以在 M1 iPad Air 上开发应用程序更多的是一个技术问题，而不是现实。作为一个苹果迷，我了解营销和公司如何赚钱，我认为他们的这种说法近乎不道德。

像我这样的技术头脑是很难被愚弄的，当我们不知道一些事情时，我们会研究，直到我们理解了声明的局限性，或者发现了细则。但我们只是苹果目标市场的一小部分。当塔米和蒂米的妈妈在复活节给他们俩买了新的 M1 iPad air，以引导他们学习计算机科学和编程时，她和她的双胞胎会很快意识到他们做出了错误的购买决定。

> 苹果反复将 M1 iPad Air 与价格相似的个人电脑进行比较，但忘记了房间里的巨大大象——iPad OS，坦白地说，对开发者来说，这仍然是 iPad 最糟糕的功能。

**作为一名软件工程师，我不能也不会向任何类型的严肃代码推荐 M1 iPad Air**，无论是学习还是实际开发。从一个务实的程序员来说，这是一个很难通过的关卡。

[](https://attilavago.medium.com/membership) [## 通过我的推荐链接加入 Medium-Attila vágó

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

attilavago.medium.com](https://attilavago.medium.com/membership) [](https://medium.com/codex/apple-tricked-us-with-the-m1-ipad-air-early-hands-on-impressions-6339f83b78a3) [## 苹果用 M1 iPad Air 欺骗了我们——早期的实际体验

### 一个“新”的旧 iPad Air，苹果公司的一个狡猾但聪明的举动…

medium.com](https://medium.com/codex/apple-tricked-us-with-the-m1-ipad-air-early-hands-on-impressions-6339f83b78a3) [](https://medium.com/codex/why-i-reluctantly-ordered-the-apple-studio-display-6bf671299668) [## 为什么我不情愿订购苹果工作室显示器

### 出于同样的原因，许多人会和我有同样的感受…

medium.com](https://medium.com/codex/why-i-reluctantly-ordered-the-apple-studio-display-6bf671299668) [](https://medium.com/codex/can-apples-ultrafusion-technology-mean-that-m2-is-still-a-while-away-150089387104) [## 苹果的超融合技术是否意味着 M2 还需要一段时间？

### 如果他们把两个 m1“粘”在一起，他们可能还能粘三个、四个……?

medium.com](https://medium.com/codex/can-apples-ultrafusion-technology-mean-that-m2-is-still-a-while-away-150089387104) 

*阿提拉·瓦戈——软件工程师，一次一行代码地改善世界。永远的酷呆子，代码和博客的作者。网络无障碍倡导者，乐高迷，黑胶唱片收藏家。喜欢精酿啤酒！*