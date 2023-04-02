# 如何用 JavaScript HTML5 Canvas 画出一条通过 N 个点的光滑曲线？

> 原文：<https://javascript.plainenglish.io/how-to-draw-a-smooth-curve-through-n-points-using-javascript-html5-canvas-86ecb84b6d6d?source=collection_archive---------3----------------------->

![](img/ea49358ef931cbc251045c3b03c4541b.png)

Photo by [Jan Kopřiva](https://unsplash.com/@jxk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想在网页上画一条平滑的曲线，通过一些点。

在本文中，我们将看看如何使用 JavaScript HTML5 canvas 绘制一条通过多个点的平滑曲线。

# 使用 quadraticCurveTo 方法

我们可以使用 canvas context 对象附带的`quadraticCurveTo`方法来绘制一条穿过`n`点的曲线。

要使用它，我们可以先编写下面的 HTML:

```
<canvas width="200" height="200"></canvas>
```

然后我们可以通过写来使用它:

```
const points = [{
  x: 1,
  y: 1
}, {
  x: 20,
  y: 30
}, {
  x: 30,
  y: 40
}, {
  x: 40,
  y: 20
}, {
  x: 50,
  y: 60
}]const canvas = document.querySelector('canvas')
const ctx = canvas.getContext("2d")
ctx.beginPath();
ctx.moveTo(points[0].x, points[0].y);for (const point of points) {
  const xMid = (point.x + point.x) / 2;
  const yMid = (point.y + point.y) / 2;
  const cpX1 = (xMid + point.x) / 2;
  const cpX2 = (xMid + point.x) / 2;
  ctx.quadraticCurveTo(cpX1, point.y, xMid, yMid);
  ctx.quadraticCurveTo(cpX2, point.y, point.x, point.y);
}
ctx.stroke();
```

我们有`points`数组，它有一些点的`x`和`y`坐标。

然后我们得到带有`document.querySelector`的画布。

接下来，我们调用`getContext`方法来获取上下文对象。

然后我们调用`beginPath`开始画图。

然后我们调用`moveTo`移动到第一个点。

接下来，我们调用`quadraticCurveTo`从我们计算的第一个点(`cpX1`、`point.y`)到(`xMid`、`yMid`)绘制曲线。

然后我们画出从(`cpX2`、`point.y`)到(`point.x`、`point.y`)的曲线。

`cpX1`和`cpX2`是一点和下一点之间线段的 x 和 y 的中心点。

最后，我们调用`stroke`在屏幕上画线。

# 结论

我们可以使用画布上下文对象附带的`quadraticCurveTo`方法，通过`n`点绘制一条曲线。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****