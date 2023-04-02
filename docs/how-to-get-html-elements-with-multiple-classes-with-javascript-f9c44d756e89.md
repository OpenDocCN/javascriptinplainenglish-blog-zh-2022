# 如何用 JavaScript 获取带有多个类的 HTML 元素

> 原文：<https://javascript.plainenglish.io/how-to-get-html-elements-with-multiple-classes-with-javascript-f9c44d756e89?source=collection_archive---------2----------------------->

## 一个关于如何用 JavaScript 获得多个类的 HTML 元素的教程。

![](img/25236611419de9ac8723166f14d468e4.png)

Photo by [Feliphe Schiarolli](https://unsplash.com/@flpschi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 获得多个类的多个元素。

在本文中，我们将看看如何用 JavaScript 获得带有多个类的 HTML 元素。

# 用这两个类获取 HTML 元素

要用这两个类获取 HTML 元素，我们可以使用`getElementsByClassName`或`querySelectorAll`方法。

例如，如果我们有下面的 HTML:

```
<div class='class1'>
  foo
</div>
<div class='class2'>
  bar
</div>
<div class='class1 class2'>
  baz
</div>
```

然后，我们可以通过编写以下内容获得带有文本“baz”的 div:

```
const list1 = document.getElementsByClassName("class1 class2");
const list2 = document.querySelectorAll(".class1.class2");
console.log(list1)
console.log(list2)
```

我们用`'class1 class2'`调用`getElementsByClassName`,以获得同时存在`class1`和`class2`的 div。

同样，我们可以通过使用`“.class1.class2”` CSS 选择器对`querySelectorAll`做同样的事情。

然后`list1`是第 3 个 div 的 HTMLCollection。

并且`list2`是具有第三个 div 的节点列表。

# 获取至少包含一个类的 HTML 元素

我们可以通过使用`querySelector`方法获得至少包含一个类的 HTML 元素。

例如，如果我们有下面的 HTML:

```
<div class='class1'>
  foo
</div>
<div class='class2'>
  bar
</div>
<div class='class1 class2'>
  baz
</div>
```

然后我们可以写:

```
const list = document.querySelectorAll(".class1,.class2");
console.log(list)
```

我们使用带有`querySelectorAll`的`“.class1,.class2”`来获取带有`class1`或`class2`或两者都作为类的元素。

因此`list`是一个包含所有 3 个元素的节点列表。

# 用一个类而不是两个类获取 HTML 元素

我们也可以使用`querySelector`用一个类而不是两个类来获取 HTML 元素。

例如，如果我们有下面的 HTML:

```
<div class='class1'>
  foo
</div>
<div class='class2'>
  bar
</div>
<div class='class1 class2'>
  baz
</div>
```

然后我们写道:

```
const list = document.querySelectorAll(".class1:not(.class2),.class2:not(.class1)");
console.log(list)
```

我们使用`:not`伪选择器来排除带有`class1`的`class2`和带有`class2`的`class1`。

所以`list`是一个包含前两个 div 的节点列表。

# 获取没有类或只有一个类的 HTML 元素

为了获得所有元素，而不应用任何类或者只应用一个类，我们可以再次使用`:not`伪选择器。

例如，如果我们有下面的 HTML:

```
<div class='class1'>
  foo
</div>
<div class='class2'>
  bar
</div>
<div class='class1 class2'>
  baz
</div>
```

然后我们可以写:

```
const list = document.querySelectorAll(":not(.class1),:not(.class2)");
console.log(list)
```

我们得到了页面中的所有元素，除了带有文本 baz 的 div。

# 获取不包含任何类的 HTML 元素

为了获得不包含任何类的 HTML 元素，我们可以再次使用`:not`伪选择器。

例如，如果我们有下面的 HTML:

```
<div class='class1'>
  foo
</div>
<div class='class2'>
  bar
</div>
<div class='class1 class2'>
  baz
</div>
```

然后我们可以写:

```
const list = document.querySelectorAll(":not(.class1):not(.class2)");
console.log(list)
```

用`class1`或`class2`选择除 div 以外的任何内容。

# 结论

我们可以使用`querySelector`来选择一个元素，将任何类的组合应用到我们想要的元素上。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *。**