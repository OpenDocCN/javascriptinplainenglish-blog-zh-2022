# 5 个常用的 JavaScript 高阶函数以及何时使用它们

> 原文：<https://javascript.plainenglish.io/5-lines-to-understand-5-commonly-used-javascript-higher-order-function-58085fc28a2a?source=collection_archive---------16----------------------->

## 用门外汉的术语理解这些方法映射、归约、过滤、一些和每个做什么，以及何时使用它们。

![](img/ff6a9a385559fb8dd14cc5ecb5ca5e8d.png)

Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

所以在做代码审查的时候，我经常发现开发人员使用 JavaScript 函数，比如 map，reduce，filter，some，每一个都可以互换来迭代数组。

在核心中，这些方法中的每一个都在数组上迭代，但是函数在迭代过程中所做的事情使得一个函数与另一个函数不同。

因此，今天我们将仔细研究每一种方法，并试图用外行人的术语来理解每种方法的作用以及何时使用。

出于我们的目的，我创建了一个简单的数组，我们将在上面进行操作。

```
let arr = [1, 2, 3, 4, 5];
```

1.  **map** :当要修改数组的每个元素时使用。

```
let mappedArr = arr.map((elem) => {return elem * 2;});console.log(mappedArr); // [ 2, 4, 6, 8, 10 ]
```

所以，正如你在这个例子中看到的，我们希望每个元素都是初始数组中值的两倍，所以使用了 map。

2.**化简**:用于将一个数组化简为单个值。

```
let reducedArr = arr.reduce((acc, elem) => {return acc + elem;}, 0);console.log(reducedArr); // 15
```

正如您在上面的例子中所看到的，我们为 reduce 方法提供了一个初始值(这里是零)，然后将每个元素添加到这个值中，得到所有元素的总和。

3. **filter** :该方法用于接收根据一定条件过滤出来的新数组。

```
let filteredArr = arr.filter((elem) => {return elem % 2 === 0;});console.log(filteredArr);
```

根据上面的例子，我们只需要列表中的偶数，也就是说，我们需要一个基于特定条件的过滤列表，所以我们使用了一个过滤器。

4. **some:** 这个函数根据函数中提供的条件返回一个布尔值。顾名思义，即使其中一个条件为 true，它也返回 true。

```
let someArr = arr.some((elem) => {return elem % 2 === 0;});console.log(someArr); // true
```

这里我们使用一些函数来检查数组中的元素是否是偶数。

5. **every:** 顾名思义，与一些函数所做的相反，只有当所有元素都满足函数中提供的特定条件时，每个函数才会返回 true。

```
let everyArr = arr.every((elem) => {return elem % 2 === 0;});console.log(everyArr); // false
```

在这里，由于一些元素是奇数，一些是偶数，我们在这里得到假。

所以，这些都是上述功能的简单用法，希望你能弄清楚什么时候使用。

尽管如此，如果有任何困惑。请在评论区告诉我，如果你想让我写任何特定的话题，你也可以提出建议。🍺

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*