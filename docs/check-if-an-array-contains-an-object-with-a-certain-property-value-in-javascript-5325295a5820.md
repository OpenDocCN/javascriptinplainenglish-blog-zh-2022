# 在 JavaScript 中检查数组是否包含具有特定属性值的对象

> 原文：<https://javascript.plainenglish.io/check-if-an-array-contains-an-object-with-a-certain-property-value-in-javascript-5325295a5820?source=collection_archive---------6----------------------->

![](img/77d6656b956962e772d6bc4462a0ec80.png)

Photo by [Viktor Forgacs](https://unsplash.com/@sonance?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，有几种方法可以检查数组是否包含具有特定属性值的对象。一种选择是使用 Array.prototype.find()方法，该方法返回数组中满足所提供测试函数的第一个元素。

例如，假设我们有一个表示不同用户的对象数组，我们想检查该数组是否包含名为“John”的用户:

```
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
  { id: 3, name: "John" },
  { id: 4, name: "Jane" },
];

const john = users.find((user) => user.name === "John");
if (john) {
  console.log("John is in the array!");
} else {
  console.log("John is not in the array.");
}
```

另一种选择是使用 Array.prototype.some()方法，该方法返回一个布尔值，表明数组中是否至少有一个元素满足提供的测试函数。

例如，我们可以使用 some()方法来检查数组中是否包含名为“John”的用户，如下所示:

```
const containsJohn = users.some((user) => user.name === "John");

if (containsJohn) {
  console.log("The array contains a user with the name John!");
} else {
  console.log("The array does not contain a user with the name John.");
}
```

这两种方法都允许您使用任何想要的测试函数来检查数组中是否存在具有特定属性值的对象。例如，您可以使用一个函数来检查是否存在具有特定 id 的对象，或者您想要检查的任何其他属性值。

除了这些内置的数组方法，您还可以使用循环来手动迭代数组，并检查是否存在具有特定属性值的对象。

例如，您可以使用 for-of 循环来检查数组中是否包含名为“John”的用户，如下所示:

```
let containsJohn = false;

for (const user of users) {
  if (user.name === "John") {
    containsJohn = true;
    break;
  }
}
if (containsJohn) {
  console.log("The array contains a user with the name John!");
} else {
  console.log("The array does not contain a user with the name John.");
}
```

无论选择哪种方法，都可以很容易地在 JavaScript 中检查数组是否包含具有某个属性值的对象。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

*****想扩大你的软件创业规模*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***