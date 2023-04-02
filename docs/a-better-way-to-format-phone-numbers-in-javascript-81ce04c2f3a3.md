# 用 JavaScript 格式化电话号码的更好方法

> 原文：<https://javascript.plainenglish.io/a-better-way-to-format-phone-numbers-in-javascript-81ce04c2f3a3?source=collection_archive---------3----------------------->

## JavaScript 技巧

## 使用 JavaScript 中的自定义模板实现电话号码格式的一致性

![](img/a8005407292204daaf77b59d2888df7a.png)

今天的问题涉及根据模板格式化电话号码。这是一个有趣的谜题，因为它非常有用。不久前，我有机会开发一个 Microsoft Access 应用程序来管理电话号码列表。最有趣的方面之一是理解如何根据号码本身的国家显示电话号码。或者，如何基于模板显示电话号码。在这篇文章中，我用 JavaScript 解决了同样的问题。

# 问题:通过模板格式化电话号码

链接到[形](https://www.codewars.com/kata/61393fd03e441f001ac9c7d4)

![](img/2b1a07654c6ba406803c8f287a87480d.png)

你需要写一个函数，通过一个模板来格式化一个电话号码。

给你数字和字符串。

如果位数比需要的多，应该忽略它们

如果位数少于所需位数，应返回无效的电话号码

例子

```
(79052479075, "+# ### ### ## ##") => "+7 905 247 90 75"
(79052479075, "+# (###) ### ##-##") => "+7 (905) 247 90-75"
(79052479075, "+# ### ### ## ##") => "+7 905 247 90 75"
(81237068908090, "+## ### ### ## ##") => "+81 237 068 90 80"
(8123706890, "+## ### ### ##-##") => "Invalid phone number"
(911, "###") => "911"
(112, "+ () -") => "+ () -"
```

# 我的解决方案

![](img/b7b1b311356ace6f1cf423e7133e188a.png)

我对我的解决方案很满意。我决定用正则表达式来解决这个问题。我只需要一个简单的正则表达式来标识模板中的标签(`#`):

```
const re: RegExp = /#/g;
```

使用这个正则表达式，我可以计算模板中所有的 hashtags。这让我明白数字中的位数是否足以满足模板。

```
const len: number = template.match(re)?.length ?? -1;
```

我不能在正则表达式上直接使用`length`，因为它可能是`undefined`。在这种情况下，我返回`-1`来表明我没有找到任何标签。

要计算数字的位数，只需将其转换为字符串并计算位数即可:

```
const num: string = number.toString();
```

如果数字的位数小于标签数，我返回`Invalid phone number`。

```
if (num.length < len) {
  return "Invalid phone number";
}
```

为了用数字替换模板中的标签，我可以使用一个`for`循环。但在这种情况下，我不需要它。我只需要在模板字符串上调用`replace`。这样，每当我找到一个标签，我就用相应的数字替换这个字符。

```
let i = 0;
let result = template.replace(re, () => num[i++]);
```

我不得不使用一个`replace`循环外部的变量来跟踪当前数字的索引。这样，每当我找到一个 hashtag，我就用相应的数字替换这个字符。此外，我还利用了 Increment ( `++`)运算符的属性:

> 递增(++)运算符对其操作数进行递增(加 1 ),并根据运算符的位置返回递增前后的值。

这样，我只有在替换完成后才增加索引。

综合所有因素，我得到了以下解决方案:

```
export const formatNumber = (number: number, template: string): string => {
  const re: RegExp = /#/g;
  const num: string = number.toString();
  const len: number = template.match(re)?.length ?? -1;

  let i = 0;
  let result =
    num.length < len
      ? "Invalid phone number"
      : template.replace(re, () => num[i++]);
  return result;
};
```

# 更好的解决方案

![](img/6bca2cf0c9e895d3bc7471c83aca634a.png)

尽管我对自己的解决方案很满意，但还有另一种基于模板格式化电话号码的方法。解决方案不是我的，而是另一个用户提出的。解决方案更加优雅，可读性更好。

```
export function formatNumber(number: number, template: string): string {
  for (const digit of `${number}`) template = template.replace("#", digit);
  if (template.includes("#")) return "Invalid phone number";
  return template;
}
```

在这种情况下，我们使用一个`for...of`循环来迭代数字中的所有数字。这样，用相应的数字替换每个 hashtag 就足够了。

甚至控制条件也比较简单。如果模板仍然包含 hashtags，则表示数字中的位数小于 hashtags 的个数。这种情况下，我返回`Invalid phone number`。

我也可以用这个方法来检查数字中的位数是否足够满足模板。这样，我可以稍微简化一下我的解决方案:

```
export const formatNumber = (n: number, template: string, i = 0): string => {
  let result: string = template.replace(/#/g, () => `${n}`[i++] ?? "#");
  return result.includes("#") ? "Invalid phone number" : result;
};
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及*******不和****

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*