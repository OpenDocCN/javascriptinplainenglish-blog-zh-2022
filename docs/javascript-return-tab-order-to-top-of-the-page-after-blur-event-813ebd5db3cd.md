# 模糊事件后 JavaScript 将 Tab 键顺序返回到页面顶部

> 原文：<https://javascript.plainenglish.io/javascript-return-tab-order-to-top-of-the-page-after-blur-event-813ebd5db3cd?source=collection_archive---------13----------------------->

![](img/bf2ee5378cbcb02ef9e0adc29bce05d7.png)

`document.activeElement.blur()`正在按预期工作，并在单击时将焦点从“下一步”按钮上移开。但是，在下一个表单内容呈现后，单击 tab 会将焦点放在我的页脚上。焦点将转移到页脚，因为“下一步”按钮是表单选项卡流中的最后一个元素。所以`document.activeElement.blur()`看起来是有效的，因为聚焦环被移除了，但是 tab 键顺序没有被重置。

不使用`blur`，只需将表单的`[tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)`设置为`-1`和`[focus](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus)`即可。这里有一个普通的 JS 示例，您可以在 React 中使用`[ref](https://reactjs.org/docs/refs-and-the-dom.html)`来修改它。

## **document . query selector()**

`[Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)`方法`**querySelector()**`返回文档中匹配指定选择器或选择器组的第一个`[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)`。如果没有找到匹配，则返回`null`。

## EventTarget.addEventListener()

`[EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)`接口的`**addEventListener()**`方法设置了一个函数，每当指定的事件被传递到目标时，这个函数就会被调用。

常见的目标是`[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)`，或者其子节点`[Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)`和`[Window](https://developer.mozilla.org/en-US/docs/Web/API/Window)`，但是目标可以是任何支持事件的对象(比如`[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)`)。

**注意:**`addEventListener()`方法是*推荐的*注册事件监听器的方法。好处如下:

*   它允许为一个事件添加多个处理程序。这对于库、JavaScript 模块或任何其他需要与其他库或扩展良好协作的代码特别有用。
*   与使用一个`onXYZ`属性相比，当监听器被激活时，它给你一个更细粒度的阶段控制(捕获与冒泡)。
*   它适用于任何事件目标，而不仅仅是 HTML 或 SVG 元素。

## HTMLElement.focus()

方法将焦点设置在指定的元素上，如果它可以被聚焦的话。焦点元素是默认情况下接收键盘和类似事件的元素。

```
const form = document.querySelector('form');document.querySelector('#next').addEventListener('click', (ev) => {
  // Instead of blurring:
  // ev.target.blur();

  // Focus the form:
  form.focus({preventScroll: true});
});button,
form {
  border: 2px solid black;
  margin: 0.2rem;
  outline: none;
}*:focus {
  border-color: red;
}<form tabindex="-1">
  <button id="next" type="button">Next</button>
</form>
<footer>
  <button>Unrelated button</button>
</footer>
```

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***