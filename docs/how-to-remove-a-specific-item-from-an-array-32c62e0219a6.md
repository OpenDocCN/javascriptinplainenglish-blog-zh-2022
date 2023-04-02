# 如何从数组中移除特定的项

> 原文：<https://javascript.plainenglish.io/how-to-remove-a-specific-item-from-an-array-32c62e0219a6?source=collection_archive---------16----------------------->

![](img/8acf8657597a45ab92ffe8d0872b6fa2.png)

Photo by [Iker Urteaga](https://unsplash.com/@iurte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有几种方法可以从数组中删除特定的项目:

1.  您可以使用`splice()`方法从特定索引中删除一个项目。例如:

```
let arr = [1, 2, 3, 4, 5];
arr.splice(2, 1); // removes the item at index 2 (3)
console.log(arr); // [1, 2, 4, 5]
```

2.您可以使用`filter()`方法根据条件删除一个项目。例如:

```
let arr = [1, 2, 3, 4, 5];
arr = arr.filter(item => item !== 3); // removes all items that are not equal to 3
console.log(arr); // [1, 2, 4, 5]
```

3.你可以使用`indexOf()`方法找到你想要移除的项目的索引，然后使用`splice()`方法移除它。例如:

```
let arr = [1, 2, 3, 4, 5];
let index = arr.indexOf(3);
if (index > -1) {
  arr.splice(index, 1);
}
console.log(arr); // [1, 2, 4, 5]
```

4.您可以使用`delete`操作符从数组中删除一个项目，但是它会在原来的位置留下一个`undefined`值。例如:

```
let arr = [1, 2, 3, 4, 5];
delete arr[2]; // removes the item at index 2 (3)
console.log(arr); // [1, 2, undefined, 4, 5]
```

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

## **想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。**