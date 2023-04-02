# 如何使用 JavaScript 以编程方式设置 Select 元素的值？

> 原文：<https://javascript.plainenglish.io/how-to-programmatically-set-the-value-of-a-select-element-using-javascript-f152fad36452?source=collection_archive---------9----------------------->

![](img/8aa93364397bbbc2bcd868451da047c3.png)

Photo by [Jen Theodore](https://unsplash.com/@jentheodore?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望用 JavaScript 以编程方式设置 select 元素的值。

在本文中，我们将了解如何用 JavaScript 以编程方式设置 select 元素的值。

# 设置值属性

设置选择元素值的一种方法是设置选择元素的`value`属性的值。

例如，我们可以编写以下 HTML:

```
<select>
  <option value="apple">Apple</option>
  <option value="orange">Orange</option>
  <option value="grape">Grape</option>
</select>
```

用选项创建 select 元素。

然后，我们可以通过编写以下代码，在用 JavaScript 选择 select 元素后设置它的`value`属性:

```
const select = document.querySelector('select')
select.value = 'orange'
```

我们使用`querySelector`来获取选择元素。

然后，我们只需将`value`属性设置为选项元素的`value`属性的值，我们希望选取该元素来选择一个值。

因此，当我们加载页面时，应该会看到从下拉列表中选择了橙色。

# 将选项元素的 selected 属性设置为 true

我们还可以将选项元素的`selected`属性设置为`true`来设置下拉列表中的选项。

为此，我们编写以下 HTML:

```
<select>
  <option value="apple">Apple</option>
  <option value="orange">Orange</option>
  <option value="grape">Grape</option>
</select>
```

然后，我们可以使用`options`属性获取选项，并通过编写以下内容来设置选项的`selected`属性:

```
const select = document.querySelector('select')
select.options[1].selected = true
```

`select.options`有选项。

我们可以通过索引来访问选择。

然后我们调用设置它的`selected`属性为`true`来选择它。

因为橙色是第二选项，所以它的索引为 1。

因此橙色被设置为下拉列表中的选定选项。

# 结论

我们可以通过设置选项的`selected`属性，以编程方式设置下拉菜单的选择。

或者我们可以将 select 元素的`value`属性设置为我们想要的 option 元素的`value`属性的值。

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*