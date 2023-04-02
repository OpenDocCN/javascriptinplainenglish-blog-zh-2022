# Intl JavaScript API 的 4 个很酷的语言技巧

> 原文：<https://javascript.plainenglish.io/4-cool-language-tricks-with-the-intl-javascript-api-ec6cd0a94a94?source=collection_archive---------2----------------------->

![](img/8b4499bfe7a8599595b79a66fdd8749e.png)

Photo by [Shannon Potter](https://unsplash.com/@cifilter?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

是 ECMAScript 国际化 API。它为数字、日期、列表等提供了对语言敏感的格式。这里有 4 个真正有用的东西可以用这个 API 来做。

# **序数**

序数是表示位置的数字，如 1、2、3。我们可以使用`PluralRules`构造函数，设置为类型`ordinal`，并根据返回值将响应映射到一系列后缀。

```
const suffixes = new Map([
  ['one',   'st'],
  ['two',   'nd'],
  ['few',   'rd'],
  ['other', 'th'],
]);const formatter = new Intl.PluralRules('en-US', { type: 'ordinal' });const numberToOrdinal = (n) => {
  const suffix = suffexes.get(formatter.select(n));
  return `${n}${suffix}`;
};
```

要转换一个数字，我们只需将它传递给`numberToOrdinal`方法。

```
numberToOrdinal(1) // '1st'
numberToOrdinal(2) // '2nd'
numberToOrdinal(11) // '11th'
numberToOrdinal(33); // '33rd'
```

# **列表格式**

如果你想显示一个字符串数组，你可以使用`Intl.ListFormat`构造函数来代替`.join(', ')`调用，从而获得简单国际化的额外好处。

```
// Conjunction
const formatter = new Intl.ListFormat('en-US', { style: 'long' })
formatter.format(['apple', 'orange', 'banana']) // 'apple, orange, and banana'// Disjunction
const formatter = new Intl.ListFormat('en-US', { style: 'long', type: 'disjunction' })
formatter.format(['apple', 'orange', 'banana']) // 'apple, orange, or banana'// German Conjunction
const formatter = new Intl.ListFormat('de', { style: 'long' })
formatter.format(['apple', 'orange', 'banana']) // 'apple, orange und banana'
```

# **大数格式**

`NumberFormat`有助于将较大的数字格式化成可读性更强的东西。例如，您可以用乘法单位显示一个紧凑的数字(如“m”代表百万或“k”代表千)以减少它所占的空间。

```
const formatter = new Intl.NumberFormat('en-US', { notation: 'compact' })
formatter.format(87654321) // '88M'
```

或者，如果你只是想在数字之间用逗号分隔，那么“标准”符号就很容易做到。

```
const formatter = new Intl.NumberFormat('en-US', { notation: 'standard' })
formatter.format(87654321) // '87,654,321'
```

你甚至可以格式化科学数字。

```
const formatter = new Intl.NumberFormat('en-US', { notation: 'scientific' })
formatter.format(87654321) // '8.765E7'
```

# **翻译国家和地区名称**

使用`DisplayNames`构造函数，我们可以将国家和地区名称翻译成用户偏好的语言。我们将`type`设置为 region，并调用传递区域代码的`of`方法。

```
const formatter = new Intl.DisplayNames('en-US', { type: 'region' })
formatter.of('us') // United Statesconst formatter = new Intl.DisplayNames('it', { type: 'region' })
formatter.of('us') // Stati Uniti
```

# **奖励:自动检测用户的语言**

通过将第一个参数(`locales`)保留为`undefined`，我们告诉 JavaScript 自动检测用户的语言。

```
// My English configured laptop
const formatter = new Intl.ListFormat(undefined, { style: 'long' })
formatter.format(['apple', 'orange', 'banana']) // 'apple, orange and banana'// Someone's German configured laptop
const formatter = new Intl.ListFormat(undefined, { style: 'long' }) // 'apple, orange und banana'
```

# **资源**

- `[Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)` [API 参考— MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****