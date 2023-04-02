# 如何在 JavaScript 中实现动态 Getters 和 Setters

> 原文：<https://javascript.plainenglish.io/how-to-implement-dynamic-getters-and-setters-in-javascript-2a40b4bb88e6?source=collection_archive---------2----------------------->

## 如何用 JavaScript 实现动态 getters 和 setters 的指南。

![](img/f34d71870cbf86904c1430473b551a30.png)

Photo by [Amelie & Niklas Ohlrogge](https://unsplash.com/@pirye?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望动态地向 JavaScript 对象添加 getters 和 setters。

在本文中，我们将看看如何用 JavaScript 实现动态 getters 和 setters。

# 使用代理

JavaScript 附带了`Proxy`构造函数，允许我们创建一个对象，它是另一个对象的门面。

例如，我们可以通过编写以下代码向它添加一个动态 getter:

```
const original = {
  "foo": "bar"
};
const proxy = new Proxy(original, {
  get(target, name, receiver) {
    let rv = Reflect.get(target, name, receiver);
    if (typeof rv === "string") {
      rv = rv.toUpperCase();
    }
    return rv;
  }
});
console.log(original.foo)
console.log(proxy.foo);
```

我们用`foo`属性创建了`original`对象。

然后我们使用`Proxy`构造函数创建一个带有`original`对象的代理。

我们用`get`方法传递给它一个对象，以获得我们想要用`Reflect.get`方法修改返回值的属性。

Ir 返回属性名设置为`name`的`original`对象的值。

如果`rv`返回值是一个字符串，我们返回`rv`作为大写字母。

因此，第一个控制台日志记录了`'bar'`，但是第二个日志记录了`'BAR'`。

我们可以通过将`set`方法添加到我们作为`Proxy`构造函数的第二个参数传入的对象中来添加 setter。

例如，我们可以写:

```
const original = {
  "foo": "bar"
};
const proxy = new Proxy(original, {
  get(target, name, receiver) {
    let rv = Reflect.get(target, name, receiver);
    if (typeof rv === "string") {
      rv = rv.toUpperCase();
    }
    return rv;
  },
  set(target, name, value, receiver) {
    if (!Reflect.has(target, name)) {
      console.log(`Setting non-existent property '${name}', initial value: ${value}`);
    }
    return Reflect.set(target, name, value, receiver);
  }
});
proxy.baz = 'abc'
console.log(original.foo)
console.log(proxy.foo);
```

我们添加了`set`方法，让我们修改如何修改`original`对象的属性。

我们调用`Reflect.has`方法来检查`original`对象是否具有属性`name`。

如果没有，我们会记录一条消息。

否则，我们调用`Reflect.set`将`name`属性设置为给定的`value`并返回结果。

因此，当我们试图设置`proxy.baz`属性时，我们得到:

```
'Setting non-existent property ‘baz’, initial value: abc’
```

其余的控制台日志和以前一样。

# 结论

我们可以使用 JavaScript 代理按照我们想要的方式修改 getters 和 setters。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***