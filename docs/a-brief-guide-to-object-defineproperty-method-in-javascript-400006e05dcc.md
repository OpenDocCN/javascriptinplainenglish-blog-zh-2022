# JavaScript 中 Object.defineProperty()方法的简要指南

> 原文：<https://javascript.plainenglish.io/a-brief-guide-to-object-defineproperty-method-in-javascript-400006e05dcc?source=collection_archive---------6----------------------->

![](img/fb5ee4ef84b3fb9aba4c645bcf694a43.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

方法添加或修改一个对象的属性。我们可以使用这个方法来提供关于对象属性的额外配置细节，并控制它们的行为。语法是:

```
Object.defineProperty(object, prop, descriptor);
```

*   `object`–我们想要定义属性的任何对象。
*   `prop`–要添加或修改的属性的名称。
*   `descriptor`–这是一个指定属性配置细节的对象。

让我们探索一下可以在描述符对象中使用的属性以及它们的作用。

任何对象中都有两种类型的属性，一种是有值的数据属性，另一种是由 [getter-setter](https://jscurious.com/javascript-getters-and-setters/) 函数描述的访问器属性。数据和访问器属性的描述符属性是不同的，我们不能一起使用它们。

# 通用描述符属性

数据和访问器属性有两个共同的描述符属性，它们如下:

## 可配置的

它指示属性是否可重新配置(使用`defineProperty()`重新定义)或删除。如果没有设置，默认为`false`。如果设置为`false`，我们不能删除这个属性，如果我们试图重新定义它，它会抛出一个错误。

```
const ob = { x: 20 };
Object.defineProperty(ob, "x", { configurable: false });
delete ob.x;
console.log(ob); // { x: 20 }
// re-define property x
Object.defineProperty(ob, "x", { configurable: true });
// TypeError: Cannot redefine property: x
```

## 可列举的

它指示在枚举对象的属性期间是否出现该属性。如果没有设置，默认为`false`。如果设置为`false`，该属性不会出现在`Object.keys`、`Object.values`、`Object.entries`、`Object.assign`、spread 运算符、`for...in`循环等方法中。

```
const ob = { x: 20, y: 30, z: 40 };
Object.defineProperty(ob, "x", { enumerable: false });console.log(Object.keys(ob)); // ['y', 'z']
console.log(Object.assign({}, ob)); // { y: 30, z: 40 }
console.log({ ...ob }); // { y: 30, z: 40 }
for (const key in ob) {
  console.log(key); // y z
}
```

# 数据描述符属性

数据描述符有两个名为`value`和`writable`的属性。让我们来探索它们。

## 价值

它设置属性的值。如果没有提供，则默认为`undefined`。

```
const ob = { x: 20 };
Object.defineProperty(ob, "x", { value: 40 });
Object.defineProperty(ob, "y", { value: 55 });
console.log(ob); // { x: 40, y: 55 }
```

## 可写的

它指示属性值是否可以使用赋值运算符(=)进行更改。如果没有设置，默认为`false`。如果设置为`false`，属性值不能使用赋值操作符更改，但仍可使用`defineProperty()`方法更改。

```
const ob = { x: 20 };
Object.defineProperty(ob, "x", { writable: false });
ob.x = 100;
console.log(ob.x); // 20
Object.defineProperty(ob, "x", { value: 55 });
console.log(ob.x); // 55
```

> 如果在创建对象时或通过点/括号符号添加了任何属性，那么可配置、可枚举和可写的默认值将被设置为`true`。

# 访问者描述符属性

访问器描述符还有两个名为`get`和`set`的属性。让我们来探索它们。

## 得到

它用于创建一个 getter 函数。默认值为`undefined`。

```
const ob = { x: 10 };
Object.defineProperty(ob, "x2", {
  get: function () {
    return this.x ** 2;
  },
});console.log(ob.x2); // 100
```

## 设置

它用于创建 setter 函数。默认值是`undefined`。

```
const ob = {};
Object.defineProperty(ob, "x", {
  get: function () {
    return this._x;
  },
  set: function(value) {
    this._x = value;
  }
});console.log(ob.x); // undefined
ob.x = 99;
console.log(ob.x); // 99
```

如果我们混合了数据和访问器描述符属性，它会抛出一个错误。

```
const ob = {};
Object.defineProperty(ob, "x", {
  value: 20,
  get: function () {
    return this._x;
  }
});// TypeError: Invalid property descriptor. 
// Cannot both specify accessors and a value or writable attribute
```

> 如果在`defineProperty()`方法中没有提到数据和访问器属性，那么默认情况下该属性被视为数据属性。

到目前为止，我们已经讨论了如何设置属性描述符。现在让我们看看如何查看任何属性的描述符。

# object . getownpropertydescriptor()方法

该方法将对象及其属性名作为参数，并返回各自的属性描述符对象。

```
const ob = { x: 20 };
console.log(Object.getOwnPropertyDescriptor(ob, "x"));
/*
{
  configurable: true,
  enumerable: true,
  value: 20,
  writable: true
}
*/
ob.y = 30;
console.log(Object.getOwnPropertyDescriptor(ob, "y"));
/*
{
  configurable: true,
  enumerable: true,
  value: 30,
  writable: true
}
*/
Object.defineProperty(ob, "z", {
  value: 40,
  writable: true,
});
console.log(Object.getOwnPropertyDescriptor(ob, "z"));
/*
{
  configurable: false,
  enumerable: false,
  value: 40,
  writable: true
}
*/
```

# 你可能也喜欢

*   [JavaScript 中的地图以及它如何优于 Object](https://jscurious.com/map-in-javascript-and-how-it-is-better-than-object/)
*   [JavaScript 设置对象存储唯一值](https://jscurious.com/javascript-set-object-to-store-unique-values/)
*   [JavaScript 中检查对象中是否存在键的不同方法](https://jscurious.com/different-ways-to-check-if-a-key-exists-in-an-object/)
*   【Object.freeze()、Object.seal()和 Object.preventExtensions( )的区别
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [JavaScript 中承诺的简要指南](https://jscurious.com/a-brief-guide-to-promises-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [20+ JavaScript 速记编码技巧](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的时间:)*
***阿米塔夫·米什拉***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*