# 如何使用 React 创建下载按钮

> 原文：<https://javascript.plainenglish.io/how-to-download-files-on-button-click-reactjs-f7257e55a26b?source=collection_archive---------4----------------------->

## 使用 React 创建下载按钮的指南。

![](img/24a5f8e39a87c58bee9f3756e30157b8.png)

当我在构建 [100 创意](https://thelearning.dev/100ideas.thelearning.dev)时，我想给用户一个选项，将他们的内容导出到一个文本文件中。这非常简单。这篇文章试图分享这些知识，并记录下来以备将来使用。假设您已经知道 React 的基本知识，让我们开始吧。

## 创建按钮

```
<div className="btnDiv">
     <button id="downloadBtn" value="download">Download</button>
</div>
```

## 添加事件处理程序

```
const downloadTxtFile = () => {
    console.log("download logic goes here")
}<div className="btnDiv">
     <button id="downloadBtn" onClick={downloadTxtFile} value="download">Download</button>
</div>
```

接下来，我们需要将一个事件处理程序挂接到按钮的`onClick`事件。让我们这样做，看看是否一切正常。

## 添加下载逻辑

要下载一个文件，我们需要四样东西。

1.  应该放入文件的内容
2.  文件对象
3.  下载文件对象的链接
4.  最后，模拟用户点击链接

```
const downloadTxtFile = () => {
    // text content
    const texts = ["line 1", "line 2", "line 3"]// file object
    const file = new Blob(texts, {type: 'text/plain'});// anchor link
    const element = document.createElement("a");
    element.href = URL.createObjectURL(file);
    element.download = "100ideas-" + Date.now() + ".txt";// simulate link click
    document.body.appendChild(element); // Required for this to work in FireFox
    element.click();
}
```

**注释**

1.  `Date.now()`是给文件下载添加时间戳
2.  文件 blob 不会自动给`texts`添加新行。您可以使用`[texts.join('\n')]`添加新行

*原发布于*[*https://the learning . dev*](https://thelearning.dev/how-to-download-files-on-button-click-reactjs)*。*

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*