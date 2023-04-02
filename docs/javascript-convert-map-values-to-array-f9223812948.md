# 如何在 JavaScript 中将地图值转换为数组

> 原文：<https://javascript.plainenglish.io/javascript-convert-map-values-to-array-f9223812948?source=collection_archive---------20----------------------->

![](img/67d3d699fa04891e4029e63e1b011d04.png)

让我们来看一些在 JavaScript 中将`Map`对象的值轻松转换成数组的方法。

# 1.从()映射值()和数组

要将`Map`值转换成数组，我们可以调用`Map`上的`values()`方法，并将结果传递给`Array.from()`方法。例如:

```
const map = new Map([
  ['user1', 'John'],
  ['user2', 'Kate'],
  ['user3', 'Peter'],
]);const values = Array.from(map.values());console.log(values); // [ 'John', 'Kate', 'Peter' ]
```

`Map` `values()`方法返回`Map`中的可迭代值。`Array.from()`方法可以像这样从 iterables 创建数组。

# 2.映射值()和展开语法(…)

我们还可以使用 spread 语法(`...`)将`Map` `values()`方法返回的 iterable 的元素解包到一个数组中。例如:

```
const map = new Map([
  ['user1', 'John'],
  ['user2', 'Kate'],
  ['user3', 'Peter'],
]);const values = [...map.values()];console.log(values); // [ 'John', 'Kate', 'Peter' ]
```

使用 spread 语法允许我们将多个`Map`对象的值合并到一个数组中。例如:

```
const map1 = new Map([['user1', 'John']]);const map2 = new Map([
  ['user2', 'Kate'],
  ['user3', 'Peter'],
]);const values = [...map1.values(), ...map2.values()];console.log(values); // [ 'John', 'Kate', 'Peter' ]
```

*更新于:*[*codingbeautydev.com*](https://cbdev.link/e012fd)

每周获取新的 web 开发技巧和教程

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)