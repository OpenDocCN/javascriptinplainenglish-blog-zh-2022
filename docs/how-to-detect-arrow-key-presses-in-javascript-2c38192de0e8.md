# 如何在 JavaScript 中检测箭头键的按下？

> 原文：<https://javascript.plainenglish.io/how-to-detect-arrow-key-presses-in-javascript-2c38192de0e8?source=collection_archive---------7----------------------->

## 如何在 JavaScript 中检测箭头键的指南。

![](img/f208ddacdd420fc229a7a5ee271c9e00.png)

Photo by [Paweł Czerwiński](https://unsplash.com/@pawel_czerwinski?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们需要检测 JavaScript web 应用程序中的箭头键。

在本文中，我们将研究如何在 JavaScript 中检测箭头键的按下。

# 使用 keyCode 属性

我们可以监听`keydown`事件，并从事件对象中获取`keyCode`属性。

例如，我们可以写:

```
document.onkeydown = (e) => {
  e = e || window.event;
  if (e.keyCode === 38) {
    console.log('up arrow pressed')
  } else if (e.keyCode === 40) {
    console.log('down arrow pressed')
  } else if (e.keyCode === 37) {
    console.log('left arrow pressed')
  } else if (e.keyCode === 39) {
    console.log('right arrow pressed')
  }
}
```

将 keydown 事件处理函数分配给`document.onkeydown`属性。

这让我们可以监听 HTML 文档中的 keydown 事件。

然后我们可以从`e`事件对象中获取`keyCode`属性，看看哪个键被按下了。

38 是向上箭头的代码。

40 是向下箭头的代码。

37 是左箭头的代码。

39 是右箭头的代码。

同样，我们可以使用`addEventListener`方法来添加 keydown 事件监听器:

```
document.addEventListener('keydown', (e) => {
  e = e || window.event;
  if (e.keyCode === 38) {
    console.log('up arrow pressed')
  } else if (e.keyCode === 40) {
    console.log('down arrow pressed')
  } else if (e.keyCode === 37) {
    console.log('left arrow pressed')
  } else if (e.keyCode === 39) {
    console.log('right arrow pressed')
  }
})
```

# 使用 key 属性

此外，我们可以将事件对象的`key`属性用于作为字符串而不是数字按下的键。

例如，我们可以写:

```
document.onkeydown = (e) => {
  e = e || window.event;
  if (e.key === 'ArrowUp') {
    console.log('up arrow pressed')
  } else if (e.key === 'ArrowDown') {
    console.log('down arrow pressed')
  } else if (e.key === 'ArrowLeft') {
    console.log('left arrow pressed')
  } else if (e.key === 'ArrowRight') {
    console.log('right arrow pressed')
  }
}
```

我们将`key`属性值与键的字符串名称进行比较。

同样，我们可以使用`addEventListener`方法通过编写以下内容来添加按键监听器:

```
document.addEventListener('keydown', (e) => {
  e = e || window.event;
  if (e.key === 'ArrowUp') {
    console.log('up arrow pressed')
  } else if (e.key === 'ArrowDown') {
    console.log('down arrow pressed')
  } else if (e.key === 'ArrowLeft') {
    console.log('left arrow pressed')
  } else if (e.key === 'ArrowRight') {
    console.log('right arrow pressed')
  }
})
```

# 结论

我们可以通过监听 keydown 事件来检测箭头键的按下。

在事件监听器中，我们可以检查事件对象的`key`或`keydown`属性，看看哪个键被按下了。

现在你知道了。感谢您的阅读。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***