# 如何用 JavaScript 获取选中复选框的值？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-value-of-a-checked-checkbox-with-javascript-31a4a9c572da?source=collection_archive---------2----------------------->

![](img/55bafa9bb991dde13b6b5de3072413d8.png)

Photo by [Kamil Kalkan](https://unsplash.com/@kamilklkn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在我们的 web 应用程序中获得选中复选框的值。

在本文中，我们将看看如何用 JavaScript 获取被选中的复选框的值。

# 获取所有选中的复选框

我们可以使用普通的 JavaScript 来获得所有选中的复选框。

例如，如果我们有以下复选框:

```
<input type="checkbox" value="1" name="mailId[]" checked>1
<input type="checkbox" value="2" name="mailId[]" checked>2
<input type="checkbox" value="3" name="mailId[]">3
```

然后，我们可以选择所有选中的复选框，并使用以下命令获取它们的值:

```
const checked = document.querySelectorAll('input[type="checkbox"]:checked');
console.log([...checked].map(c => c.value))
```

我们添加了`:checked`伪选择器来选择所有选中的复选框。

前两个复选框有`checked`属性，所以我们应该用它获得前两个复选框的值。

然后我们记录下`value`的财产。

我们将`checked`节点列表扩展到一个数组中。

然后我们调用`map`,通过回调返回每个被选中的复选框的`value`属性。

因此，控制台日志应该记录`[“1”, “2”]`。

# 结论

我们可以用普通的 JavaScript 获得所有选中复选框的值。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***