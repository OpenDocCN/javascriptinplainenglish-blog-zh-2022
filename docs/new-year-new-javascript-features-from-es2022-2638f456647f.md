# 新的一年，ES2022 的新 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/new-year-new-javascript-features-from-es2022-2638f456647f?source=collection_archive---------8----------------------->

![](img/51d539185c9486a8761a8a74bf6423ec.png)

## 顶级等候。私人#。在()& more。ES2022 即将推出的产品。

每年，ES 团队都会收到许多关于改进辉煌的 JavaScript 生态系统的建议，其中一些最终被正式实施。为了被接受，一个特性需要经历 [TC39](https://tc39.es/process-document/) 中提到的 4 个阶段(同时查看 [TC39 回购](https://github.com/tc39))。

以下部分将在即将到来的更新中增加:

*   对于令人敬畏的**异步/等待**风扇，我们有**:模块加载**
*   对于精明的 OOP 爱好者，我们有**类**
*   对于出色的**函数式**程序员，我们有:**内置对象**

![](img/ec1ce13df8b45c06201126348ef77c1c.png)

ES2022 > ES2021

# 1.模块加载

> 厌倦了在文件根等待时出错？升级传入。

每个人都喜欢 ***异步*** 函数和 ***await*** 关键字，因为它将我们从嵌套承诺的地狱中拯救了出来，但是它将 await 的使用限制为只能使用异步函数，而不能在文件的根目录下使用，作为程序员，我们讨厌(或喜欢)编写变通办法🤓。

在 ES2022 中，我们可以使用顶级 await 来动态导入资源，这在 CLI 脚本中非常有用。

我们可以这样使用它:

```
// load-resources.mjs 
// with top-level await
const data = await (await fetch("https://resources")).text();
export const resource = JSON.parse(data).resource;
```

截至 2022 年 1 月， [81%的设备](https://caniuse.com/mdn-javascript_operators_await_top_level)和 Node.js 14.8+都支持它。

# 2.班级

## 私有一切

> 俗话说，保持你的变量私人，但你的关系公开。

大多数面向 OOP 的语言使用 private 和 public 来限制或扩展字段、方法或访问器的可见性。但是 JavaScript 在这方面没有限制。现在，它们通过前缀#包含在 JavaScript 中。

```
class LikeCounter {
  #likes;constructor(likes) {
    this.#likes = likes;    
  } #increment () {
    return this.#likes + 1;
  }#decrement () {
    return this.#likes - 1;
  }doSomethingWithIt() {
    this.#decrement()
  }
}const obj = new LikeCounter(123);
console.log(object.#doSomethingWithIt());    // SyntaxError
console.log(object.#likes);   // SyntaxError
object.doSomethingWithIt();
```

[大部分浏览器](https://caniuse.com/mdn-javascript_classes_private_class_fields)(2022 年 1 月使用率 88%左右)和 Node.js 12+都支持私有实例字段。

关于[私有方法和访问器](https://caniuse.com/mdn-javascript_classes_private_class_methods)对大多数浏览器的支持大约是 82 %, node . js 从 14.6 版本开始支持这个特性。

## 公共静态类字段

> 想让你的班级更时尚吗？添加全新的静态字段。

[**静态类字段**](https://github.com/tc39/proposal-static-class-features#static-public-fields) 是一种方便的向类对象追加属性的新符号。

```
// no static class fields:
class Product {
  // ...
}
Product.id = 1;// now static class fields:
class Product {
  static id = 1;
  // ...
}
```

[大部分浏览器](https://caniuse.com/mdn-javascript_classes_static_class_fields)(2022 年 1 月使用率:~89%)和 Node.js 12+都支持公共类字段。

## 私有字段的存在性检查

> 存在或不存在，或者更好地说，存在或不存在是一种该死的财产。

因为试图访问一个对象上不存在的私有字段会抛出一个不幸的异常，所以需要 **exist** 一个方法来检查一个对象是否有给定的私有字段。运算符 中的 [**来了。**](https://github.com/tc39/proposal-private-fields-in-in)

```
class Dog {
  #namestatic isDogInstance(object) {
    return #name in object;
  }
}
```

对于在私有字段上使用 `[in](https://caniuse.com/mdn-javascript_classes_private_class_fields_in)` [操作符的](https://caniuse.com/mdn-javascript_classes_private_class_fields_in)[浏览器支持是有限的(2022 年 1 月使用率约为 70%)。Node.js 从 16.4 版开始支持该功能。](https://caniuse.com/mdn-javascript_classes_private_class_fields_in)

## 私有静态类字段和方法

> 静态变量总是公共的？只是将他们私有化(糟糕的苏联笑话)。

作为私有字段和方法，封装限制在类级别上是有用的。 [**私有静态方法和字段特性**](https://github.com/tc39/proposal-static-class-features) 使用`#`前缀为类级别的字段和方法添加了硬可见性限制。

```
class Customer {
  static #idCounter = 1; // static privatestatic #getNextId() { // static private
    return Customer.#idCounter++;
  }#id; // instance privateconstructor() {
    this.#id = Customer.#getNextId();
  }toString() {
    return `c${this.#id}`;
  }
}const customers = [new Customer(), new Customer()];
console.log(customers.join(' ')); // c1 c2
```

支持百分比类似于前面描述的私有实例字段和方法。

## 静态类初始化块

> 想把静态变量复杂化吗？好了，我们开始吧…

有时对静态类字段进行更复杂的初始化工作是必要的或方便的。使用前面的私有静态字段特性，这种初始化必须发生在类内部，因为私有字段是不可访问的。

[**静态初始化程序块特性**](https://github.com/tc39/proposal-class-static-block) 提供了一种在类定义评估期间执行代码的机制。

只需创建一个以`static`关键字为前缀的代码块，它将在类初始化时执行:

```
class Example {
  static propertyA;
  static #propertyB; // privatestatic { // static initializer block
    try {
      const json = JSON.parse(fs.readFileSync('example.json', 'utf8'));
      this.propertyA = json.someProperty;
      this.#propertyB = json.anotherProperty;
    } catch (error) {
      this.propertyA = 'default1';
      this.#propertyB = 'default2';
    }
  }static print() {
    console.log(Example.propertyA);
    console.log(Example.#propertyB);
  }
}Example.print();
```

[浏览器对静态类初始化块](https://caniuse.com/mdn-javascript_classes_static_initialization_blocks)的支持有限(2022 年 1 月正好 **69.69%)** 。Node.js 从 16.4 版开始支持该功能。

# 3.内置对象

## 错误:。原因

> 有意义的信息不够有意义？给你的错误添加原因。

错误通常被包装以附加有意义的消息并记录错误上下文。然而，这意味着原始错误可能会丢失。出于日志记录和调试目的，将原始错误附加到包装错误是可取的。

[**错误原因特性**](https://github.com/tc39/proposal-error-cause) 提供了一种将原始错误附加到包装错误的标准化方法。它向`Error`构造函数添加了`cause`选项，并添加了一个用于检索原始错误的`cause`字段。

```
const getProduct = async (productId) => {
  try {
    return await fetch(`https://server/api/products/${productId}`);
  } catch (error) {
    throw new Error(
      `Loading product data with id ${productId} failed`, 
      { cause: error }
    );
  }
}try {
  const productData = await load(69420);
  // do something
} catch (error) {
  console.log(error); // Error: Loading data for product with id 69420 failed
  console.log(error.cause); // TypeError: Failed to fetch
}
```

当前浏览器对错误子句功能的支持是有限的(2022 年 1 月使用率:~75%)。Node.js 从 16.9 版本开始支持该功能。

## 数组、字符串和类型数组:。在()

> 用 at(-1)python 化您的 JavaScript 代码

从数组或字符串的末尾获取元素是一件麻烦的事情，经常会导致冗长的重复代码，就像`let last = arr[arr.length - 1]`。这要求数组存储在临时变量中，并防止无缝链接。

[。at()特性](https://github.com/tc39/proposal-relative-indexing-method)提供了一种更短、更优雅的方式来从字符串或数组的开头或结尾获取元素，而不需要临时变量。

```
const someString = "JSiscool";console.log(someString.at(3));    // i
console.log(someString[3]);       // iconst temp = someString;
console.log(temp[temp.length - 1]);      // l
console.log(temp.at(-1));   // l - no temporary variable required
```

[浏览器对。at 特性](https://caniuse.com/mdn-javascript_builtins_array_at)目前受限(2022 年 1 月使用率 70%左右)，仅在 Node.js 16.6+中可用。

## 对象:。hasOwn()

> 如果 hasOwn 是 IRL 父母测试将被淘汰

[**object . has own feature**](https://github.com/tc39/proposal-accessible-object-hasownproperty)是检查一个属性是否直接出现在一个对象上的强大而健壮的方法。这是使用`hasOwnProperty`的首选替代方案:

```
const dog = {
  name: "Olaf" // who would name his dog Olaf
};console.log(Object.prototype.hasOwnProperty.call(dog, 'name'));
console.log(Object.hasOwn(dog, 'name')); // better
```

[浏览器支持目前有限](https://caniuse.com/mdn-javascript_builtins_object_hasown)(2022 年 1 月使用率 70%左右)，需要 Node 16.9+才能直接使用`hasOwn`。

## RegExp:匹配索引(' d '标志)

> 如果你说正则表达式，这是为你疯狂的人

默认情况下，正则表达式匹配记录匹配文本的开始索引，但不记录其结束索引，也不记录其捕获组的开始和结束索引。

在涉及文本编辑器语法或搜索结果突出显示的用例中，将捕获组匹配索引作为正则表达式匹配的一部分会非常有用。

使用 [**regexp 匹配索引功能(‘d’flag)**](https://github.com/tc39/proposal-regexp-match-indices)，匹配和捕获组索引在表达式结果的`indices`数组属性中可用。匹配文本位置和匹配索引位置是相同的，例如，完全匹配的文本是匹配数组和索引数组中的第一个值。

在`indices.groups`中记录了被命名的捕获组的索引。

我真的不是正则表达式或古鲁，所以不要破坏我的语法。

```
const regexpr = /match\s(?<word>\w+):(?<digit>\d)/gd;
const someString = "Game three:3.";for (const match of someString.matchAll(regexpr)) {
    console.log(match);
}©
```

上面的示例代码有以下输出:

```
[
  'Game three one:3',
  'three',
  '3',
  index: 5,
  input: "Game three one:3.",
  groups: { word: 'three', digit: '3' },
  indices: {
    0: [6,17],
    1: [12,15],
    2: [16,17],
    groups: { 
      digit: [16, 17],
      word: [12, 15]
    }
  }
]
```

[浏览器对 RegExp 匹配索引特性的支持目前是有限的](https://caniuse.com/mdn-javascript_builtins_regexp_hasindices)(2021 年 1 月使用率约为 79%)。在 Node.js 中，您可以使用`--harmony-regexp-match-indices`标志来启用该特性，但是默认情况下它是禁用的。

# 全部的

多亏了 TC39 团队，已经辉煌的 JavaScript 生态系统又增添了新的一年的精彩特性。

希望你喜欢这篇关于 2022 年 JavaScript 和**新事物的介绍，请点击**阅读更多编程文章🦄。

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*