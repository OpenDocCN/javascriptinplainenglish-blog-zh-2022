# 如何使用 JavaScript 显示或隐藏 div？

> 原文：<https://javascript.plainenglish.io/how-to-show-or-hide-a-div-using-javascript-5c882f70f9fa?source=collection_archive---------2----------------------->

![](img/9843f1f48271948abd0834b70e20d5f1.png)

Photo by [Tyler Callahan](https://unsplash.com/@tylercallahan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要在 web 应用程序中显示或隐藏一个 div。

在本文中，我们将看看如何用 JavaScript 显示或隐藏一个 div。

# 操作 style.display 属性

为了用 JavaScript 显示或隐藏一个 div，我们可以操纵`style.display`属性来改变 CSS `display`属性。

如果我们将 div 设置为`'block'`、`'inline'`或`'inline-block'`，我们就会显示它。

`'block'`使其成为块级，`'inline'`使其成为内联。`'inline-block'`类似于 block，只是它没有在元素后添加换行符。

如果我们把它设置为`'none'`，我们就会隐藏它。

例如，我们可以编写以下 HTML:

```
<button id='show'>
  show
</button>
<button id='hide'>
  hide
</button><div>
  hello
</div>
```

然后我们可以编写以下 JavaScript 代码来切换 div 的`display`属性:

```
const showBtn = document.querySelector('#show')
const hideBtn = document.querySelector('#hide')
const div = document.querySelector('div')showBtn.addEventListener('click', () => {
  div.style.display = 'block'
})
hideBtn.addEventListener('click', () => {
  div.style.display = 'none'
})
```

我们得到了显示和隐藏按钮以及带有`document.querySelector`的 div。

然后我们调用带有`'click'`参数的`addEventListener`来为按钮添加点击监听器。

当我们点击`showBtn`时，我们将`div.style.display`设置为`'block'`。

当我们点击`hideBtn`时，我们将`div.style.display`设置为`'none'`。

# 操作 style.visibility 属性

我们还可以更改`style.visibility`属性的值来显示或隐藏一个 div。

`display`和`visibility`的区别在于当我们改变 div 的值时，`display`会在屏幕上添加或删除 div。

`visibility`保留元素的空间，不管它是显示还是隐藏。

例如，我们可以写:

```
const showBtn = document.querySelector('#show')
const hideBtn = document.querySelector('#hide')
const div = document.querySelector('div')showBtn.addEventListener('click', () => {
  div.style.visibility = 'visible'
})
hideBtn.addEventListener('click', () => {
  div.style.visibility = 'hidden'
})
```

并保持 HTML 与前面的例子相同。

`'visible'`使 div 可见，`'hidden'`使其隐藏。

# 显示或隐藏元素集合

使用 JavaScript，我们可以很容易地显示或隐藏一组元素。

例如，如果我们有下面的 HTML:

```
<button id='show'>
  show
</button>
<button id='hide'>
  hide
</button><div>
  hello
</div>
<div>
  world
</div>
```

然后我们可以遍历每个 div 来显示和隐藏它们。

为此，我们编写了以下 JavaScript:

```
const showBtn = document.querySelector('#show')
const hideBtn = document.querySelector('#hide')
const divs = document.querySelectorAll('div')showBtn.addEventListener('click', () => {
  for (const div of divs) {
    div.style.display = 'block'
  }
})
hideBtn.addEventListener('click', () => {
  for (const div of divs) {
    div.style.display = 'none'
  }
})
```

我们获得按钮的方式与前面的例子相同。

然后我们用`querySelectorAll`得到两个 div。

在点击监听器中，我们遍历 div 并为每个 div 设置`style.display`属性。

我们可以对`visibility`属性做同样的事情。

# 结论

我们可以用 JavaScript 轻松地显示或隐藏一个或多个 div。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***