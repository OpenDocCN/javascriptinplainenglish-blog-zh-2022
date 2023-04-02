# JavaScript 中的 URLSearchParams API

> 原文：<https://javascript.plainenglish.io/the-urlsearchparams-api-in-javascript-19748ef513d5?source=collection_archive---------11----------------------->

![](img/1b3bf1cf9ca3803eb271bb5afab2d181.png)

Photo by [Nubelson Fernandes](https://unsplash.com/@nublson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`URLSearchParams` API 提供了实用方法来解析来自 [URL](https://developer.mozilla.org/en-US/docs/Glossary/URL) 的查询字符串的数据。`URLSearchParams()`构造函数从查询字符串创建一个新的`URLSearchParams`对象并返回它。它忽略了查询字符串中的前导问号`?`，所以我们也可以传递没有前导`?`的查询字符串。

```
// URL: [https://myshop.com/mobiles?color=black&sort=price_asc](https://myshop.com/mobiles?color=black&sort=price_asc)
const search = new URLSearchParams('color=black&sort=price_asc');
```

如果我们提供完整的 URL 而不是查询字符串，那么`URLSearchParams()`构造函数就不能正确解析数据。如果我们有一个完整的 URL，我们可以使用 [URL API](https://jscurious.com/the-url-api-in-javascript/) 解析其中的查询字符串，并将其传递给`URLSearchParams()`构造函数。

```
// Wrong way
const search = new URLSearchParams('[https://myshop.com/mobiles?color=black&sort=price'](https://myshop.com/mobiles?color=black&sort=price'));// Correct way
const url = new URL('[https://myshop.com/mobiles?color=black&sort=price'](https://myshop.com/mobiles?color=black&sort=price'));
const search = new URLSearchParams(url.search);
// OR pass the query string directly 
const search = new URLSearchParams('color=black&sort=price');
```

# 实用方法

`URLSearchParams`实用程序方法让我们可以轻松地访问查询参数，还可以添加新的或修改任何现有的参数。让我们一起来探索它们。

## get()方法

该方法采用查询参数名称，并返回第一个匹配的值。如果没有找到匹配，它返回`null`。

```
const search = new URLSearchParams('color=black&sort=price_asc&color=red');
console.log(search.get('color')); // 'black'
console.log(search.get('brand')); // null
```

## getAll()方法

该方法采用查询参数名称，并以数组形式返回所有关联的值。如果没有找到匹配，它返回一个空数组。

```
const search = new URLSearchParams('color=black&sort=price_asc&color=red');
console.log(search.getAll('color')); // ['black', 'red']
console.log(search.getAll('sort')); // ['price_asc']
console.log(search.getAll('brand')); // []
```

## has()方法

此方法检查查询字符串中是否存在提供的参数。如果参数存在，则返回`true`，否则返回`false`。

```
const search = new URLSearchParams('color=black&sort=price_asc');
console.log(search.has('sort')); // true
console.log(search.has('brand')); // false
```

## forEach()方法

这个方法让我们遍历所有的查询参数值。

```
const search = new URLSearchParams("color=black&sort=price_asc");
search.forEach((value, key) => console.log(key, value));
// color black
// sort price_asc
```

## keys()方法

这个方法返回一个包含所有查询参数名的迭代器对象。我们可以使用`for…of`循环迭代这个迭代器对象，或者使用 spread 操作符或`Array.from()`方法将它转换成一个数组。

```
const search = new URLSearchParams("color=black&sort=price_asc");
for (const key of search.keys()) {
  console.log(key);
}
/* -output-
    color
    sort
*/// convert to Array
console.log([...search.keys()]); // ['color', 'sort']
// OR
console.log(Array.from(search.keys())); // ['color', 'sort']
```

## values()方法

该方法返回包含所有查询参数值的迭代器对象。

```
const search = new URLSearchParams("color=black&sort=price_asc");
console.log([...search.values()]); // ['black', 'price_asc']
```

## entries()方法

这个方法返回一个迭代器对象，包含查询参数的所有键值对及其值。

```
const search = new URLSearchParams("color=black&sort=price_asc");
console.log([...search.entries()]); 
// [['color', 'black'], ['sort', 'price_asc']]
```

## append()方法

此方法将带有值的新查询参数追加到现有查询字符串中。

```
const search = new URLSearchParams('color=black&sort=price_asc');
search.append('brand', 'apple');
console.log(search.toString()); 
// 'color=black&sort=price_asc&brand=apple'
```

## set()方法

该方法用提供的参数值替换任何现有的查询参数值，如果提供的参数不存在，它会追加它。如果所提供的参数出现多次，它将删除它们并只替换第一个参数的值。

```
const search = new URLSearchParams('color=black&sort=price_asc&color=red');
search.set('sort', 'popularity');
search.set('color', 'green');
search.set('brand', 'apple');
console.log(search.toString()); 
// 'color=green&sort=popularity&brand=apple'
```

## delete()方法

此方法删除与所提供的查询参数键关联的所有条目。

```
search = new URLSearchParams('color=black&sort=price_asc&color=red');
search.delete('color');
search.delete('brand');
console.log(search.toString()); // 'sort=price_asc'
```

## sort()方法

这个方法按照键对查询字符串进行排序，如果存在多个同名的键，那么它们的相对顺序将被保留。

```
const search = new URLSearchParams('sort=price&ram=8gb&color=red&ram=4gb');
search.sort();
console.log(search.toString()); 
// color=red&ram=8gb&ram=4gb&sort=price
```

# 你可能也喜欢

*   [JavaScript 中的 URL API](https://jscurious.com/the-url-api-in-javascript/)
*   [使用 JavaScript 中的通知 API 发送推送通知](https://jscurious.com/the-notification-api-in-javascript/)
*   [用 JavaScript 中的 HTMLAudioElement API 播放音频](https://jscurious.com/play-audio-with-htmlaudioelement-api-in-javascript/)
*   [JavaScript 中的地图，当它是比对象更好的选择时](https://jscurious.com/map-in-javascript-and-how-it-is-better-than-object/)
*   [JavaScript 中检查对象中是否存在键的不同方法](https://jscurious.com/different-ways-to-check-if-a-key-exists-in-an-object/)
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [JavaScript 中承诺的简要指南](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20+ JavaScript 速记编码技巧和窍门](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的时间:)*
***阿米塔夫·米什拉***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **