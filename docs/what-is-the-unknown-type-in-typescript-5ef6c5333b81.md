# TypeScript 中的“未知”类型是什么？

> 原文：<https://javascript.plainenglish.io/what-is-the-unknown-type-in-typescript-5ef6c5333b81?source=collection_archive---------4----------------------->

## 在 TypeScript 中，任何值都可以赋给“未知”类型，但是如果没有类型断言，“未知”只能赋给它本身

![](img/a0cc9ccec83f8af00eaa8664726f3c75.png)

Photo by [Milad Fakurian](https://unsplash.com/@fakurian?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/abstract?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

不久前，在 3.0 版本中，TypeScript 在其工具包中引入了一个新的`unknown`类型，但是这个类型做什么，更具体地说，我们应该在什么时候使用它？

本文将研究这种“新”类型，以便更好地理解它的目标。

我们也将始终如一地把它与它的兄弟类型`any`进行比较；如果你还不熟悉它，看看这篇的文章，在那里我们已经更详细地讨论过了。

# 未知类型是什么？

在[类型脚本中，](https://www.geeksforgeeks.org/introduction-to-typescript/)任何值都可以赋给`unknown`类型，但是没有类型断言，`unknown`只能赋给自身和`any`类型。类似地，如果不首先声明或限制为更精确的类型，就不允许对类型设置为`unknown`的值进行任何操作。

我们可以给一个`unknown`类型的变量赋值，就像我们给一个`any`类型的变量赋值一样。与 in 的情况不同，我们不能访问`unknown`类型变量的属性，也不能调用或构造它们。

此外，`unknown`值只能分配给`any`和`unknown`类型的变量。

给类型`unknown`的变量赋值:

```
let val: unknown;

val = true; // Fine
val = 42; // Fine
val = "hey!"; // Fine
val = []; // Fine
val = {}; // Fine
val = Math.random; // Fine
val = null; // Fine
val = undefined; // Fine
val = () => { console.log('Hey again!'); }; // Fine
```

将各种类型的值赋给类型`any`的变量:

```
let val: any;

val = true; // Fine
val = 42; // Fine
val = "hey!"; // Fine
val = []; // Fine
val = {}; // Fine
val = Math.random; // Fine
val = null; // Fine
val = undefined; // Fine
val = () => { console.log('Hey again!'); }; // Fine
```

将类型`unknown`的值赋给其他类型的变量:

```
let val: unknown;

const val1: unknown = val; // Fine
const val2: any = val; // Fine
const val3: boolean = val; // Will throw error
const val4: number = val; // Will throw error
const val5: string = val; // Will throw error
const val6: Record<string, any> = val; // Will throw error
const val7: any[] = val; // Will throw error
const val8: (...args: any[]) => void = val; // Will throw error
```

# 使未知类型更加具体

我们可以缩小一个`unknown`类型值的可能结果。

让我们看看下面的例子:

```
const isNumbersArray = (val: unknown): val is number[] => (
  Array.isArray(val) && val.every((element) => typeof element === 'number')
);
```

```
const unknownValue: unknown = [12, 2, 8, 17, 14];if (isNumbersArray(unknownValue)) {
  const sum = unknownValue.reduce((accumulator, currentElement) => (accumulator + currentElement) , 0); console.log(sum);
}
```

之前，的类型是`unknown`；然而，在使用`unknownValue`作为参数调用`isNumbersArray`之后，我们得出结论，`unknownValue`的类型实际上是数字的**数组的类型。**

# 什么时候我们需要使用未知类型？

我们可能想要使用`unknown`类型的一个特殊场景是我们需要从本地存储中获取一些东西。

在存储之前，所有`localStorage` API 项目都被**序列化。然而，我们的用例包含了在反序列化**之后检索到的条目的**值。**

通过利用`unknown`类型，我们将能够打出反序列化项目的类型，而不是简单地使用`any`注释。

```
type ResultType =
  | { success: true; value: unknown }
  | { success: false; error: Error };
```

```
const retrieveItemFromLocalStorage = (key: string): ResultType => {
  const item = localStorage.getItem(key); if (!item) {
    // The item does not exist, thus return an error
    return {
      success: false,
      error: new Error(`Item with key "${key}" does not exist`),
    };
  } let value: unknown; try {
    value = JSON.parse(item);
  } catch (error) {
    // The item is not a valid JSON value, thus return an error
    return {
      success: false,
      error,
    };
  } // Everything's fine, thus return a successful result
  return {
    success: true,
    value,
  };
}
```

`ResultType`是一个[标记的联合类型](https://mariusschulz.com/blog/tagged-union-types-in-typescript)(也称为区别联合类型)。你可能会遇到`Maybe`、`Option`或`Optional`，它们在其他语言中是它的对等词。

我们使用`ResultType`清晰地模拟操作的成功或不成功的结果。

这里有一个我们如何使用`retrieveItemFromLocalStorage`函数的例子:

```
const result = retrieveItemFromLocalStorage("cached-blogs");

if (result.success) {
  // We've narrowed the `success` property to `true`,
  // so we can access the `value` property
  const cachedBlogs: unknown = result.value;

  if (isArrayOfBlogs(cachedBlogs)) {
    // We've narrowed the `unknown` type to `Array<Blog>`,
    // so we can safely use our cached `cachedBlogs` array as we would
    console.log('Cached blogs:', cachedBlogs);
  }
} else {
  // We've narrowed the `success` property to `false`,
  // so we can access the `error` property
  console.error(result.error);
}
```

# 摘要

我希望你喜欢这篇文章，并对`unknown`类型与`any`类型的不同之处有了更多的了解，以及我们通常在实际项目中使用它的时间。

欢迎在下面的评论区留下你的想法。

干杯！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***