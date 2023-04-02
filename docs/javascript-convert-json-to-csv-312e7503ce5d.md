# 如何用 JavaScript 将 JSON 转换成 CSV

> 原文：<https://javascript.plainenglish.io/javascript-convert-json-to-csv-312e7503ce5d?source=collection_archive---------7----------------------->

![](img/6587a8de65396b2533e0d7d450cfc6fb.png)

下面是我们如何用 JavaScript 轻松地将 JSON 转换成 CSV:

```
function jsonToCsv(items) {
  const header = Object.keys(items[0]); const headerString = header.join(','); // handle null or undefined values here
  const replacer = (key, value) => value ?? ''; const rowItems = items.map((row) =>
    header
      .map((fieldName) => JSON.stringify(row[fieldName], replacer))
      .join(',')
  ); // join header and body, and break into separate lines
  const csv = [headerString, ...rowItems].join('\r\n'); return csv;
}const obj = [
  { color: 'red', maxSpeed: 120, age: 2 },
  { color: 'blue', maxSpeed: 100, age: 3 },
  { color: 'green', maxSpeed: 130, age: 2 },
];const csv = jsonToCsv(obj);console.log(csv);
```

这将是 CSV 输出:

```
color,maxSpeed,age
"red",120,2
"blue",100,3
"green",130,2
```

# 了解步骤

我们创建了一个可重用的`jsonToCsv()`函数，让我们将多个 JSON 字符串转换成 CSV。它接受一个包含对象的数组。每个对象将在 CSV 输出中占据一行。

我们在这个函数中做的第一件事是获取将用于 CSV 头的所有键。我们希望数组中的所有对象都有相同的键，所以我们使用 [Object.keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) 方法将第一个对象项中的键提取到一个数组中。

```
const obj = [
  { color: 'red', maxSpeed: 120, age: 2 },
  { color: 'blue', maxSpeed: 100, age: 3 },
  { color: 'green', maxSpeed: 130, age: 2 },
];// { color: 'red', maxSpeed: 120, age: 2 }
console.log(obj[0]);// [ 'color', 'maxSpeed', 'age' ]
console.log(Object.keys(obj[0]));
```

得到键后，我们调用数组上的 [join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 方法将所有元素连接成一个 CSV 头字符串。

```
const header = ['color', 'maxSpeed', 'age'];const headerString = arr.join(',');console.log(headerString); // color,maxSpeed,age
```

接下来，我们创建一个函数，它将作为回调传递给 [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 函数的 [replacer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#the_replacer_parameter) 参数。这个函数将处理 JSON 数组中对象的`undefined`或`null`属性值。

```
const obj = { prop1: 'Earth', prop2: undefined };// replace undefined property values with empty string ('')
const replacer = (key, value) => value ?? '';const str = JSON.stringify(obj, replacer);// {"prop1":"Earth","prop2":""}
console.log(str);
```

然后我们使用 [Array map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 方法从每个对象中获取属性值。`map()`采用在每个数组元素上调用的回调函数来返回转换。

这个回调使用`header`数组来获取每个对象的所有键。通过对`map()`的另一个调用，它遍历每个键，获取该键在对象中的对应值，并使用 [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) 将其转换为字符串。

这个对`map()`的内部调用最终产生一个数组，其中包含当前对象的所有字符串化属性值。

```
const header = ['color', 'maxSpeed', 'age'];const row = { color: 'red', maxSpeed: 120, age: 2 };const replacer = (key, value) => value ?? '';const rowItem = header.map((fieldName) =>
  JSON.stringify(row[fieldName], replacer)
);// array of stringified property values
console.log(rowItem); // [ '"red"', '120', '2' ]
```

将对象转换成属性值数组后，使用 [join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) 将数组转换成 CSV 行。

```
['"red"', '120', '2'].join(',') // -> "red",120,2
```

因此，JSON 数组中的每个对象都会发生这种转换，从而生成一个 CSV 行列表，存储在我们最初示例中的`rowItems`变量中。

为了生成最终的 CSV 输出，我们利用[扩展语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) ( `...`)将`headerString`和`rowItems`组合成一个数组。

```
const headerString = ['color', 'maxSpeed', 'age'];const rowItems = ['"red",120,2', '"blue",100,3', '"green",130,2'];[headerString, ...rowItems];
/*
Output ->
[
  [ 'color', 'maxSpeed', 'age' ],
  '"red",120,2',
  '"blue",100,3',
  '"green",130,2'
]
 */
```

然后我们在这个数组上调用 [join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) ，用`'\r\n'`字符串作为分隔符，创建一个字符串，CSV 标题和每个 CSV 行在单独的一行中。

```
const headerString = ['color', 'maxSpeed', 'age'];const rowItems = ['"red",120,2', '"blue",100,3', '"green",130,2'];console.log([headerString, ...rowItems].join('\r\n'));
/*
color,maxSpeed,age
"red",120,2
"blue",100,3
"green",130,2
 */
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/89c712)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[报名](https://cbdev.link/d3c4eb)立即免费领取一份。