# 您可能错过的 10 个 JavaScript 新特性

> 原文：<https://javascript.plainenglish.io/10-javascript-new-features-you-might-have-missed-1c6e71fa44c0?source=collection_archive---------7----------------------->

## 让我们来看看 ES11 的亮点。

![](img/8d722c387d17fc5eefc90520b2e26381.png)

很难跟上 ECMAScript 规范持续呈现给我们的相对较新的特性。让我们来看看 ES11 的亮点。

# BigInt

`BigInt`是一个[原语包装对象](https://developer.mozilla.org/en-US/docs/Glossary/Primitive#primitive_wrapper_objects_in_javascript)，用于表示和操作[原语](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) `bigint`值——这些值[太大](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)而无法由`number` [原语](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)表示。

```
const previouslyMaxSafeInteger = 9007199254740991nconst alsoHuge = BigInt(9007199254740991)
// ↪ 9007199254740991nconst hugeString = BigInt("9007199254740991")
// ↪ 9007199254740991nconst hugeHex = BigInt("0x1fffffffffffff")
// ↪ 9007199254740991nconst hugeOctal = BigInt("0o377777777777777777")
// ↪ 9007199254740991nconst hugeBin = BigInt("0b11111111111111111111111111111111111111111111111111111")
// ↪ 9007199254740991n
```

# 零化合并算子(？？)

无效合并运算符(`??`)是一种逻辑运算符，当其左侧操作数为`[null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)`或`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`时，返回其右侧操作数，否则返回其左侧操作数。

```
const nullValue = null;
const emptyText = ""; // falsy
const someNumber = 42;const valA = nullValue ?? "default for A";
const valB = emptyText ?? "default for B";
const valC = someNumber ?? 0;console.log(valA); // "default for A"
console.log(valB); // "" (as the empty string is not null or undefined)
console.log(valC); // 42
```

# 可选链接

可选链接是一种简单而可行的舒适方式，可以让生活变得更简单。

这个特性允许您使用处理空值或未定义值的快捷方式来导航对象和函数链。

```
box = {
  innerBox: {},
  nullFunction: **function**() { **return** **null**; },
  *// non-existent method foo() and members bar*
}
*// with optional chaining:*
**if** (box?.innerBox?.foo){ }*// navigate object graph safely*
*// old style without optional chaining:*
**if** (box.innerBox && box.innerBox.foo){ }
*//also works for functions:*
box.nullFunction()?.foo
*// and nonexistent methods and members:*
box?.foo() && box?.bar
```

# globalThis

全局`globalThis`属性包含全局`this`值，类似于[全局对象](https://developer.mozilla.org/en-US/docs/Glossary/Global_object)。

```
function canMakeHTTPRequest() {
 return typeof globalThis.XMLHttpRequest === ‘function’;
}console.log(canMakeHTTPRequest());
// expected output (in a browser): true
```

# 字符串.原型.匹配

ES11 规范为字符串原型增加了另一项技术:matchAll。这种技术将正则表达式应用于字符串实例，并在每次命中时返回一个迭代器。例如，假设您需要为一个单词以 t 或 t 开头的每个位置过滤一个字符串。

```
**let** text = "The best time to plant a tree was 20 years ago. The second best time is now.";
**let** regex = /(?:^|\s)(t[a-z0-9]\w*)/gi; *// matches words starting with t, case insensitive*
**let** result = text.matchAll(regex);
**for** (match of result) {
  console.log(match[1]);
}
```

# 动态`import()`

它引入了一种新的类似函数形式的`import`，与静态的`import`相比，它释放了新的能力。

```
**let** asyncModule = await **import**('/lib/my-module.ts');
```

# Promise.allSettled()

`Promise.allSettled()`方法返回一个承诺，该承诺在所有给定的承诺履行或拒绝后解决，并带有一个对象数组，每个对象描述每个承诺的结果。

```
**let** promise1 = **Promise**.resolve("OK");
**let** promise2 = **Promise**.reject("Not OK");
**let** promise3 = **Promise**.resolve("After not ok");
**Promise**.allSettled([promise1, promise2, promise3])
    .**then**((results) => console.log(results))
    .**catch**((err) => console.log("error: " + err));
```

# Export *语法

这个特性增加了从一个模块到`export *`的能力。您本来可以从另一个模块中`import *`，但是现在您可以用相同的语法导出

```
**Export** * **from** '/dir/another-module.js'
```

# 顶级 Await 运算符

JavaScript 中使用异步函数已经有一段时间了。之前，我们无法在异步函数之外声明 await 关键字，这导致了一个错误。然而，我们现在可以在异步函数和类之外声明 await 操作符，这解决了同步问题。

```
import {getUser} from ‘. /data/User’ let user=await getUser();
```

这个话题到此为止。感谢您的阅读。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于**[***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**