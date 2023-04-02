# 如何在 JavaScript 中得到两个日期的月差？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-difference-in-months-between-two-dates-in-javascript-85c9b5acfd5c?source=collection_archive---------3----------------------->

![](img/6e4c1f3b1fe0d607e948a0cd6a55801e.png)

Photo by [niko photos](https://unsplash.com/@niko_photos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在 JavaScript 代码中得到两个日期之间的月差。

在这篇文章中，我们将看看如何用 JavaScript 获得月份中两个日期之间的差异。

# 获取两个日期之间的月份差异

我们可以计算两个日期之间的月差，然后根据年差得到月差。

然后，我们将年差乘以 12，将其转换为月。

然后我们从开始日期减去月份。

然后我们加上结束日期的月份。

为此，我们写道:

```
const monthDiff = (d1, d2) => {
  let months;
  months = (d2.getFullYear() - d1.getFullYear()) * 12;
  months -= d1.getMonth();
  months += d2.getMonth();
  return months <= 0 ? 0 : months;
}const start = new Date(2020, 1, 1)
const end = new Date(2020, 5, 1)
console.log(monthDiff(start, end))
```

我们首先获得年份差异，并将其转换为月份:

```
months = (d2.getFullYear() - d1.getFullYear()) * 12;
```

然后我们用以下公式减去`d1`的月份:

```
months -= d1.getMonth();
```

然后我们将从`d2`开始的月份加上:

```
months += d2.getMonth();
```

如果它大于 0，我们就返回`months`。

否则，我们返回 0。

因此，控制台日志应该记录 4，因为这两个日期相差 4 个月。

# 结论

我们可以通过获得年份差异，将其转换为月份来获得这两个日期之间的差异。

然后我们可以从开始日期中减去月数。

并将结束日期后的月份相加，以消除重复计算。