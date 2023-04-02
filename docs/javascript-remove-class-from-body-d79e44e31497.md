# 如何使用 JavaScript 从 Body 元素中移除一个类

> 原文：<https://javascript.plainenglish.io/javascript-remove-class-from-body-d79e44e31497?source=collection_archive---------17----------------------->

## 了解如何使用 JavaScript 轻松地从 HTML 文档的 body 元素中移除一个类。

![](img/90b7b61b38811d53732062f6693ca56c.png)

在本文中，我们将了解如何使用 JavaScript 轻松地从 HTML 文档的 body 元素中移除一个类。

# DOMTokenList remove()方法

要从 body 元素中移除一个类，调用`body`元素上的`classList.remove()`方法，例如`document.body.classList.remove('the-class)'`。

以下是一些 HTML 示例:

**index.html**

```
<!DOCTYPE html>
<html>
  <head>
    <title>Coding Beauty Tutorial</title>
  </head>
  <body class="class-1 class-2">
    <div>This is a div element.</div> <script src="index.js"></script>
  </body>
</html>
```

下面是我们如何使用 JavaScript 从主体中移除类`class-1`:

**索引. js**

```
document.body.classList.remove('class-1');
```

我们使用`document`的`body`属性来访问表示文档主体的`HTMLElement`对象。

属性返回一个代表元素拥有的类列表的对象。

`classList`属性的 [remove()](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList/remove) 方法获取一个类列表，并将它们从元素中移除。

移除`class-1`后，文档标记将如下所示:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Coding Beauty Tutorial</title>
  </head>
  <body class="class-2">
    <div>This is a div element.</div> <script src="index.js"></script>
  </body>
</html>
```

我们可以向`remove()`方法传递多个参数来从主体中移除多个类。例如，我们可以使用一条语句将`class-1`和`class-2`从主体中删除:

**index.js**

```
document.body.classList.remove('class-1', 'class-2');
```

这将是生成的文档标记:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Coding Beauty Tutorial</title>
  </head>
  <body>
    <div>This is a div element.</div> <script src="index.js"></script>
  </body>
</html>
```

如果我们传递一个元素没有的类，`remove()`忽略这个类并且不抛出错误。

# 如何向 Body 元素添加一个类

要向 body 元素添加一个类，我们可以使用 body 对象的`classList.add()`方法。

**index.js**

```
document.body.classList.add('class-3', 'class-4');
```

`classList`属性的 [add()](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList/add) 方法获取一个类名列表并将它们添加到一个元素中。

这将是添加两个类后得到的 HTML:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Coding Beauty Tutorial</title>
  </head>
  <body class="class-1 class-2 class-3 class-4">
    <div>This is a div element.</div> <script src="index.js"></script>
  </body>
</html>
```

`add()`防止同一个类被多次添加到一个元素中，因此如果该元素已经有一个指定的类，则忽略它。

*更新于:*[*codingbeautydev.com*](https://cbdev.link/79f2c0)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。