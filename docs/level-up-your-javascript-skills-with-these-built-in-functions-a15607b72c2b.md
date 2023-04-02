# 使用这些内置函数提升您的 JavaScript 技能

> 原文：<https://javascript.plainenglish.io/level-up-your-javascript-skills-with-these-built-in-functions-a15607b72c2b?source=collection_archive---------5----------------------->

## 通过学习这些 JavaScript 内置函数成为更好的开发人员:at()、map()、forEach()和 filter()。

![](img/c343a74f9a848814dfe74f71bfb56c95.png)

[Photo by Josh Hild from Pexels](https://www.pexels.com/photo/photo-of-tent-at-near-trees-2422265/)

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) [## 标准内置对象- JavaScript | MDN

### 本章记录了 JavaScript 的所有标准内置对象，包括它们的方法和属性。术语…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) [## 数组- JavaScript | MDN

### 在 JavaScript 中，数组不是原语，而是具有以下核心特征的数组对象:创建…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) 

每一次更新，JavaScript 都会添加一些新的功能，使我们作为开发人员的生活更加轻松。如果我们能够利用内置的功能，那么一些库和框架是不错的，为什么不呢？下面我们将介绍几个我最喜欢的！

# 在()

at()方法接受一个整数，然后返回给定索引处的项目。这很好，因为它允许我们传递正数和负数。正整数值从左向右计数，负整数值从右向左计数。

虽然您可以很容易地用方括号符号传递整数值，例如用`array[3]`表示正整数，或者用`array[array.length-3]`，但是使用`array(-3)`或者`array(3)`更简单，可读性更好。在下面的例子中，我们将传递一些反叛的成员，并抓取我们最关心的成员:

```
const namesArray = [
  'Ahsoka',
  'Luke',
  'Jyn',
  'Leia',
  'Wedge'
];// at()
console.log(namesArray.at(2)); // Output: Jyn
console.log(namesArray.at(-2)); // Output: Leia// Square bracket notation
console.log(namesArray[2]); // Output: Jyn
console.log(namesArray[namesArray.length - 2]); // Output: Leia
```

正如你所看到的，虽然两种方法都有效，但是`at()`更简洁，更容易阅读。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at) [## array . prototype . at()-JavaScript | MDN

### at()方法接受一个整数值并返回该索引处的项目，允许使用正整数和负整数…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/at) 

# 地图()

`map()`函数创建一个数组，其中填充了被调用数组中元素的值。例如，如果我们想要一个新的数组来填充反抗军成员的名字或姓氏，我们可以调用`map()`函数。

虽然我们可以用 for 循环完成类似的事情，但是。map()函数允许我们简化代码和复杂性。

```
const rebellionNames = [
  {
   firstName: 'Ahsoka',
   lastName: 'Tano'
  },
  {
    firstName: 'Luke',
    lastName: 'Skywalker'
  },
  {
    firstName: 'Jyn',
    lastName: 'Erso'
  },
  {
    firstName: 'Leia',
    lastName: 'Organa'
  },
  {
    firstName: 'Wedge',
    lastName: 'Antilles'
  }
];const firstName = rebellionNames.map((character) => {
  return character.firstName;
});const lastName = rebellionNames.map((character) => {
  return character.lastName;
});console.log(firstName); 
// Output: ["Ahsoka", "Luke", "Jyn", "Leia", "Wedge"]
console.log(lastName); 
// Output: ["Tano", "Skywalker", "Erso", "Organa", "Antilles"] 
```

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) [## array . prototype . map()-JavaScript | MDN

### (受这篇博文的启发)使用带有一个参数(被遍历的元素)的回调是很常见的。某些…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 

# forEach()

虽然`.map()`函数为我们提供了一个由我们传递的值组成的新数组，但是如果我们想逐个输出每个元素呢？我们可以使用内置的`forEach()`来完成这项工作，这非常方便。

在提供的例子中，我们将使用 namesArray，它由几个字符串组成，然后逐个输出它们。我们可以很容易地将它与类似于`.filter()`的东西配对，以搜索特定的名称或基于名称的长度。

```
const namesArray = [
  'Ahsoka',
  'Luke',
  'Jyn',
  'Leia',
  'Wedge'
];namesArray.forEach((name) => console.log(name));
// expected output: "Ahsoka"
// expected output: "Luke"
// expected output: "Jyn"
// expected output: "Leia"
// expected output: "Wedge"
```

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) [## array . prototype . foreach()-JavaScript | MDN

### forEach()按索引升序为数组中的每个元素调用一次提供的 callbackFn 函数。它不是…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) 

# 过滤器()

最后，我们来讨论一下`filter()`函数。`filter()`函数创建一个给定数组的一部分的[浅拷贝](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)，过滤掉给定数组中通过由提供的函数实现的测试的元素。本质上，如果我们想获取长度超过 4 个字符的内容，或者等于' Luke '的内容，我们可以这样做。让我们来看一个例子！

在给定的例子中，我们将检查任何带有`name.length > 4`或`name === 'Luke'`的东西。我们正在检查 names 数组中的值。这些应该会返回一个新的数组，其中包含了我们所关心的内容。

```
const namesArray = [
  'Ahsoka',
  'Luke',
  'Jyn',
  'Leia',
  'Wedge'
];
const result = namesArray.filter((name) => name.length > 4);
console.log(result);
// Output: Array ["Ahsoka", "Wedge"]const specifiedName = namesArray.filter((name) => name === 'Luke');
console.log(specifiedName);
// Output: Array ["Luke"]
```

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) [## array . prototype . filter()-JavaScript | MDN

### filter()为数组中的每个元素调用一次 callbackFn 函数，并构造一个包含所有元素的新数组

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) 

虽然这些只是 JavaScript 提供的现成可用功能中的一小部分，但我希望它们对您有所帮助。我为每一个都附上了 MDN 文档链接，以防你想要更详细的内容。我对编码的总体看法是，如果没有必要，就避免安装库或工具，这将使您的代码库更小，并导致更快的加载时间！

The Mandalorian by Disney

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于用 React 设置[Firebase](/use-a-firebase-db-inside-your-reactjs-project-2cfb56b51162)、[自定义主题开发 Shopify](/developing-custom-themes-for-shopify-getting-started-b137407c0cb7) 、[基于类的 React 组件](/class-based-components-in-react-14335f0ee539)、 [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 、 [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) 、& [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) 的文章。感谢您的阅读，祝您愉快！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，*[*不和*](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。*