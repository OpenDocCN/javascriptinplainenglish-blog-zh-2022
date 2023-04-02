# 如何获取 JavaScript 点击处理程序中被点击元素的 ID？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-id-of-the-clicked-element-in-the-javascript-click-handler-8ca398d848d6?source=collection_archive---------2----------------------->

![](img/dc445a1d7c3fbf737a10471c10b338da.png)

Photo by [Tawhidur R](https://unsplash.com/@abscondet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望获得我们在 JavaScript click 事件处理程序中单击的元素的 ID。

在本文中，我们将研究如何在 JavaScript click 处理程序中获取被点击元素的 ID。

# 将每个元素的 onclick 属性设置为同一个事件处理函数

当我们单击一个元素时，获取元素 ID 的一种方法是将每个元素对象的`onclick`属性设置为同一个 click 事件处理函数。

例如，我们可以编写以下 HTML:

```
<button id="1">Button 1</button>
<button id="2">Button 2</button>
<button id="3">Button 3</button>
```

然后我们可以编写以下 JavaScript 代码，将每个元素的事件处理程序设置为同一个 click 事件处理程序:

```
const onClick = function() {
  console.log(this.id, this.innerHTML);
}
document.getElementById('1').onclick = onClick;
document.getElementById('2').onclick = onClick;
document.getElementById('3').onclick = onClick;
```

`onClick`函数是每个按钮点击的事件处理程序。

`this`是我们点击的元素。

我们可以获取`id`属性来获取被点击元素的 ID。

而`innerHTML`有按钮的内容。

然后我们将`onClick`函数作为`onclick`属性的值分配给每个按钮元素。

因此，当我们点击按钮 1 按钮时，我们得到:

```
'1' 'Button 1'
```

记录在案。

当我们点击按钮 2 按钮时，我们得到:

```
'2' 'Button 2'
```

当我们点击按钮 3 时，我们得到:

```
'3' 'Button 3'
```

记录在案。

# 从事件对象中获取被点击的元素

获取我们在事件处理程序中单击的元素的另一种方法是从事件对象中获取它，这是事件处理程序函数中的第一个参数。

例如，我们可以编写以下 HTML:

```
<button id="1">Button 1</button>
<button id="2">Button 2</button>
<button id="3">Button 3</button>
```

和下面的 JavaScript 代码:

```
const onClick = (event) => {
  console.log(event.srcElement.id);
}
window.addEventListener('click', onClick);
```

我们调用`window.addEventListener`将点击事件监听器连接到`html` 元素。

然后我们从`event.srcElement`属性中获得被点击的元素。

我们可以用`id`属性获得该元素的 ID。

我们可以用`event.target`代替`event.srcElement`:

```
const onClick = (event) => {
  console.log(event.target.id);
}
window.addEventListener('click', onClick);
```

我们得到了同样的结果。

我们还可以检查我们点击的元素是否是一个带有`nodeName`属性的按钮。

例如，我们可以写:

```
const onClick = (event) => {
  if (event.target.nodeName === 'BUTTON') {
    console.log(event.target.id);
  }
}
window.addEventListener('click', onClick);
```

添加一条`if`语句，在运行`console.log`方法之前检查`event.target.nodeName`是否为`'BUTTON'`。

这样，我们只在点击按钮时运行点击处理程序代码。

# 结论

我们可以从 click 事件处理程序中获取被点击元素的 ID。

如果使用常规函数，我们可以从`this`中获取值。

或者我们可以从 click 事件处理程序的`event`对象中获得相同的值。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*