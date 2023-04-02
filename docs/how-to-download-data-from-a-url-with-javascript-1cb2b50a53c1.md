# 如何用 JavaScript 从一个 URL 下载数据？

> 原文：<https://javascript.plainenglish.io/how-to-download-data-from-a-url-with-javascript-1cb2b50a53c1?source=collection_archive---------0----------------------->

![](img/1d048881549af2338a617c9a90ddcc9c.png)

Photo by [Aaron Alvarado](https://unsplash.com/@aaronalvaradome?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望使用 JavaScript 以编程方式从 URL 下载数据到文件。

在他的文章中，我们将研究如何使用 JavaScript 以编程方式从 URL 下载数据到文件。

# 创建一个不可见的链接并单击它

我们可以创建一个不可见的链接，用 JavaScript 点击它下载一个文件。

为此，我们写道:

```
const downloadURI = (uri, name) => {
  const link = document.createElement("a");
  link.download = name;
  link.href = uri;
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
}
downloadURI('https://file-examples-com.github.io/uploads/2017/02/file-sample_100kB.doc', 'sample.doc')
```

我们有`downloadURI`函数，它获取要下载文件的`uri`和已下载文件的`name`。

在函数体中，我们用`document.createElement`方法创建了一个`a`元素。

然后，我们用以下内容设置`download`属性:

```
link.download = name;
```

将下载文件的文件名设置为`name`。

接下来，我们用以下内容设置`href`属性:

```
link.href = uri;
```

然后我们调用`appendChild`将`link`追加到 body 元素。

然后我们通过调用`click`点击`link`。

最后，我们调用`removeChild`从主体中移除链接。

现在我们运行`downloadURI`功能的时候，浏览器直接打不开的文件就要下载。

# 结论

我们可以创建一个不可见的链接，用 JavaScript 点击它下载一个文件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****