# 24 个鲜为人知的 HTML 属性你可能想用✨📚

> 原文：<https://javascript.plainenglish.io/24-lesser-known-html-attributes-you-may-want-to-use-326dca041fdb?source=collection_archive---------9----------------------->

## 理解这些鲜为人知的 HTML 属性的用例及语法。

![](img/436d72acb3aef40fa28a34f797c9dd5d.png)

不久前，我写了一篇文章，介绍了有用的 HTML 标签及其类型。本周我决定写一个续集，回顾一些你可能会用到的 HTML 属性。

所有的属性都很容易设置，并且可以帮助您完成常见的任务，否则您将通过使用一些复杂的外部库来完成这些任务。

在本文中，我将回顾每个属性并包括代码片段，这样您就更容易理解属性的用例及语法。

## 1.接受

描述允许哪些输入文件类型。

```
<input type="file" accept=".jpg, .png">
```

仅与`<input>`标签的`file`类型一起使用。接受一个或多个文件类型的逗号分隔列表。要允许特定媒体类型的所有文件，请使用`accept="image/*"`。

## 2.自（动）调焦装置

它表示特定的元素应该关注页面负载。

```
<input type="text" autofocus>
```

文档或对话框中只能有一个元素具有`autofocus`属性。如果应用于多个元素，第一个元素将获得焦点。

## 3.输入模式

提示用户在编辑元素或其内容时可能输入的数据类型。

```
<input type="text" inputmode="url" />
<input type="text" inputmode="email" />
<input type="text" inputmode="numeric" />
```

这允许浏览器显示适当的虚拟键盘。

## 4.模式

指定一个正则表达式，表单提交时将根据该表达式检查`<input>`值。

```
<input name="username" id="username" pattern="[A-Za-z0-9]+">
```

## 5.需要

确保在提交表单之前必须填写元素。

```
<form action="/send_form.js">  
Username: <input type="text" name="username" required>  
<input type="submit">  
</form>
```

## 6.自动完成

指定浏览器是否有权限为填写电子邮件、电话号码、国家等表单字段提供帮助。

```
<input name="credit-card-number" id="credit-card-number" autocomplete="off">
```

有关可用`autocomplete`值的完整列表，请参见 [MDN 参考](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete)。

## 7.多重

该属性允许用户选择多个值。

```
<input type="file" multiple>
```

您可以使用`file`和`email`类型的`<input>`和`<select>`标签。

## 8.[计] 下载

指定当用户单击超链接时将下载目标。

```
<a href="document.pdf" download>Download PDF</a>
```

## 9.内容可编辑

该属性允许用户编辑元素的内容。

```
<div contenteditable="true">
  This text can be edited by the user.
</div>
```

## 10.只读

指定输入字段是只读的。

```
<input type="text" id="sports" name="sports" value="golf" readonly>
```

用户仍然可以定位到它，突出显示它，并从中复制文本。要禁止这些操作，请使用`disabled`属性。

## 11.隐藏的

指定元素是否可见。

```
<p hidden>This text is hidden</p>
```

## 12.拼写检查

定义是否检查元素的拼写错误。

```
<p contenteditable="true" spellcheck="true">Myy spellinng is checkd</p>
```

通常，所有不可编辑的元素都不会被检查，即使`spellcheck`属性被设置为`true`并且浏览器支持拼写检查。

## 13.翻译

指定当页面本地化时是否应翻译元素。

```
<footer><p translate="no">Printing Works, Inc</p></footer>
```

一个示例用例是您的公司名称、书名、位置等。

## 14.装货

指定浏览器是应该立即加载图像，还是推迟加载离屏图像，直到用户滚动到离屏图像附近。

```
<img src="https://cdn.mysite.com/media/image.jpg" loading="lazy">
```

`eager`是默认行为，`lazy`用于延迟(也就是延迟加载)。

## 15.错误

如果原始图像未加载，允许添加回退图像。

```
<img src="imageafound.png" onerror="this.onerror=null;this.src='imagenotfound.png';"/>
```

`this.onerror=null`用于在回退图像本身不可用时防止循环。

## 16.海报

允许在下载视频时添加要显示的图像。

```
<video 
src="https://cdn.mysite.com/media/video.mp4"
poster="image.png">
</video>
```

如果未指定，则在第一帧可用之前不会显示任何内容，第一帧将显示为标志帧。

## 17.控制

指定是否应该在播放器上显示音频/视频控件。

```
<audio controls
<source src="track11.mp3"  type="audio/mpeg">
</audio>
```

## 18.自动播放

确保音频/视频一加载就自动开始播放。

```
<video autoplay
src="https://cdn.mysite.com/media/myvideo.mp4"
poster="image.png">
</video>
```

## 19.环

指定音频/视频将在每次结束时重新开始。

```
<audio loop
<source src="track323.mp3"  type="audio/mpeg">
</audio>
```

## 20.引用

指向内容的来源，或引用更改或删除的位置。

```
<blockquote cite="https://mysite.com/original-source-url">
  <p>Some awesome quote</p>
</blockquote>
```

## 21.日期时间

它指定删除/插入文本的日期和时间。

```
<p>
  My plans for 2021 include visiting Thailand,
  <del datetime="2021-01-01T18:21">creating 6 courses,</del> 
  <ins datetime="2021-02-02T14:07">writing 12 articles.</ins>
</p>
<p>I will evaluate the completion on <time datetime="2021-12-31"></time>.</p>
```

当与`<time>`元素一起使用时，它以机器可读的格式表示日期和/或时间。

## 22.异步ˌ非同步(asynchronous)

确保脚本与页面的其余部分异步执行。

```
<script src="script.js" async></script>
```

`async`属性仅对外部脚本有效(`src`属性必须存在)。

## 23.推迟

确保在页面完成解析后执行脚本。

```
<script src="script.js" defer></script>
```

`defer`属性仅对外部脚本有效(`src`属性必须存在)。

## 24.可拖动的

指定元素是否可拖动。

```
<script>
const allowDrop = (e) => e.preventDefault();
const drag = (e) => e.dataTransfer.setData("text", e.target.id);
const drop = (e) => {
  var data = e.dataTransfer.getData("text");
  e.target.appendChild(document.getElementById(data));
}
</script>
<div ondrop="drop(event)" ondragover="allowDrop(event)" style="width:150px; height:50px; padding: 10px; border:1px solid black"></div>
<p id="drag" draggable="true" ondragstart="drag(event)">Drag me into box</p>
```

写作一直是我的激情所在，帮助和激励他人给我带来了快乐。如果您有任何问题，请随时联系我们！

在 [Twitter](https://twitter.com/madzadev) 、 [LinkedIn](https://www.linkedin.com/in/madzadev/) 和 [GitHub](https://github.com/madzadev) 上连接我！

访问我的[博客](https://madza.dev/blog)获取更多类似的文章。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*