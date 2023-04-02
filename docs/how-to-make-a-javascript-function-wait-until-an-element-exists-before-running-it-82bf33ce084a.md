# 如何让一个 JavaScript 函数等到元素存在后再运行？

> 原文：<https://javascript.plainenglish.io/how-to-make-a-javascript-function-wait-until-an-element-exists-before-running-it-82bf33ce084a?source=collection_archive---------1----------------------->

![](img/b8815b34d32760a83b4042ef92715e21.png)

Photo by [Tamara Gak](https://unsplash.com/@tamara_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望等到元素存在后再运行 JavaScript 函数。

在本文中，我们将了解如何让 JavaScript 函数在运行之前等待元素的存在。

# 使用 MutationObserver 监视要添加到 DOM 中的元素

我们可以使用现代浏览器提供的`MutationObserver`构造函数来观察元素的出现。

例如，如果我们有下面的 HTML:

```
<div id='container'></div>
```

然后，我们可以向它添加一个子元素，并通过编写以下内容来观察它的出现:

```
const container = document.getElementById('container')
setTimeout(() => {
  const div = document.createElement('div')
  div.textContent = 'hello'
  div.id = 'hello'
  container.appendChild(div)
}, 2000)const observer = new MutationObserver((mutations, obs) => {
  const hello = document.getElementById('hello');
  if (hello) {
    console.log(hello.innerText)
    obs.disconnect();
    return;
  }
});observer.observe(document, {
  childList: true,
  subtree: true
});
```

我们用一个回调函数调用`setTimeout`，该回调函数追加一个 div 作为 ID 为`container`的 div 的子 div。

然后，我们用一个带有`mutation`和`obs`参数的回调函数调用`MutationObserver`构造函数。

`obs`是返回的观察者。

在回调中，我们试图获取 ID 为`hello`的元素。

如果存在，那么我们得到元素的`innerText`属性值。

然后我们调用`disconnect`停止观察 DOM 中的变化。

然后我们调用`observer.observe`来观察`document`的变化。

`childList`设置为`true`以观察元素的添加或删除。

`subtree`也被设置为`true`以监视子元素的变化。

# 结论

我们可以使用`MutationObserver`构造函数轻松地观察 DOM 的变化。

因此，我们可以使用它在运行任何代码之前等待一个元素出现。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*