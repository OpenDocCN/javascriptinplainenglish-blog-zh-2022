# 如何在 JavaScript 中从平面数组构建树形数组

> 原文：<https://javascript.plainenglish.io/how-to-build-a-tree-array-from-flat-array-in-javascript-8d0414ac1190?source=collection_archive---------2----------------------->

## 一个关于如何用 JavaScript 从一个扁平数组构建一个树形数组的教程。

![](img/169f922507b4e1ef61abde2f02061acc.png)

Photo by [trevor pye](https://unsplash.com/@trevmepix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想在 JavaScript 中从一个展平的数组构建一个树形数组。

在本文中，我们将研究如何用 JavaScript 从扁平数组构建树形数组。

# 使用 JavaScript 数组方法和递归

我们可以很容易地用各种数组方法和递归从一个扁平数组构建一个树形数组。

例如，我们可以写:

```
const comments = [{
  id: 1,
  parentId: null
}, {
  id: 2,
  parentId: 1
}, {
  id: 3,
  parentId: 1
}, {
  id: 4,
  parentId: 2
}, {
  id: 5,
  parentId: 4
}];const nest = (items, id = null, link = 'parentId') =>
  items
  .filter(item => item[link] === id)
  .map(item => ({
    ...item,
    children: nest(items, item.id)
  }));console.log(nest(comments))
```

我们有带有`id`和`parentId`属性的`comments`数组，其中`parentId`是父注释的`id`。

然后，我们创建接受`items`数组、`id`和`link`的`nest`函数。

`id`是`parentId`的值。

并且`link`具有父 ID 的属性名。

在该函数中，我们调用`filter`来获取具有给定 ID 的子注释。

然后调用`map`来映射带有`children`数组属性的`item`和我们从`nest`方法中得到的子注释。

因此，控制台日志应该记录:

```
[
  {
    "id": 1,
    "parentId": null,
    "children": [
      {
        "id": 2,
        "parentId": 1,
        "children": [
          {
            "id": 4,
            "parentId": 2,
            "children": [
              {
                "id": 5,
                "parentId": 4,
                "children": []
              }
            ]
          }
        ]
      },
      {
        "id": 3,
        "parentId": 1,
        "children": []
      }
    ]
  }
]
```

# 结论

我们可以用一些数组方法和 JavaScript 的递归来取消一个数组的扁平并返回一个树形数组。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)**和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**