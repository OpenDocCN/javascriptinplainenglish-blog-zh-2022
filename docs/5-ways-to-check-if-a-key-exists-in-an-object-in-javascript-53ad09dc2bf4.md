# JavaScript 中检查对象中是否存在键的 5 种方法

> 原文：<https://javascript.plainenglish.io/5-ways-to-check-if-a-key-exists-in-an-object-in-javascript-53ad09dc2bf4?source=collection_archive---------2----------------------->

![](img/f1cfa8a83bf0db8565be4b4b0fae4a9c.png)

Photo by [Walling](https://unsplash.com/@walling?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 使用“in”运算符

如果指定的属性存在于指定的对象或其原型链中，那么`in`操作符返回`true`，否则返回`false`。

```
const app = { name: 'Instagram', type: 'Social Media' };
console.log('name' in app); // true
console.log('release_date' in app); // false
```

# 使用 Reflect.has()方法

[Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect) 是一个内置对象，为 JavaScript 操作提供一些实用方法。如果指定的属性存在于指定的对象或其原型链中，该对象的`has()`方法返回`true`，否则返回`false`。语法是:`Reflect.has(targetObject, propertyKey);`

让我们在一个例子中使用它。

```
const app = { name: 'Instagram', type: 'Social Media' };
console.log(Reflect.has(app, 'name')); // true
console.log(Reflect.has(app, 'release_date')); // false
```

# 使用 hasOwnProperty()方法

该方法存在于对象原型中。所以任何不是用`Object.create(null)`创建的对象都可以访问这个方法。如果指定的属性存在于对象中(不是继承的)，该方法返回`true`，否则返回`false`。

```
const app = { name: 'Instagram', type: 'Social Media' };
console.log(app.hasOwnProperty('type')); // true
console.log(app.hasOwnProperty('founder_name')); // false
```

# 通过访问属性并将其与“未定义”进行比较

如果我们访问对象上不存在的任何属性，它返回`undefined`。这样，我们可以访问该属性，并将其值与`undefined`进行比较，以了解它是否存在。

```
const app = { name: 'Instagram', type: 'Social Media' };
console.log(app['name'] === undefined); // false
console.log(app['founder_name'] === undefined); // true

// or simply use an if block without comparing to undefined
if (app['founder_name']) {
    // do your work
}
```

当一个属性存在于对象中并且值为`undefined`时，我们不能用这种方法来确定属性的存在。

```
const auth = { token: undefined };
console.log(auth['token'] === undefined); // true
console.log(auth['timestamp'] === undefined); // true
```

# Object.hasOwn()方法(ES2022 更新)

如果指定的属性存在于对象中(不是继承的)，该方法返回`true`，否则返回`false`。

```
const app = { name: 'Instagram', type: 'Social Media' };
console.log(Object.hasOwn(app, 'type')); // true
console.log(Object.hasOwn(app, 'founder_name')); // false
```

除了`hasOwnProperty()`和`hasOwn()`方法，其他三种方法在继承属性的情况下都很好。让我们看一个例子。

```
function square(side) {
    this.side = side;
}

square.prototype.getArea = function () {
    return Math.pow(this.side, 2);
}

const sq = new square(5);
console.log(sq); // { side: 5 };
console.log(sq.getArea()); // 25
/*
 Here "side" will be part of own object whereas
 "getArea" will be inherited through prototype chain.
*/

// checking with 'in'
console.log('side' in sq); // true
console.log('getArea' in sq); // true

// checking with 'Reflect.has()'
console.log(Reflect.has(sq, 'side')); // true
console.log(Reflect.has(sq, 'getArea')); // true

// checking with 'hasOwnProperty()'
console.log(sq.hasOwnProperty('side')); // true
console.log(sq.hasOwnProperty('getArea')); // false

// comparing with 'undefined'
console.log(sq['side'] !== undefined); // true
console.log(sq['getArea'] !== undefined); // true

// checking with 'hasOwn()'
console.log(Object.hasOwn(sq, 'side')); // true
console.log(Object.hasOwn(sq, 'getArea')); // false
```

# 结论

前两种方法(`in`操作符和`Reflect.has()`方法)更为突出，而其他三种则有一些限制。

*   顾名思义，`hasOwnProperty()`和`hasOwn()`方法只对对象自身的属性有效，对继承的属性无效。
*   用`Object.create(null)`创建的对象不能使用`hasOwnProperty()`方法。
*   “与`undefined`比较”的方法工作良好，除非指定的属性存在，但值为`undefined`。

# 你可能也喜欢

*   [JavaScript 中的地图，当它是比对象更好的选择时](https://jscurious.com/map-in-javascript-and-how-it-is-better-than-object/)
*   [JavaScript 设置对象存储唯一值](https://jscurious.com/javascript-set-object-to-store-unique-values/)
*   [使用 JavaScript 中的通知 API 发送推送通知](https://jscurious.com/the-notification-api-in-javascript/)
*   [用 JavaScript 中的 HTMLAudioElement API 播放音频](https://jscurious.com/play-audio-with-htmlaudioelement-api-in-javascript/)
*   [JavaScript 中的 Object.defineProperty()方法](https://jscurious.com/object-defineproperty-method-in-javascript/)
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [JavaScript 中承诺的简要指南](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript 获取 API 以发出 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20+ JavaScript 速记编码技巧和窍门](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的时间:)*
***阿米塔夫·米什拉***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****