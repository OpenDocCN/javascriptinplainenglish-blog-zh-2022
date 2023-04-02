# 如何将 JavaScript 对象数组转换成对象的属性值索引的哈希映射？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-javascript-object-array-to-a-hash-map-indexed-by-a-property-value-of-the-object-4e1365bf6d4f?source=collection_archive---------9----------------------->

## 如何将 JavaScript 对象数组转换成 hash map 对象的指南。

![](img/362e47c8063a6845540b8b824d4db83c.png)

Photo by [insung yoon](https://unsplash.com/@insungyoon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将 JavaScript objects 数组转换成 hash map 对象，其中每个条目的键都是对象的属性值。

在本文中，我们将研究如何将 JavaScript 对象数组转换成 hash map 对象。

# array . protocol . reduce

JavaScript 数组的`reduce`方法让我们可以轻松地将对象数组转换成对象。

例如，我们可以写:

```
const arr = [{
    key: 'foo',
    val: 'bar'
  },
  {
    key: 'hello',
    val: 'world'
  }
];const result = arr.reduce((map, obj) => {
  map[obj.key] = obj.val;
  return map;
}, {});console.log(result)
```

进行转换。

我们有一个`arr`对象数组。

我们调用`reduce`将数组中的对象，也就是`obj`组合成我们返回的对象，也就是`map`。

我们得到了`obj.key`，并将它设置为`map`的属性名。

而我们用`obj.val`作为`obj.key`的值。

第二个参数是一个空对象，它是归约结果的初始值。

因此，`result`的值为:

```
{foo: "bar", hello: "world"}
```

# 使用映射构造函数将对象数组转换为哈希映射

我们可以用`Map`构造函数将对象数组转换成散列图。

例如，我们可以写:

```
const arr = [{
    key: 'foo',
    val: 'bar'
  },
  {
    key: 'hello',
    val: 'world'
  }
];const result = new Map(arr.map(({
  key,
  val
}) => ([
  key,
  val
])));
console.log(result)
```

在`map`方法中，我们从回调的参数对象中析构了`key`和`val`属性。

然后我们返回一个内部有`key`和`val`的数组。

然后我们将它传递给`Map`构造函数，从中创建一个 hash map 对象。

于是，`result`就是:

```
Map(2) {"foo" => "bar", "hello" => "world"}
```

根据控制台日志。

# `Lodash keyBy Method`

我们也可以使用 Lodash `keyBy`方法在第一个例子中创建相同的对象。

例如，我们可以写:

```
const arr = [{
    key: 'foo',
    val: 'bar'
  },
  {
    key: 'hello',
    val: 'world'
  }
];const result = _.keyBy(arr, o => o.key);
console.log(result)
```

我们只是传入一个回调函数来返回返回对象的属性。

根据`key`属性的值，`arr`的条目将被设置为键值。

所以我们得到:

```
{
  "foo": {
    "key": "foo",
    "val": "bar"
  },
  "hello": {
    "key": "hello",
    "val": "world"
  }
}
```

作为`result`的值。

# 对象. fromEntries

从对象数组创建 JavaScript 对象的另一种方法是使用`Object.fromEntries`方法。

例如，我们可以写:

```
const arr = [{
    key: 'foo',
    val: 'bar'
  },
  {
    key: 'hello',
    val: 'world'
  }
];const result = Object.fromEntries(
  arr.map(({
    key,
    val
  }) => ([
    key,
    val
  ]))
)
console.log(result)
```

我们传入一个键-值对数组的数组，就像我们试图从该数组创建一个`Map`实例时所做的那样。

因此，对于`result`的值，我们得到了与第一个例子相同的结果。

# 结论

我们可以使用 Lodash 的 JavaScript 标准库的数组和对象方法来创建对象的 JavaScript 对象数组。

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*