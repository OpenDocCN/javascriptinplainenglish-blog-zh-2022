# 如何用 classList 在一条指令中添加或删除几个类？

> 原文：<https://javascript.plainenglish.io/how-to-add-or-remove-several-classes-in-one-single-instruction-with-classlist-b280adbb3937?source=collection_archive---------14----------------------->

## 关于如何用`classList`在一条指令中添加或删除几个类的指南。

![](img/b5f7d7de4ad3266b2e1eb087f8416a0e.png)

Photo by [Emma Matthews Digital Content Production](https://unsplash.com/@emmamatthews?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用`classList` API 在一条指令中添加或删除几个类。

在本文中，我们将看看如何用`classList`在一条指令中添加或删除几个类。

# 用 classList 在一条指令中添加或删除几个类

`add`方法接受一个或多个类名字符串。

因此，我们可以使用它一次添加多个类。

例如，如果我们有下面的 HTML:

```
<div></div>
```

然后，我们可以通过编写以下代码来添加多个类:

```
const div = document.querySelector('div')
div.classList.add("first", "second", "third");
```

如果我们有一个数组，那么我们可以将条目作为参数分布:

```
const div = document.querySelector('div')
const list = ['first', 'second', 'third'];
div.classList.add(...list);
```

我们可以用`apply`来代替扩展操作符:

```
const div = document.querySelector('div')
const list = ['first', 'second', 'third'];
div.classList.add.apply(
  div.classList,
  list
);
```

# 设置类名属性

我们还可以将`className`属性设置为包含多个类的字符串，每个类之间用空格隔开。

例如，我们可以写:

```
const div = document.querySelector('div')
const list = ['first', 'second', 'third'];
div.className += list.join(' ');
```

做同样的事情。

现有的类将被覆盖。

# 结论

我们可以使用`classList.add`方法或者设置`className`属性来为一个元素添加多个类名。

现在你知道了。感谢您的阅读。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****