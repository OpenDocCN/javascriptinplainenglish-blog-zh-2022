# 如何用 JavaScript 将 JSON 转换成地图

> 原文：<https://javascript.plainenglish.io/javascript-convert-json-to-map-49f95e4a6d21?source=collection_archive---------9----------------------->

## 了解如何在 JavaScript 中将 JSON 字符串快速转换为地图。

![](img/945e8163ce29cdece9c7c5f19d48da09.png)

在 JavaScript 中将 JSON 转换成`Map`:

1.  用`JSON.parse()` 方法将 JSON 字符串解析成一个对象。
2.  用这个对象作为参数调用`Object.entries()`。
3.  将`Object.entries()`的结果传递给`Map()`构造函数。

例如:

```
const json =
  '{"user1":"John","user2":"Kate","user3":"Peter"}';const map = new Map(Object.entries(JSON.parse(json)));// Map(3) { 'user1' => 'John', 'user2' => 'Kate', 'user3' => 'Peter' }
console.log(map);
```

我们首先将字符串转换为对象，然后转换为数组，因为我们不能将 JSON 字符串直接解析为`Map`。`Object.entries()`方法获取一个对象并返回一个键值对列表，这些键值对对应于对象的每个属性的键和值:

```
const obj = {
  user1: 'John',
  user2: 'Kate',
  user3: 'Peter',
};const arr = Object.entries(obj);// [ [ 'user1', 'John' ], [ 'user2', 'Kate' ], [ 'user3', 'Peter' ] ]
console.log(arr);
```

`Map()`构造函数可以接受一个键值对的 iterable 来创建`Map`元素，所以我们将`Object.entries()`的结果直接传递给它。

# 将地图转换为 JSON

要将`Map`转换回 JSON 字符串，使用 Map 作为参数调用`Object.fromEntries()`方法，并将结果传递给`JSON.stringify()`方法:

```
const json =
  '{"user1":"John","user2":"Kate","user3":"Peter"}';const map = new Map(Object.entries(JSON.parse(json)));const jsonFromMap = JSON.stringify(Object.fromEntries(map));// {"user1":"John","user2":"Kate","user3":"Peter"}
console.log(jsonFromMap);
```

我们首先用`Object.fromEntries()`转换`Map`，因为我们不能直接将`Map`序列化为 JSON 字符串。`Object.fromEntries()`方法将任何键值对列表转换成一个对象:

```
const map = new Map([
  ['user1', 'John'],
  ['user2', 'Kate'],
  ['user3', 'Peter'],
]);const obj = Object.fromEntries(map);// { user1: 'John', user2: 'Kate', user3: 'Peter' }
console.log(obj);
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/d97dc9)

每周获取新的 web 开发技巧和教程

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)

*更多内容看*[**o**](https://plainenglish.io/)**。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**