# 如何用 Lodash 过滤一个对象的键？

> 原文：<https://javascript.plainenglish.io/how-to-filter-keys-of-an-object-with-lodash-6b43832df461?source=collection_archive---------9----------------------->

![](img/60d09efc8760f0275949c609ddb2e4ac.png)

Photo by [Raychan](https://unsplash.com/@wx1993?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们可能想从一个对象中提取一些属性，用 Lodash 把它们放到一个新的对象中。

在本文中，我们将看看如何从原始对象中只获得一些键的对象。

# 使用 pickBy 方法

Lodash 附带了`pickBy`方法，该方法接受一个对象和一个回调，该回调让我们返回我们想要保留的键的条件。

例如，我们可以写:

```
const thing = {
  "a": 123,
  "b": 456,
  "abc": 6789
};const result = _.pickBy(thing, (value, key) => {
  return _.startsWith(key, "a");
});
console.log(result)
```

然后我们返回一个具有从`thing`开始的`'a'`属性的对象。

`pickBy`的第一个参数是我们想要从中提取属性的对象。

第二个参数是回调函数，它返回我们想要提取的键的属性的条件。

那么`result`是:

```
{
  "a": 123,
  "abc": 6789
}
```

# 使用 omitBy 方法

我们也可以使用 Lodash `omitBy`方法来做同样的事情。

例如，我们可以写:

```
const thing = {
  "a": 123,
  "b": 456,
  "abc": 6789
};const result = _.omitBy(thing, (value, key) => {
  return !_.startsWith(key, "a");
});
console.log(result)
```

参数与`pickBy`相同，除了回调返回我们不希望在返回的对象中出现的键的条件。

所以，`result`和之前一样。

# 结论

我们可以使用`pickBy`或`omitBy` Lodash 方法从一个对象中提取键，并从原始对象中返回一个具有我们想要的属性的对象。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***