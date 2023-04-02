# 如何用 JavaScript 把 HTML 渲染成图片？

> 原文：<https://javascript.plainenglish.io/how-to-render-html-to-an-image-with-javascript-d9d033c69823?source=collection_archive---------0----------------------->

![](img/d0a173e6e7277a645d247b28b7f83d34.png)

Photo by [Marita Kavelashvili](https://unsplash.com/@maritafox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望用 JavaScript 将 HTML 文档或节点呈现为图像。

在本文中，我们将研究如何使用 JavaScript 将 HTML 文档或节点呈现为图像。

# 使用 dom 到图像库

dom-to-image 库使得将 HTML 节点转换成图像变得很容易。

例如，如果我们有下面的 HTML:

```
<table>
  <tr>
    <td>col1 Val1</td>
    <td>col2 Val2</td>
  </tr>
  <tr>
    <td>col1 Val3</td>
    <td>col2 Val4</td>
  </tr>
</table><div>
</div>
```

然后，我们可以使用以下脚本标记添加库:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/dom-to-image/2.6.0/dom-to-image.min.js" integrity="sha512-01CJ9/g7e8cUmY0DFTMcUw/ikS799FHiOA0eyHsUWfOetgbx/t6oV4otQ5zXKQyIrQGTHSmRVPIgrgLcZi/WMA==" crossorigin="anonymous"></script>
```

或者我们可以添加 NPM 的库:

```
npm install dom-to-image
```

或者鲍尔:

```
bower install dom-to-image
```

然后我们可以通过编写以下 JavaScript 来使用它:

```
const table = document.querySelector("table");
const div = document.querySelector("div");
domtoimage.toPng(table)
  .then((dataUrl) => {
    const img = new Image();
    img.src = dataUrl;
    div.appendChild(img);
  })
  .catch((error) => {
    console.error(error);
  });
```

我们用想要渲染成图像的元素调用`domtoimage.toPng`。

然后我们得到`dataUrl`，它是被呈现元素的图像的 base64 字符串版本。

在`then`回调中，我们用`Image`构造函数创建了一个新的`img`元素。

然后我们将它的`src`属性设置为`dataUrl`。

然后我们用`img`调用`div.appendChild`将`img`追加到 div 中。

我们可以通过使用`async`和`await`语法来简化这一点:

```
const table = document.querySelector("table");
const div = document.querySelector("div");(async () => {
  try {
    const dataUrl = await domtoimage.toPng(table)
    const img = new Image();
    img.src = dataUrl;
    div.appendChild(img);
  } catch (error) {
    console.error(error);
  }
})()
```

`dataUrl`与`then`方法回调参数相同。

`error`与`catch`方法回调参数中的相同。

# 结论

dom-to-image 库让我们可以用 JavaScript 轻松地将 HTML 节点转换成图像。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*