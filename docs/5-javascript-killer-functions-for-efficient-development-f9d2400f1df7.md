# 5 个用于高效开发的黑仔 JavaScript 函数

> 原文：<https://javascript.plainenglish.io/5-javascript-killer-functions-for-efficient-development-f9d2400f1df7?source=collection_archive---------2----------------------->

## 使用这些杀手级的 JavaScript 函数来加速你的开发过程。

![](img/44755bf04db8b61a12d9255daad647ab.png)

Photo by [Juanjo Jaramillo](https://unsplash.com/@juanjodev02?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 Web 开发最关键的部分，加快 JS 开发意味着加快下班时间。

本文包含没有任何副作用的代码片段，可以安全地复制和使用。

# 1.验证元素是否在可见区域内

当开发网页时，通常需要知道元素是否在视口中，即用户是否能看到它。这可以通过使用**intersect observer**API 来完成。

```
const callback = (entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      // `entry.target` 是 dom 元素
      console.log(`${entry.target.id} is visible`);
    }
  });
};const options = {
  threshold: 1.0,
};const observer = new IntersectionObserver(callback, options);const btn = document.getElementById( btn );
const bottomBtn = document.getElementById( bottom-btn );observer.observe(btn);
observer.observe(bottomBtn);
```

**选项**参数定制观察者的行为。threshold 属性通常用于定义当观察者被触发时需要在可见区域中可见的元素的百分比。

# 2.识别设备

我们通常使用 window.navigator.userAgent 来获取当前设备的详细信息进行识别

```
onst detectDeviceType = () =>
  /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
    navigator.userAgent
  )
    ?  Mobile 
    :  Desktop ;console.log(detectDeviceType());
```

# 3.隐藏元素

CSS 有两种隐藏元素的常用方法。

1.  可以使用 style.visibility 切换元素的可见性。
2.  如果要从整个呈现流中移除元素，请使用 style.display 属性。

```
const hideElement = (element, removeFromFlow = false) => {
  removeFromFlow
    ? (element.style.display =  none )
    : (element.style.visibility =  hidden );
};
```

如果您不从渲染流中移除元素，而只是隐藏可见性，这些元素仍将被绘制并占用视图空间。

在呈现长列表时，使用 style.display 属性隐藏不在可见区域中的元素，与上面的 IntersectionObserver API 结合使用，可以大大提高呈现性能。

# 4.获取 URL 上的查询参数

建议使用 URL 对象。URL 接口用于解析、构造、规范化和编码 URL，并且很容易获得链接上的查询参数。

```
const url = new URL(window.location.href);
const paramValue = url.searchParams.get( paramName );
console.log(paramValue);
```

# 5.简单深层拷贝

```
const deepCopy = (obj) => JSON.parse(JSON.stringify(obj));
```

现在你知道了。感谢您的阅读。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*