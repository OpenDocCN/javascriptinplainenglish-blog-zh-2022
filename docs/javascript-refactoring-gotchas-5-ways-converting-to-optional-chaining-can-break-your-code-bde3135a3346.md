# JavaScript 重构陷阱:转换为可选链接的 5 种方式会破坏代码

> 原文：<https://javascript.plainenglish.io/javascript-refactoring-gotchas-5-ways-converting-to-optional-chaining-can-break-your-code-bde3135a3346?source=collection_archive---------16----------------------->

![](img/614d5b434f6beacd4ff9c25f1feb42c0.png)

**[**可选链接**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) **运算符** `**.?**` **在对象可用时返回对象属性的值，否则返回** `**undefined**` **。**它类似于标准的`.`链接操作符，增加了检查对象是否被定义(即不是 [nullish](https://developer.mozilla.org/en-US/docs/Glossary/Nullish) )。**

**可选的链接操作符让你**编写简洁安全的连接对象链**，当这些对象中的一些可以是`null`或`undefined`时。在 ES2020 中引入可选链接之前，`&&`操作符通常用于检查对象是否可用(`obj && obj.value`)。**

**您通常可以使用可选的链接模式来简化现有检查:**

*   **`obj && obj.property`变成了`obj?.property`**
*   **`obj != null && obj.property`变成了`obj?.property`**
*   **`obj != null ? obj.property : undefined`变为`obj?.property`**
*   **`arr && arr[i]`变为`arr?.[i]`**
*   **`f && f()`变为`f?.()`**
*   **等等。**

**但是，在某些情况下，重构为可选链接会导致错误:**

# **空值的可选链接短路，但不包括其他假值**

**当`a && a.b`替换为`a?.b`时，可以有 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 值的类型的执行被改变。这意味着表达式的结果值和类型可以随可选链接而不同。**

**以下代码片段显示了一些示例:**

```
function test(value) {
    console.log(`${value && value.length}, ${value?.length}`);
}test(undefined);       // undefined, undefined
test(null);            // null, undefined
test(true);            // undefined, undefined
test(false);           // false, undefined
test(1);               // undefined, undefined
test(0);               // 0, undefined
test({});              // undefined, undefined
test([]);              // 0, 0
test({ length: "a" }); // a, a
test('');              // , 0
test(NaN);             // NaN, undefined
```

**空字符串是 falsy，但不是 [nullish](https://developer.mozilla.org/en-US/docs/Glossary/Nullish) ，可能会特别成问题。下面是一个引入可选链接会导致问题的示例:**

```
// without optional chaining
if (s && s.length === 0) {
  // not called for the empty string 
  // (e.g., legacy code that works this way)
}// with optional chaining
if (s?.length === 0) {
  // called for the empty string 
  // (potentially introducing undesired behavior)
}
```

# **可选链接将 null 的结果更改为 undefined**

**用 null 调用`a?.b`时，结果是`undefined`。但是，用`a && a.b`，结果是`null`。**

# **可选链接会影响调用的数量，并产生副作用**

**例如，考虑改变**

```
f() && f().a;
```

**到…里面**

```
f()?.a;
```

**同`&&`，`f`叫一两遍。然而，可选链接`f`只被调用一次。如果`f`有副作用，这个副作用会被调用不同的次数，潜在地改变行为。这种行为不仅适用于函数和方法调用，也适用于可能有副作用的 getters。**

# **TypeScript 不支持“void”类型的可选链接**

**[TypeScript 不支持](https://github.com/microsoft/TypeScript/issues/35850) `[void](https://github.com/microsoft/TypeScript/issues/35850)`事件的可选链接，尽管相应的 JavaScript 代码可以工作。**

```
type Input = void | {
    property: string
};function f(input: Input) {
    // this works:
    console.log(input && input.property);
    // this breaks because void is not undefined in TypeScript:
    console.log(input?.property);
}
```

# **旧的浏览器和 JavaScript 引擎不支持可选链接**

**可选链接是 ES2020 的一项功能。它在所有现代浏览器和 Node 14+上都受支持，但对于较旧的浏览器和 Node 版本，可能需要 transpilation】兼容性)。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***