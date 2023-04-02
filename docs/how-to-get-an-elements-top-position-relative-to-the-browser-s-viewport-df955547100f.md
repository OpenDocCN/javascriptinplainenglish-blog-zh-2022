# 如何获取一个元素相对于浏览器视口的顶部位置？

> 原文：<https://javascript.plainenglish.io/how-to-get-an-elements-top-position-relative-to-the-browser-s-viewport-df955547100f?source=collection_archive---------1----------------------->

![](img/1aee0d16d616cd957b5eda257584f64a.png)

Photo by [Paul Gilmore](https://unsplash.com/@pueblovista?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要获得一个元素相对于浏览器视窗的顶部位置。

在本文中，我们将研究如何获取元素相对于浏览器视窗的顶部位置。

# 使用 getBoundingClientRect 方法

我们可以使用`getBoundingClientRect`方法获得一个元素相对于其视窗的位置。

例如，我们可以写:

```
const div = document.querySelector('div')
const {
  top: t,
  left: l
} = div.getBoundingClientRect();
console.log(t, l)
```

我们用`querySelector`得到 div。

然后我们在它上面调用`getBoundingClientRect`来获得一个具有`top`和`left`属性的对象。

`top`有相对于视口顶部的位置。

`left`有相对于视口左侧的位置。

两者都以像素为单位。

如果我们想考虑滚动，那么我们把`scrollY`值加到`top` 上，把`scrollX`值加到`left`上。

例如，我们可以写:

```
const div = document.querySelector('div')
const {
  top: t,
  left: l
} = div.getBoundingClientRect();
const {
  scrollX,
  scrollY
} = window
const topPos = t + scrollX
const leftPos = l + scrollY
console.log(topPos, leftPos)
```

将滚动位置包含在元素的位置中。

# 结论

我们可以通过使用`getBoundingClientRect`方法获得元素相对于视口的位置。