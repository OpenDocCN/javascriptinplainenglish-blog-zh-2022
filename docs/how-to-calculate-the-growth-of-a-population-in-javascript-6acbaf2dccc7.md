# 如何使用 JavaScript 计算人口增长

> 原文：<https://javascript.plainenglish.io/how-to-calculate-the-growth-of-a-population-in-javascript-6acbaf2dccc7?source=collection_archive---------7----------------------->

## 毁灭 2022

## 或者如何使用递归函数来代替循环

![](img/fe54425c02330ebcfb1fc40ef40d34da.png)

今天的问题是关于计算百分比、人口和数列趋势。或者简单的说，如何对一个小镇的人口增长做一个简单的预测？

# 问题是:人口的增长

链接到[形](https://www.codewars.com/kata/563b662a59afc2b5120000c6)

![](img/8d7c436b48ad84a3d3237cda71ef4d13.png)

在一个小镇上，人口在一年的开始时是。人口每年有规律地增长，而且每年都有新的居民来到这个城镇居住。这个城镇需要多少年才能看到它的人口超过或等于`p = 1200`居民？

```
At the end of the first year there will be:
1000 + 1000 * 0.02 + 50 => 1070 inhabitants

At the end of the 2nd year there will be:
1070 + 1070 * 0.02 + 50 => 1141 inhabitants

At the end of the 3rd year there will be:
1141 + 1141 * 0.02 + 50 => 1213

It will need 3 entire years.
```

更一般的给定参数:

```
p0, percent, aug (inhabitants coming or leaving each year), p (population to equal or surpass)
```

函数`nb_year`应该返回使人口大于或等于`p`所需的整年数`n`。

`aug`为整数，`percent`为正数或空浮点数，`p0`和`p`为正整数(`> 0`)

```
// Examples:
nb_year(1500, 5, 100, 5000); // 15
nb_year(1500000, 2.5, 10000, 2000000); // 10
```

# 我的解决方案

![](img/d22445e861f24b47b6edeed2fbf8497a.png)

我决定用两种方法解决这个问题。第一个解决方案是最简单的。这是一个`while`循环，它将迭代直到满足条件。条件是人口大于或等于目标人口。

```
export const nbYear = (
  p0: number,
  percent: number,
  aug: number,
  p: number
): number => {
  let pop = p0;
  let perc = percent / 100;
  let year = 0;
  while (pop < p) {
    pop = pop + pop * perc + aug;
    pop = Math.trunc(pop);
    ++year;
  }
  return year;
};
```

最难的一点是把问题理解好。既然说的是人口，数字就必须是整数。写 0.25 居民没有意义。为此，我必须使用 Math.trunc()方法来截断预期人口的数量。

我可以把同样的函数写得更简洁一点。

```
function nbYear(p0, percent, aug, p) {
  let year = 0;
  while (p0 < p) {
    p0 = Math.trunc(p0 + (p0 * percent) / 100 + aug);
    ++year;
  }
  return year;
}
```

## 复杂溶液

![](img/13245ddc46930951e5fb284636614445.png)

第二个解决方案稍微复杂一点。这是一个递归函数，它会调用自己，直到满足条件。条件是人口大于或等于目标人口。

```
export const nbYear = (
  p0: number,
  percent: number,
  aug: number,
  p: number
): number => {
  if (p0 >= p) return 0;
  return (
    1 + nbYear(Math.trunc(p0 + p0 * (percent / 100) + aug), percent, aug, p)
  );
};
```

我可以试着把这个函数一分为二，让它更清晰一点。新版本看起来像这样

```
const calculatePop = (p0, percent, aug, p) =>
  Math.trunc(p0 + p0 * (percent / 100) + aug);

function nbYear(p0, percent, aug, p) {
  const annualCount = calculatePop(p0, percent, aug, p);

  if (annualCount >= p) return 1;

  return 1 + nbYear(annualCount, percent, aug, p);
}
```

# 结论

今天的问题很简单。我决定用两种方法解决。第一个是最简单的，第二个稍微复杂一点。我希望你喜欢它。下一题明天见。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***