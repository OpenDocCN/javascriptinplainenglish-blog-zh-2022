# 如何在 JavaScript 中找到尽可能高的数字

> 原文：<https://javascript.plainenglish.io/how-to-find-the-highest-possible-number-in-javascript-3cfd505f905f?source=collection_archive---------14----------------------->

## 毁灭 2022

## 或者关于数组、字符串和排序函数

![](img/a55777cda2540c383d59ca2f7ecd490e.png)

今天的灾难问题是一个数字排序的练习。但是有一个有趣的变化:它要求你分解一个数字，并使用它的数字来得到尽可能高的数字。在某些方面，它与前面的两个问题有关([如何在 JavaScript 和 TypeScript 中获取数组的最小值或最大值](https://medium.com/@el3um4s/how-to-get-min-or-max-of-an-array-in-javascript-and-typescript-ed1087c080cf)和[在 JavaScript 中把数字转换成字符串的 5 种方法](https://medium.com/@el3um4s/5-ways-to-convert-a-number-to-a-string-in-javascript-8335c233357f))

# 问题是

链接到[形](https://www.codewars.com/kata/5467e4d82edf8bbf40000155)

您的任务是创建一个函数，它可以将任何非负整数作为参数，并以降序返回它的数字。本质上，重新排列数字以创建尽可能高的数字。

示例:输入:`42145`输出:`54421`

输入:`145263`输出:`654321`

输入:`123456789`输出:`987654321`

# 我的解决方案

![](img/a356a3214e60a4215569569c1ce72a46.png)

我提出的解决方案分为 5 个步骤。

1.将数字转换为字符串(这是必要的，因为数字是不可迭代的)

```
const str: string = "" + n;
```

2.将字符串转换为字符数组

```
const strArray: string[] = [...str];
```

3.对字符数组进行排序

```
const sortedArray: string[] = strArray.sort((a, b) => +b - +a);
```

4.加入字符数组

```
const arrayJoined: string = sortedArray.join("");
```

5.将字符串转换为数字

```
const result = +arrayJoined;
```

通过把不同的部分放在一起，我得到了这个函数

```
export function descendingOrder(n: number): number {
  const str: string = "" + n;
  const strArray: string[] = [...str];
  const sortedArray: string[] = strArray.sort((a, b) => +b - +a);
  const arrayJoined: string = sortedArray.join("");
  return +arrayJoined;
}
```

我可以通过将各个步骤合并成一个步骤来编写一个更简洁的版本

```
export const descendingOrder = (x: number): number =>
  +[...("" + x)].sort((a, b) => +b - +a).join("");
```

从这个版本开始，我可以用 JavaScript 得到相同的东西。

```
export const descendingOrder = (x) =>
  +[...("" + x)].sort((a, b) => +b - +a).join("");
```

今天我就讲到这里。今天是我和妻子第一次约会的九周年纪念日。今天编码到此为止。是时候和我的新娘共度一天了。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们关于 [**推特**](https://twitter.com/inPlainEngHQ)[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**[**不和**](https://discord.gg/GtDtUAvyhW) **。******

## ****对扩展您的软件启动感兴趣吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。****

****我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。****