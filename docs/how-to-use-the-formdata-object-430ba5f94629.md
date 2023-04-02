# 如何使用 FormData 对象

> 原文：<https://javascript.plainenglish.io/how-to-use-the-formdata-object-430ba5f94629?source=collection_archive---------6----------------------->

## 了解如何在 JavaScript/TypeScript 中使用 FormData 对象

![](img/808c6b4759b068e1b8701dd680934131.png)

JavaScript FormData 接口为我们提供了一种创建表示表单字段及其值的键值对对象的方法。

如果编码类型设置为`“multipart/form-data"`，它使用的格式与表单使用的格式相同。这使得在与 fetch 或 XMLHTTPRequest 一起发送表单数据之前格式化表单数据变得容易。

## 什么是 FormData 对象？

为了完全理解 FormData 对象，我们需要知道它是什么。FormData 接口是所有主流浏览器都支持的原生浏览器接口[。](https://caniuse.com/mdn-api_formdata)

创建这个接口是为了让开发人员更容易地访问表单域的内容及其值。这有助于准备提交给 API 的内容，或者有助于对所述字段执行验证。

## 如何创建 FormData 对象？

可以使用 FormData 构造函数创建 FormData 对象。

## 如何访问 FormData 对象中的数据？

FormData 对象允许我们直接通过 get()方法检索值。您还可以通过相应的方法追加或删除值。还可以用 set()方法为一个键设置一个新值。

最后，还可以通过遍历 formDate.entries()或使用 for…of 循环来遍历键值对。

## 如何基于表单数据创建 URL 查询参数？

如果你想把表单数据转换成一组查询参数，这很容易做到。您可以将 FormData 对象直接传递到 URLSearchParams 中。

## 如何使用 Fetch API 发布表单数据

FormData 对象可以很容易地与 Fetch API 一起使用。您可以简单地将对象作为请求的主体进行传递。

## 如何使用 FormData 事件

每当为窗体创建 FormData 对象时，都会针对该窗体调度一个事件。我们可以监听这个事件，并将一些逻辑绑定到它，例如将表单数据提交给一个 API 端点。

在下面的例子中，我们在提交表单时创建了一个 FormData 对象。我们侦听 FormData 事件并提交数据。这让我们可以自由地创建表单数据，而不仅仅是提交表单数据。

## 额外资源

*   [MDN 表单数据](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
*   [MDN URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
*   [表单数据浏览器支持](https://caniuse.com/mdn-api_formdata)
*   [MDN 表单数据事件](https://developer.mozilla.org/en-US/docs/Web/API/FormDataEvent)

## 结论

FormData 对象在处理表单数据、获取请求和 url 参数处理时非常有用。它的浏览器支持是全面绿色的，没有理由不利用这个 API。

感谢阅读。如果你对此有想法，一定要留下评论。

如果你喜欢我的内容，并想支持我的努力，考虑通过[我的会员链接](https://medium.com/@WesleySmits/membership)成为一个媒体订阅者。这不会花费你任何额外的费用，但 Medium 会把部分收益给我，让我推荐你。

如果你愿意，你可以在 [LinkedIn](https://www.linkedin.com/in/wesley-robert-smits/) 或 [Twitter](https://twitter.com/iamwesleysmits) 上联系我！

[](https://medium.com/@WesleySmits/membership) [## 通过我的推荐链接加入 Medium-Wesley Smits

### 阅读韦斯利·斯密特(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

medium.com](https://medium.com/@WesleySmits/membership) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。**