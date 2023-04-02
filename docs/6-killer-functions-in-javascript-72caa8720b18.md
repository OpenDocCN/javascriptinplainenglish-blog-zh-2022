# JavaScript 中的 6 个黑仔函数

> 原文：<https://javascript.plainenglish.io/6-killer-functions-in-javascript-72caa8720b18?source=collection_archive---------9----------------------->

## 你应该知道的简单的 JavaScript 魔术

![](img/ae0f885d8b359e31f47ede9b020e0d08.png)

Photo by [KMA .img](https://unsplash.com/@kmaimg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript，正如我通常所说的，充满了惊喜。它从未停止让我们震惊。每天，我都会在这种编程语言中获得一项新技能。一些小问题，但对你的代码有重大影响。是值得分享的东西。

在本文中，我将向您展示可以在日常开发中使用的六个 JavaScript 函数。所以让我们继续学习新的东西吧！

## 1.检查元素在视口中是否可见

IntersectionObserver 是检查一个元素在视窗中是否可见的好方法。

```
const callback = (entries) => {
    entries.forEach((entry) => {
        if (entry.isIntersecting) {
            // 'entry.target' is the DOM element
            console.log(`${entry.target.id} is visible.`);
        }
    });
};const options = {
    threshold: 1.0,
};const observer = new IntersectionObserver(callback, options);
const btn = document.getElementById("btn");
const bottomBtn = document.getElementById("bottom-btn");observer.observe(btn);
observer.observe(bottomBtn);
```

您可以使用`option`参数自定义观察器的行为。`threshold`是最有用的属性，它定义了观察点触发时需要在视口中可见的元素的百分比。

有关 IntersectionObserver 的更多信息，请单击此处的。

## 2.检测设备

您可以使用`navigator.userAgent`获得细微的洞察力，并检测运行该应用程序的设备。

```
const detectDeviceType = () =>
    /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)
        ? "Mobile"
        : "Desktop";console.log(detectDeviceType());
```

> 不建议使用这种方法，因为它取决于浏览器的当前版本。任何浏览器的未来版本都可能会删除对此方法的支持。所以使用它时一定要小心，并且只适用于当前和以前版本的浏览器。

**你可以在这里** **阅读更多关于** `**navigator.userAgent**` [**。**](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)

## 3.隐藏元素

你可以使用`style.visibility`属性切换一个元素的可见性，如果你想从渲染流中移除它，你可以使用`style.display`属性。

```
const hideElement = (element, removeFromFlow = false) => {
    removeFromFlow
        ? (element.style.display = "none")
        : (element.style.visibility = "hidden");
};
```

> 如果不从渲染流中移除元素，它将被隐藏，但其空间仍将被占用。

这在渲染长元素列表时非常有用，不在视图中的元素(可以使用`IntersectionObserver`进行测试)可以被隐藏以提高性能。

## 4.从 URL 获取参数

JavaScript 使得使用 URL 对象从任何地址获取参数变得轻而易举。

```
const url = new URL(window.location.href);
const paramValue = url.searchParams.get("paramName");
console.log(paramValue);
```

## 5.轻松深层复制对象

您可以通过将任何对象转换为字符串并转换回对象来对其进行深度复制。这不仅适用于对象，也适用于其他复合数据类型，比如数组。

```
const deepCopy = (obj) => JSON.parse(JSON.stringify(obj));
```

**此处阅读**[](https://www.geeksforgeeks.org/what-is-shallow-copy-and-deep-copy-in-javascript/)****详细讲述深、浅抄。****

## **6.等待功能**

**JavaScript 确实附带了一个`setTimeout`函数，但是它不返回一个`Promise`对象，这使得它很难在`async`函数中使用。所以我们要自己写**等待/睡眠**函数。**

```
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));const asyncFunc = async () => {
    await wait(1000);
    console.log("async");
};asyncFunc();
```

**这就是这篇文章的内容。我希望你今天学到了一些新东西。您可以在[媒体](https://gouravkajal.medium.com/membership)上[关注我](https://gouravkajal.medium.com/)或者在 [LinkedIn](https://www.linkedin.com/in/gouravkajal/) 上与我联系。想看更多这样的文章，敬请期待！**

**感谢阅读！**

***更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***