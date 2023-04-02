# 下载前端文件的 5 种方法

> 原文：<https://javascript.plainenglish.io/5-ways-to-download-front-end-files-a321271e7f5d?source=collection_archive---------0----------------------->

## 1.一个标签，2。window.open，请按 3。location.href，4。位置。？其他属性，以及 5。XMLHttpRequest。每种方法的优缺点是什么？

![](img/9e037722a5d801654d0014dcf4ef76f6.png)

前端涉及的文件下载还有很多应用场景，那么前端文件下载有多少种方式呢？每种方法的优缺点是什么？下面就一个一个介绍吧。

# 1.一个标签

文件下载是通过 a 标签的下载属性实现的。这种方法是最简单也是最常用的方法。让我们先来看看示例代码:

```
<a href="[http://www.](http://www.baidu.com)google.com" download="google.html">download</a>
```

在上面的例子中，我们点击了下载，发现跳转到了 Google 的首页，并没有实际下载文件。
因为一个标签下载只能下载同一来源的文件，如果是跨域文件，包括图片、音视频等媒体文件，则是预览版，不能下载。
上面的代码是通过写标签直接实现文件下载，我们也可以通过 js 来实现，代码如下:

```
const a = document.createElement('a')
a.href = '[http://www.google.com'](http://www.baidu.com')
a.download = 'google.html'
a.click()
```

效果和上面一样，不下载文件就跳转到百度首页。
这里的重点是标签的下载属性，这是 HTML5 中新增的。
其功能是指定下载的文件名。如果未指定，将根据请求内容的内容处理来确定下载的文件名。如果没有 Content-Disposition，那么所请求的 URL 的最后一部分将被用作文件名。

# 2.窗口.打开

上面使用标签的情况也可以通过 window.open 实现，效果是一样的，代码如下:

```
window.open('[http://www.google.com'](http://www.baidu.com'), '_blank')
```

这里的 _blank 是指定开口的方式。如果未指定，将在当前页面打开。在这里指定 _blank 意味着在新的页面上打开它。

也可以使用标签的下载属性，代码如下:

```
window.open('[http://www.google.com'](http://www.baidu.com'), '_blank', 'download=google.html')
```

当然这种方法也是有缺陷的。与标签相比，该方法不能下载。html，。htm，。xml，。xhtml 等文件，因为这些文件会被当作 html 文件，所以它们会直接出现在当前页面上。打开。
跨域下载文件也是不可能的。毕竟是 window.open，不是 window . download(window . download 是虚构的)。

# 3.location.href

这个方法和 window.open(url)一样，代码如下:

```
location.href = '[http://www.google.com'](http://www.baidu.com')
```

这种方法有 window.open 的所有缺陷，不建议使用。这里只是作为一种理解，不做过多解释。

# 4.位置。？其他属性

这里的其他是指可以跳转到页面的属性，比如 location.assign、location.replace、location.reload 等。这些属性可以实现文件下载，代码如下:

```
location.assign('[http://www.google.com'](http://www.baidu.com'))
location.replace('[http://www.google.com'](http://www.baidu.com'))
location.reload('[http://www.google.com'](http://www.baidu.com'))
```

这里的 location.reload 有点特殊，它的功能是重载当前页面，但是它也可以接受一个参数，这个参数就是要跳转的页面，所以它也可以实现文件下载。
当然，和 location.href 一样，这些方法也有相同的缺点，也各有各的属性特点。这只是为了扩充知识面，不做过多解释。

# 5.XMLHttpRequest

这个方法就是我们常说的 ajax 下载，包括 Axios，fetch 等。都是一样的，代码如下:

```
const xhr = new XMLHttpRequest()
xhr.open('GET', '[http://www.google.com'](http://www.baidu.com'))
xhr.send()xhr.onload = function () {
  const blob = new Blob([xhr.response], { type: 'text/html' })
  const a = document.createElement('a')
  a.href = URL.createObjectURL(blob)
  a.download = 'google.html'
  a.click()
}
```

这里就不说 XMLHttpRequest 相关的知识了，只说文件下载相关的部分。
这里的主要逻辑是，当我们的请求成功时，我们会得到响应体的响应，这个响应就是我们要下载的内容，然后我们将其转换成 blob 对象，再通过 url.createObjectURL 创建一个 URL，然后通过 a 标签的 download 属性实现文件下载。
这里有两个知识点，一个是 blob 对象，一个是 URL.createObjectURL

# 5.1 斑点

下面是 blob 对象的定义，来自 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Blob) :

```
The Blob object represents a blob, which is a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) so its methods can be used for processing the data.Blobs can represent data that isn't necessarily in a JavaScript-native format. The [File](https://developer.mozilla.org/en-US/docs/Web/API/File) interface is based on Blob, inheriting blob functionality and expanding it to support files on the user's system.
```

blob 对象是 html5 中的一个新对象。它的功能是存储二进制数据，如图片、视频、音频等。其用法如下:

```
/**
 * [@param](http://twitter.com/param) {Array}  array binary data
 * [@param](http://twitter.com/param) {Object} options configuration item
 *      [@param](http://twitter.com/param) {String} options.type The file type, which represents the MIME type of the array contents that will be put into the blob.
 *      [@param](http://twitter.com/param) {String} options.endings Used to specify how strings containing line terminators \n are written. Defaults to transparent, which means that line terminators will not be modified. It can also be specified as native, which means that \n will be converted to \r\n.
 */
const blob = new Blob([], { type: '' })
```

这里主要关心的是类型属性。默认情况下，blob 对象没有 type 属性，所以 blob 是一个非类型化的 blob，文件不会被破坏，但是不能正常识别。

# 5.2 URL.createObjectURL

以下来自 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL) :

```
The URL.createObjectURL() static method creates a string containing a URL representing the object given in the parameter.The URL lifetime is tied to the [document](https://developer.mozilla.org/en-US/docs/Web/API/Document) in the window on which it was created. The new object URL represents the specified [File](https://developer.mozilla.org/en-US/docs/Web/API/File) object or [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) object.
```

此方法用于创建 url。它的功能是将 blob 对象转换成 url。此 url 可用于下载文件或预览文件。代码如下:

```
const url = URL.createObjectURL(blob)
```

这里需要注意的是，这个 url 的生命周期是和创建它的窗口中的文档绑定在一起的，也就是说，当我们的文档被销毁时，这个 url 就会失效，所以我们需要在合适的时候销毁它，代码显示如下:

```
URL.revokeObjectURL(url)
```

回到我们刚刚下载的问题，我们通过 blob 对象解决了它，但是我们的 type 属性是硬编码的。如果文件类型确定了就没有问题，但是如果这个接口是下载文件的接口，文件可以是各种类型，我们该怎么处理呢？
这里没有正确答案。首先是与接口提供商协商。谈判方案不确定。二是通过响应的头获取文件的类型，这也是我们要讲的:

```
const type = response.headers['content-type']const blob = new Blob([response.data], { type })
```

这里我们通过响应的头获取类型，然后创建 blob 对象，这样文件就可以正确下载了。
事实上，内容类型也可以是应用/八位流。这时，我们需要通过 file-type 获取文件的类型。
下面的代码使用 file-type 来获取文件的类型:

```
import {fileTypeFromStream} from 'file-type';const type = await fileTypeFromStream(response.body);
const blob = new Blob([response.data], { type })
```

文件类型的使用可以参考这里的[。](https://github.com/sindresorhus/file-type)

# 总结

上面这么多解决方案，其实最后都落在一个标签上，所以不管是通过浏览器内置的行为下载，还是通过 ajax 下载，最后文件下载都是浏览器的行为。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*