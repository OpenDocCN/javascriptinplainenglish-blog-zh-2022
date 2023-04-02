# 如何用 JavaScript 在 select 元素中检索选中的 option 元素的文本？

> 原文：<https://javascript.plainenglish.io/how-to-retrieve-the-text-of-the-selected-option-element-in-a-select-element-with-javascript-6933e5d4457d?source=collection_archive---------2----------------------->

![](img/e70ab39baf0a921bb69b2b2e7fc3ad72.png)

Photo by [Wolfgang Hasselmann](https://unsplash.com/@wolfgang_hasselmann?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 在 select 元素中检索所选 option 元素的文本。

在本文中，我们将研究如何用 JavaScript 在 select 元素中检索所选选项元素的文本。

# 使用 selectedIndex 属性

我们可以用`selectedIndex`属性得到选中条目的索引。

然后我们可以使用`text`属性来获取所选项的文本。

例如，如果我们有下面的 HTML:

```
<select>
  <option value="1">apple</option>
  <option value="2" selected>orange</option>
</select>
```

然后，我们可以编写以下 JavaScript 代码，从 select 元素中获取选定的项目:

```
const getSelectedText = (el) => {
  if (el.selectedIndex === -1) {
    return null;
  }
  return el.options[el.selectedIndex].text;
}const select = document.querySelector('select')
const text = getSelectedText(select);
console.log(text)
```

我们创建了`getSelectedText`函数，它将一个元素作为参数。

然后我们检查`selectedIndex`是否为-1。

如果它是-1，那么没有选择任何东西，我们返回`null`。

否则，我们用`el.options`得到选项。

然后，我们通过将`el.selectedIndex`传递到方括号中来获得选中的选项。

最后，我们获取`text`属性来获取所选选项元素的文本。

因此，控制台日志应该记录`'orange'`。

# 结论

我们可以用`selectedIndex`和`text`属性检索所选选项元素的文本。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***