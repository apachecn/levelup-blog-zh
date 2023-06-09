# 带 Vue 和 GSAP 的动画卡片滑块— WotW

> 原文：<https://levelup.gitconnected.com/animated-card-slider-with-vue-gsap-7fc77cd9306a>

![](img/391d64648041f6597066672d3f555206.png)

这是本周系列**小工具的第三部分。**

> 查看本周所有的 [Widget 文章](https://levelup.gitconnected.com/wotw/home)并关注 gitconnected，确保你不会错过任何 Widget 教程。

今天我将向你展示使用 Vue 从头开始制作一个样式化的**卡片滑块**的过程。

这个小工具的灵感来自于[这个](https://uimovement.com/ui/5332/ticket-booking/)，看起来像这样:

![](img/1d13712e1ac633656e0c801304495b08.png)

## 准备

类似于[上一个小部件](http://ederdiaz.com/blog/2018/04/11/making-a-submit-button-with-loader-wotw/)，今天的小部件我们将使用 [vue.js](https://vuejs.org/) 进行交互，使用 [tweenlite](https://greensock.com/tweenlite) 进行动画。

## HTML 结构

基本上滑块的元素是**卡片**和**信息容器**，我将开始添加它们和一些类，以便能够在下一步对它们进行样式化:

```
<div id="slider" class="slider">
  <div class="slider-cards">
    <div class="slider-card"></div>
    <div class="slider-card"></div>
    <div class="slider-card"></div>
  </div>
  <div class="slider-info">
    <h1>Title</h1>
    <p>description</p>
    <button>Action</button>
  </div>
</div>
```

## 造型！

现在它看起来一点也不像最终产品。首先，我将使用以下规则模拟移动视口:

```
.slider {
  overflow: hidden;
  background-color: #1F1140;
  width: 360px;
  height: 640px;
}
```

对于卡片，我将在容器中使用一个边距来使第一张卡片居中，然后卡片将通过右边距彼此分开。我们还需要 cards 容器是相对的，并且在`slider-info` div 的顶部有一个 z-index。

卡片应该是`inline`的，这样它们就可以放在一起，但是为了方便起见，容器应该足够宽。在这种情况下，每张卡片大约 300 像素宽，因此容器将是 900 像素宽，因为我们有 3 张卡片(如果我们有更多的卡片，我们将需要计算所需的总宽度)。

最后，我们将添加一个方框阴影，给人以卡片漂浮的印象。

```
.slider-cards {
  position: relative;
  width: 900px;
  margin: 20px 50px;  
  z-index: 1;
}
.slider-card {
  display: inline-block;
  background-color: grey;
  overflow: hidden;
  width: 260px;
  height: 360px;
  margin-right: 30px;
  border-radius: 12px;
  box-shadow:0px 60px 20px -20px rgba(0, 0, 0, 0.3)
}
```

我们越来越近了

![](img/cead95ae9e88c032fda15a845a30a581.png)

现在轮到`slider-info`号进行改造了。我们将添加一个背景颜色，尺寸和空白的信息。

重要的是，它与卡片容器重叠，为了做到这一点，margin-top 将是负的，为了补偿，我们添加了一些`padding-top`。

我们需要确保`overflow`属性是*隐藏的*，以使底部的按钮和信息容器有相同的圆角。接下来就是用下面的方式设计标题、描述和按钮的样式了:

```
.slider-info {
  position: relative;
  overflow: hidden;
  background-color: white;
  margin-top: -200px;
  margin-left: 30px;
  padding: 200px 20px 0;
  width: 260px;
  height: 200px;
  text-align: center;
  border-radius: 8px;
}
.slider-info h1 {
  font-family: Arial Black, Gadget, sans-serif;
  line-height: 25px;
  font-size: 23px;
}
.slider-info p {
  font-family: Arial, Helvetica, sans-serif;
}
.slider-button {
  position: absolute;
  width: 100%;
  height: 50px;
  bottom: 0;
  left: 0;
  border: none;
  color: white;
  background-color: #E71284;
  font-size: 18px;
  font-family: Arial, Helvetica, sans-serif;
}
```

![](img/5aaae1eed0bd3e4b154d20b0310d83e3.png)

好多了。

## 用数据填充

我们准备开始使用 Vue，让我们创建一个实例，并从电影数据库中设置一些数据:

```
new Vue({
  el: '#slider',
  data: {
    slides: [
      {
        title: 'Ready Player One',
        description: 'When the creator of a popular video game system dies, a virtual contest is created to compete for his fortune.',
        image: 'https://image.tmdb.org/t/p/w300_and_h450_bestv2/pU1ULUq8D3iRxl1fdX2lZIzdHuI.jpg'
      },
      {
        title: 'Avengers: Infinity War',
        description: 'As the Avengers and their allies have continued to protect the world from threats too large for any...',
        image: 'https://image.tmdb.org/t/p/w300_and_h450_bestv2/7WsyChQLEftFiDOVTGkv3hFpyyt.jpg'
      },
      {
        title: 'Coco',
        description: 'Despite his family’s baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician...',
        image: 'https://image.tmdb.org/t/p/w300_and_h450_bestv2/eKi8dIrr8voobbaGzDpe8w0PVbC.jpg'
      }
    ]
  }
})
```

现在为了能够显示数据，我们需要定义默认选择的电影。这可以通过我们数据中的另一个变量`selectedIndex`和一个计算属性来实现，该属性可以根据所选的索引为我们提供幻灯片中的数据:

```
data: {
    // ... slide data
    selectedIndex: 0
  },
  computed: {
    selectedSlide () {
      return this.slides[this.selectedIndex]
    }
  }
```

然后，在我们的模板中，我们将使用`v-for`绑定卡片，并将信息绑定到相应的数据:

```
<div id="slider" class="slider">
  <div class="slider-cards">
    <div 
         v-for="(slide, index) in slides" 
         :key="index"
         class="slider-card">
      <img :src="slide.image" :alt="slide.title">
    </div>
  </div>
  <div class="slider-info">
    <h1>{{selectedSlide.title}}</h1>
    <p>{{selectedSlide.description}}</p>
    <button class="slider-button">BOOK</button>
  </div>
</div>
```

![](img/02cf0436ef16a5ae6c1c1ee5633a151d.png)

这看起来差不多完成了，至少从美学上来说，但是我们仍然需要…

## 互动

如果我们分解滑块的交互，当我们按下卡片，移动卡片和放开卡片时，它们基本上是 3。为了跟踪这些动作，我们需要将`@mouseDown`、`@mouseUp`和`@mouseMove`绑定到 Vue 实例中的方法。同样为了防止图像出现*重影*，它们应该具有属性`draggable=false`。

```
<div id="slider" class="slider" @mouseMove="mouseMoving">
  <div class="slider-cards">
    <div @mouseDown="startDrag"
         @mouseUp="stopDrag"
         v-for="(slide, index) in slides" 
         :key="index"
         class="slider-card">
      <img :src="slide.image" :alt="slide.title" draggable="false">
    </div>
  </div>
  <!-- slider info -->
```

现在我们需要在 Vue 端创建这些方法，我们还将在数据对象中添加几个变量:

```
data: {
    // ... other variables
    dragging: false,
    initialMouseX: 0,
    initialCardsX: 0,
    cardsX: 0
  },
  methods: {
    startDrag (e) {

    },
    stopDrag () {

    },
    mouseMoving (e) {

    }
  }
```

这三个方法都接收一个事件(在这种情况下我们称之为`e`)，但是我们只需要在`startDrag`和`mouseMoving`方法中使用它。在接下来的代码片段中，我将一步一步地分解这个过程来填充这 3 个方法，所以我将忽略其余的代码。

首先我们需要根据鼠标动作将`dragging`设置为*真*或*假*:

```
startDrag (e) {
  this.dragging = true
},
stopDrag () {
  this.dragging = false
},
mouseMoving (e) {

}
```

非常简单，现在我们希望只有在拖动卡片时才能移动它们，所以在`mouseMoving`方法中我们将添加这个条件:

```
startDrag (e) {
  this.dragging = true
},
stopDrag () {
  this.dragging = false
},
mouseMoving (e) {
  if(this.dragging) {

  }
}
```

好了，现在事情变得有趣了，当我们开始拖动时，我们需要跟踪卡片和鼠标的位置，属性`pageX`将告诉我们鼠标的位置，数据中的`cardsX`将跟踪卡片的容器位置:

```
startDrag (e) {
  this.dragging = true
  this.initialMouseX = e.pageX
  this.initialCardsX = this.cardsX
},
stopDrag () {
  this.dragging = false
},
mouseMoving (e) {
  if(this.dragging) {

  }
}
```

在存储了卡片和鼠标的初始 X 后，我们可以通过计算鼠标位置差来推断卡片容器的目标位置，此时`mouseMoving`方法执行如下:

```
startDrag (e) {
  this.dragging = true
  this.initialMouseX = e.pageX
  this.initialCardsX = this.cardsX
},
stopDrag () {
  this.dragging = false
},
mouseMoving (e) {
  if(this.dragging) {
    const dragAmount = e.pageX - this.initialMouseX
    const targetX = this.initialCardsX + dragAmount
    this.cardsX = targetX
  }
}
```

我们的组件几乎可以移动了，我们只需要找到一种方法将卡片的容器绑定到`cardsX`属性，这可以通过将该属性添加到 HTML:

```
...
<div class="slider-cards" :style="`transform: translate3d(${cardsX}px,0,0)`">
...
```

你可能会问“为什么你使用 translate3d 而不是普通的 2d translate？”，原因是 translate3d 是硬件加速的，大部分时候性能更好。你可以在这个[站点](https://jsperf.com/translate3d-vs-xy)自行查询。

幻灯片现在正在移动，但是有一个小问题，当我们放开它们时，它们会停留在我们放下它们的地方，而且电影信息不会改变。

我们实际上需要的是让他们找到最近的幻灯片并将其居中。

为了找到最近的幻灯片，我们只需要将当前位置除以卡片的宽度，然后将结果四舍五入。然后使用 TweenLite，我们将动画显示卡片到相应的位置:

```
stopDrag () {
  this.dragging = false

  const cardWidth = 290
  const nearestSlide = -Math.round(this.cardsX / cardWidth)
  this.selectedIndex = Math.min(Math.max(0, nearestSlide), this.slides.length -1)
  TweenLite.to(this, 0.3, {cardsX: -this.selectedIndex * cardWidth})
}
```

为了更好地理解这个公式，这张 gif 展示了`cardsX`值如何与`nearestSlide`相关联。

而现在最后的结果！

现在它只在桌面设备上工作，但这可能会通过“vue-touch”得到解决，你可以在[这篇文章](https://alligator.io/vuejs/vue-touch-events/)中了解更多。

这就是本周第三个**小部件**的内容。

如果你还没检查过上一个，[这里是](http://ederdiaz.com/blog/2018/04/11/making-a-submit-button-with-loader-wotw/)。

另外，如果你想看下周的某个小部件，可以在评论区发表。

下周见，关注 [gitconnected](https://levelup.gitconnected.com) 获取每周小工具！

*最初发表于*[*Eder díaz*](http://ederdiaz.com/blog/2018/04/18/animated-card-slider-with-vue-gsap/)*。*