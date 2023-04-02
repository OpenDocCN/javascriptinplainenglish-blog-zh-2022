# 当一个元素用 JavaScript 变得可见时，如何添加一个事件监听器？

> 原文：<https://javascript.plainenglish.io/how-to-add-an-event-listener-for-when-an-element-becomes-visible-with-javascript-29325b556653?source=collection_archive---------0----------------------->

![](img/88627c9c6cf8799d5144c85eb3ee6bd0.png)

Photo by [Anne Nygård](https://unsplash.com/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望观察一个元素何时出现在屏幕上。

在本文中，我们将通过 JavaScript 来了解元素何时在屏幕上可见。

# 使用 IntersectionObserver API

我们可以使用 IntersectionObserver API 来观察一个元素何时可见或不可见。

例如，如果我们有下面的 HTML:

```
<div></div>
```

然后我们可以添加以下 JavaScript:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  p.id = `el-${i}`
  div.appendChild(p)
}const options = {
  rootMargin: '0px',
  threshold: 1.0
};const observer = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    console.log(entry.intersectionRatio > 0 ? 'visible' : 'invisible');
  });
}, options);const element = document.querySelector('#el-50')
observer.observe(element);
```

用`for` 循环向 div 中添加元素。

然后我们使用`IntersectionObserver`构造函数来添加交叉点观察器。

`options`对象有`rootMargin`，这是元素被视为可见时的边距。

`threshold`是元素在屏幕上可见的程度。

该值介于 0 和 1 之间。

我们向`IntersectionObserver`传递一个回调函数，当我们正在观察的元素在屏幕上出现或消失时，这个函数就会运行。

我们循环通过`entries`来获得交叉点条目对象。

我们记录`entry.intersectionRatio`并检查它是否大于 0，看看我们正在观察的元素是否可见。

最后，我们调用`observer.observe`来观察 ID 为`el-50`的元素在屏幕上可见或不可见。

# 结论

我们可以使用 IntersectionObserver API 来观察一个元素何时可见或不可见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****