# 什么是新的 Object.hasOwn()方法，为什么我们应该使用它而不是 object . prototype . hasownproperty()方法

> 原文：<https://javascript.plainenglish.io/what-is-object-hasown-and-why-should-we-use-it-over-object-prototype-hasownproperty-53b5acc2247a?source=collection_archive---------7----------------------->

`*Object.hasOwn()*` *意在替代* `[*Object.hasOwnProperty(*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)*)*` *。在这篇文章中，我将探讨他们的不同之处，以及为什么从现在开始应该使用* `*Object.hasOwn()*` *。*

![](img/1fe3c93cfdd2c7a20b47d14ac580b732.png)

JavaScript

`Object.hasOwn()`是一个新的静态方法，如果指定的对象将指定的属性作为自己的属性，则返回 true。如果该属性是继承的，或者不存在，则该方法返回 false。`hasOwnProperty()`方法还返回一个布尔值，表明对象是否将指定的属性作为自己的属性。

比如说:

```
const person = { name: 'John' };
console.log(Object.hasOwn(person, 'name'));// true
console.log(Object.hasOwn(person, 'age'));// falseconsole.log(person.hasOwnProperty('name'));// true
console.log(person.hasOwnProperty('age'));// falseconst person2 = Object.create({gender: 'male'});
console.log(Object.hasOwn(person2, 'gender')); // false
console.log(person.hasOwnProperty('gender')); //false

// gender is not an own property of person, it exist on the person2 prototype
```

所以，在观察了`Object.hasOwn()`和`Object.hasOwnProperty()`的动作后，它们看起来很像。那么，我们为什么要使用`Object.hasOwn()`而不是`Object.hasOwnProperty()`？因为它也适用于使用`Object.create(null)`创建的对象和覆盖了继承的`hasOwnProperty()`方法的对象。虽然可以通过调用外部对象上的`Object.prototype.hasOwnProperty.call(<object reference>, <property name>)`来解决这类问题，但是`Object.hasOwn()`克服了这些问题，因此是首选。

让我们来看看一些例子:

1.覆盖继承的`hasOwnProperty()`

```
let person = {
 hasOwnProperty: function() {
 return false;
 },
 age: 35
 };

 console.log(Object.hasOwn(person, 'age')); // true
 console.log(person.hasOwnProperty('age')); // false
```

2.使用`Object.create(null)`创建的对象

```
let person = Object.create(null);
person.age = 35;

if (Object.hasOwn(person, ‘age’)) {
  console.log(person.age); // true
  //works regardless of how the object was created
}if (person.hasOwnProperty(‘age’)){ // throws error —  person.hasOwnProperty is not a function
 console.log(‘hasOwnProperty’ + person.age);
}
```

我希望这篇文章能帮助你理解在 JavaScript 中使用`Object.hasOwn()`比使用`hasOwnProperty()`方法的好处。如果你觉得这篇文章有帮助，我会感谢下面的一些掌声。(:

您也可以关注我以获得更多类似的文章(:

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*