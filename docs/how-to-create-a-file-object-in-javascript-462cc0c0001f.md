# 如何在 JavaScript 中创建文件对象

> 原文：<https://javascript.plainenglish.io/how-to-create-a-file-object-in-javascript-462cc0c0001f?source=collection_archive---------3----------------------->

## 使用 JavaScript 中的“file”构造函数创建 File 对象的指南。

![](img/d0506c0d4b0909a0da37a39189169ad7.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想要创建一个没有 JavaScript 代码的文件对象。

在本文中，我们将看看如何用 JavaScript 创建一个文件对象。

# 用文件构造函数创建一个文件对象

我们可以用 JavaScript 的`File`构造函数创建一个文件。

例如，我们可以写:

```
const parts = [
  new Blob(['you construct a file...'], {
    type: 'text/plain'
  }),
  ' Same way as you do with blob',
  new Uint16Array([33])
];const file = new File(parts, 'sample.txt', {
  lastModified: new Date(2020, 1, 1),
  type: "text/plain"
});const fr = new FileReader();fr.onload = (evt) => {
  document.body.innerHTML = `
   <a href="${URL.createObjectURL(file)}" download="${file.name}">download</a>
    <p>file type: ${file.type}</p>
    <p>file last modified: ${new Date(file.lastModified)}</p>
  `
}fr.readAsText(file);
```

我们用文件的各个部分创建了`parts`数组。

`parts`的第一个条目是一个包含文件内容的`Blob`实例。

`Blob`的第一个参数是数组中的文件内容。

`Blob`的第二个参数有文件元数据。

`parts`的第 2 和第 3 项有更多的文件内容。

接下来，我们使用`File`构造函数创建一个文件对象。

第一个参数是文件内容，我们存储在`parts`中。

第二个参数是文件名。

第三个参数是一些元数据。

接下来，我们创建一个`FileReader`实例，这样我们就可以读取文件内容。

我们设置它的`onload`属性来观察文件何时加载到内存中。

在回调中，我们从`file`中获取文件元数据。

我们使用`URL.createObjectURL`和`file`来创建一个 URL，这样我们就可以通过将它设置为`href`的值来从我们创建的链接中下载文件。

当我们用`file`调用`readAsText`时，`onload`方法将会运行。

现在，当我们单击下载时，我们会看到 sample.txt 文件下载，其中包含我们放入文本文件中的`parts`的内容。

# 结论

我们可以用`File`构造函数创建一个文件。然后我们可以用`FileReader`对象读取文件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***