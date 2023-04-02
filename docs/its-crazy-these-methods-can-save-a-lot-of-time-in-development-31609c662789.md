# 这太疯狂了:这些方法可以节省大量开发时间

> 原文：<https://javascript.plainenglish.io/its-crazy-these-methods-can-save-a-lot-of-time-in-development-31609c662789?source=collection_archive---------7----------------------->

![](img/bf86dadb876f1e361fb02a3e7c2b6035.png)

**1。你知道吗？也可以使用逐位运算进行舍入运算**

```
var y = 3.45 | 0; // 3
```

**解释:因为位运算只支持 32 位整数，所以所有小数点都被丢弃。**

**2。判断代码是否压缩，还可以这么做:**

```
function CustomFn() {}const isCrashed = typeof CustomFn.name === ‘string’ && CustomFn.name === ‘CustomFn’;
```

**3。你认为** `**clearTimeout**` **和** `**clearInterval**` **可以互换使用吗？当然，大部分浏览器都支持相互清理定时器，但是建议使用相应的清理功能。**

```
var timeout = setTimeout(() => console.log(1), 1000);var interval = setInterval(() => console.log(2), 800);clearInterval(timeout);clearTimeout(interval);
```

**4。除了 slice 还有其他清空数组的方法吗？**

```
const arr = [4, 5, 6];console.log(arr); // [4, 5, 6]arr.length = 0;console.log(arr); // []
```

**不管引用的数组是什么，重新分配一个新的空数组也是一个不错的选择。**

**5。一个有趣的问题:+0 和-0 有区别吗？答案是肯定的，有区别。**

```
1/+0 === Infinity1/-0 === -Infinity
```

就这些，谢谢。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*