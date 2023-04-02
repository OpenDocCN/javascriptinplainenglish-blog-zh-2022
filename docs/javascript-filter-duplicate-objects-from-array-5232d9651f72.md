# 如何在 JavaScript 中过滤数组中的重复对象

> 原文：<https://javascript.plainenglish.io/javascript-filter-duplicate-objects-from-array-5232d9651f72?source=collection_archive---------3----------------------->

![](img/f0d95eeee6328556ed1ada072de4b3d6.png)

# 1.仅保留数组中具有属性值的第一个对象

要通过 JavaScript 中的属性过滤数组中的重复对象，请使用`filter()`方法过滤掉数组中不是第一个具有属性值的元素。

例如:

`JavaScript`

```
const arr = [
  {
    name: 'John',
    location: 'Los Angeles',
  },
  {
    name: 'Kate',
    location: 'New York',
  },
  {
    name: 'Mike',
    location: 'New York',
  },
];

const unique = arr.filter(
  (obj, index) =>
    arr.findIndex((item) => item.location === obj.location) === index
);
/*
   [
     { name: 'John', location: 'Los Angeles' },
     { name: 'Kate', location: 'New York' }
   ]
 */
console.log(unique);
```

`[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`[filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`根据回调函数指定的条件测试数组中的每个元素，并创建一个填充了通过测试的元素的新数组。它不会修改原始数组。

`JavaScript`

```
const arr = [1, 2, 3, 4];

const filtered = arr.filter((num) => num > 2);
console.log(filtered); // [ 3, 4 ]
```

`[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)`[findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)`方法搜索数组中的元素，并返回第一个通过测试的元素的索引，该索引由传递给它的回调函数指定。我们用它来查找与对象`filter()`当前测试的属性值相同的第一个数组元素。

在我们的例子中，对象的`filter()`条件是它的数组索引与`findIndex()`的结果相同。如果该条件为`true`，则意味着该对象是第一个具有属性值的数组元素。如果是`false`，这意味着已经有一个数组项具有该属性值，所以该对象是重复的，不应该包含在结果中。

`JavaScript`

```
const arr = [
  {
    name: 'John',
    location: 'Los Angeles',
  },
  {
    name: 'Kate',
    location: 'New York',
  },
  {
    name: 'Mike',
    location: 'New York',
  },
];

// true - first object with location of New York
console.log(1 === arr.findIndex((obj) => obj.location === 'New York'));

// false - will not be included in result
console.log(2 === arr.findIndex((obj) => obj.location === 'New York'));
```

# 通过多个属性过滤数组中的重复对象

根据您的具体情况，您可能希望一个对象只有在具有两个或更多相同值的属性(多个属性值相同)时才被视为重复。

对于这种情况，我们将像以前一样使用`filter()`和`findIndex()`，但是我们将在`filter()`的对象和`findIndex()`的对象之间为所有属性添加额外的比较。

例如:

`JavaScript`

```
const arr = [
  {
    name: 'Kate',
    location: 'New York'
  },
  {
    name: 'Mike',
    location: 'New York'
  },
  {
    name: 'Kate',
    location: 'New York'
  }
];

const unique = arr.filter(
  (obj, index) =>
    arr.findIndex(
      (item) => item.location === obj.location && item.name === obj.name
    ) === index
)
/*
   [
      { name: 'Kate', location: 'New York' },
      { name: 'Mike', location: 'New York' }
   ]
 */
console.log(unique);
```

# 2.从`unique`数组中排除重复项

这里有另一种在 JavaScript 中从数组中过滤重复对象的方法:

1.  创建一个空的`unique`数组来存储唯一的对象。
2.  遍历数组中的对象。
3.  对于每个对象，如果它不是重复的，就将其添加到`unique`数组中。否则，忽略它。

例如:

`JavaScript`

```
const arr = [
  {
    name: 'John',
    location: 'Los Angeles',
  },
  {
    name: 'Kate',
    location: 'New York',
  },
  {
    name: 'Mike',
    location: 'New York',
  },
];

const unique = [];
for (const item of arr) {
  const isDuplicate = unique.find((obj) => obj.location === item.location);
  if (!isDuplicate) {
    unique.push(item);
  }
}
/*
   [
    { name: 'John', location: 'Los Angeles' },
    { name: 'Kate', location: 'New York' }
  ]
*/
console.log(unique);
```

我们使用`[for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)`循环迭代数组，并对每个对象执行一个操作。

对于每个对象，我们使用`[find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)`方法来检查它是否已经存在于`unique`数组中。`Array` `find()`搜索数组中通过指定测试的第一个对象，类似于`findIndex()`，但它返回对象本身，而不是其数组索引。

`JavaScript`

```
const nums = [2, 5, 8, 13, 19];

const doubleDigit = nums.find((num) => num > 9);
console.log(doubleDigit); // 13
```

如果它不在`unique`数组中，我们简单地用`[push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)`方法添加它。

这种方法不像第一种方法那样是一个[单句](https://codingbeautydev.com/blog/javascript-one-liners/)，但是你会发现它更容易理解。作为一个人，从列表中删除重复的项目似乎是一种自然的方式。

# 通过多个属性过滤数组中的重复对象

与前面的方法一样，如果使用多个属性来确定一个对象是否重复，您可以简单地为属性添加更多检查—这次是在`find()`方法中:

`JavaScript`

```
const arr = [
  {
    name: 'Kate',
    location: 'New York',
  },
  {
    name: 'Mike',
    location: 'New York',
  },
  {
    name: 'Kate',
    location: 'New York',
  },
];

const unique = [];
for (const item of arr) {
  // 👇 "name" and "location" used for duplicate check
  const duplicate = unique.find(
    (obj) => obj.location === item.location && obj.name === item.name
  );
  if (!duplicate) {
    unique.push(item);
  }
}
/*
  [
    { name: 'Kate', location: 'New York' },
    { name: 'Mike', location: 'New York' }
  ]
 */
console.log(unique);
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/ba2999)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) 、 [***领英***](https://www.linkedin.com/company/inplainenglish/) ***、***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*