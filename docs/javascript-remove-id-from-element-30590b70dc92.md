# 如何用 JavaScript 从元素中移除 ID 属性

> 原文：<https://javascript.plainenglish.io/javascript-remove-id-from-element-30590b70dc92?source=collection_archive---------6----------------------->

## 了解如何使用 JavaScript 轻松地从 DOM 元素中移除 ID 属性。

![](img/9789a84eba38db7538e7fd6417509f5c.png)

在本文中，我们将学习如何使用 JavaScript 删除 DOM 元素的 ID 属性。

# 元素的 removeAttribute()方法

要从元素中移除 ID 属性，调用元素上的`removeAttribute()`方法，将字符串`'id'`作为参数传递。

## 例子

**index.html**

```
<!DOCTYPE html>
<html>
  <head>
    <title>
      Removing the ID Attribute from an Element with
      JavaScript
    </title>
  </head>
  <body>
    <div class="box" id="box-1">This is a box</div> <script src="index.js"></script>
  </body>
</html>
```

下面是我们如何从我们创建的`div`元素中删除 ID:

**index.js**

```
const box = document.getElementById('box-1');console.log(box.getAttribute('id')); // box-1box.removeAttribute('id');console.log(box.getAttribute('id')); // null
```

[Element remove attribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute)方法删除指定名称元素的属性。

**注意**:如果指定的属性不存在，`removeAttribute()`不会抛出错误，而是返回。

# 元素的 setAttribute()方法

如果你想替换元素的 ID 而不是删除它，你可以使用`setAttribute()`方法。

例如，我们可以将之前创建的`div`元素的 ID 更改为一个新值。

## 例子

**index.js**

```
const box = document.getElementById('box-1');console.log(box.getAttribute('id')); // box-1box.setAttribute('id', 'new-id');console.log(box.getAttribute('id')); // new-id
```

元素 setAttribute() 方法有两个参数:

1.  `name`:指定要设置其值的属性的名称的字符串。
2.  `value`:包含要分配给属性的值的字符串。

我们分别传递`'id'`和新的 id 作为第一个和第二个参数，来设置 ID 属性。

**注意:**如果元素上已经存在属性，则更新值。否则，将添加一个具有指定名称和值的新属性。

# Element getAttribute()方法

在本文中，我们已经多次使用了 [getAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute) 方法。在一个`Element`上调用这个方法会返回具有指定名称的属性值。所以我们用`'id'`调用它来获取元素的 ID。

**注意:**如果元素上不存在该属性，`getAttribute()`将返回`null`或空字符串(`''`)，具体取决于浏览器。

*更新于:*[*【codingbeautydev.com】*](https://cbdev.link/f10ff6)

您可以在哪里找到我们:

🌐[网站](https://cbdev.link/b621b9) |🌟[推特](https://twitter.com/CodingBeautyDev)🌟[脸书](http://facebook.com/CodingBeautyDev)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。