# 如何使用 JavaScript 下载文件

> 原文：<https://javascript.plainenglish.io/how-to-download-a-file-using-javascript-fec4685c0a22?source=collection_archive---------1----------------------->

## 使用文件 Blob 下载文件

![](img/b4d4914075a48c7b03d7dfee3fb6f8eb.png)

Image From [Website](https://computing.which.co.uk/hc/en-gb/articles/360001287849-How-to-download-software-and-apps-safely)

# 前言

最近我开发了一个功能，需要在页面上添加一个下载按钮来支持下载 CDN 上托管的 PDF 文件。我记得下载一个文件非常简单，基本上和在新标签页打开一个链接一样。但是你想的越简单，在执行过程中遇到的问题就越多。

为了演示下载功能，本文以下载 [Google Analytics JavaScript 文件](https://www.google-analytics.com/analytics.js)为例。

# 使用带有下载属性的标签(不起作用)

下载一个带`<a>`标签的文件很简单，只要记得加一个下载属性告诉浏览器下载而不是打开超链接就可以了。

```
<a href="https://www.google-analytics.com/analytics.js" download="file">download the google analytics javascript file with a tag </a>
```

但是它不起作用，因为`download`只对[同源 URL](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)起作用。如果文件不是同一来源，浏览器将打开它，而不是下载它。

幸运的是，下载属性支持`blob:`方案。

# 使用 Blob 下载文件

`Blob`代表`Binary Large Object`，是一种可以存储二进制数据的数据类型。如果我们使用`fetch`来请求数据，那么响应可以被转换成 blob 类型。因此，下载文件的步骤如下:

1.  使用`fetch` API 下载脚本文件。
2.  将数据转换为 blob 类型。
3.  使用`URL.createObjectURL()`将 blob 对象转换为字符串。
4.  创建一个`<a>`元素来下载字符串。

使用功能下载:

```
downloadFile('[https://www.google-analytics.com/analytics.js'](https://www.google-analytics.com/analytics.js'), 'gooleAnalytics.js')
```

您可以在 CodePen 上测试:

# 结论

通过请求下载文件并将其转换为 blob 形式，可以避免浏览器的跨域限制，但在下载大文件时，可能需要很长时间，需要主动提示用户，以免被认为是 bug。

还有其他一些下载文件的方法:

[](/how-to-download-files-with-javascript-996b8a025d3f) [## 如何用 JavaScript 下载文件

### 通过 JavaScript 下载文件的三种方式

javascript.plainenglish.io](/how-to-download-files-with-javascript-996b8a025d3f) 

# 参考

1.  [URL . createobjecturl()—Web API | MDN(mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL)
2.  [< a >:锚元素— HTML:超文本标记语言| MDN(mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)
3.  [同源策略—网络安全| MDN(mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*****