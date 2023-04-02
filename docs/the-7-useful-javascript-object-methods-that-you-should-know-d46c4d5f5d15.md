# 你应该知道的 7 个有用的 JavaScript 对象方法

> 原文：<https://javascript.plainenglish.io/the-7-useful-javascript-object-methods-that-you-should-know-d46c4d5f5d15?source=collection_archive---------3----------------------->

## JavaScript 中需要了解的强大对象方法列表。

![](img/b520b0cbf12e02ab028412d3513deab6.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是当今非常强大的编程语言。你可以用它来做网页开发，移动开发，游戏开发，机器学习，甚至一些 AI。

像所有的编程语言一样，JavaScript 也有自己的数据类型，允许我们处理数据。对象是我们可以在语言中使用的一种重要的数据类型。

最重要的是，JavaScript 对象有很多强大的方法，我们可以访问这些方法来获取信息。这就是为什么在本文中，我们将学习一些作为开发人员应该知道的方法。所以让我们开始吧。

# 1.对象值方法

JavaScript 中的方法`Object.values()`是一个非常有用的对象方法，它允许您获取对象中的所有**值**。

您只需将对象名作为参数传递，然后该方法将返回一个包含该对象所有值的数组。

下面是一个代码示例，可以让您明白一些事情:

```
const userData = {
  name: "John",
  age: 25,
  isOnline: true
}
console.log(**Object.values(userData)**); //returns ["John", 25, true]
```

正如您在代码示例中看到的，我们只是将对象作为参数传递，然后我们得到一个包含所有值的数组。

# 2.对象条目方法

方法`Object.entries()`是 JavaScript 中您应该知道的另一个有用的对象方法。

这个方法返回一个多维数组，包含一个对象的键**和值**。您只需将对象名作为方法的参数进行传递。****

**下面是代码示例:**

```
const userData = {
  name: "John",
  age: 25,
  isOnline: true
}
console.log(**Object.entries(userData)**);
//returns: [["name", "John"], ["age", 25], ["isOnline", true]]
```

*****注意*** *:方法* `*Object.entries()*` *返回一个数组，该数组只包含它自己的可枚举的字符串键属性对。它不从对象的原型链返回属性。***

# **3.对象键方法**

**方法`Object.keys()`返回一个数组，该数组包含您作为参数传递的对象中的所有键。**

**查看下面的代码示例:**

```
const person = {
  name: "James",
  age: 28,
  available: false
}
console.log(**Object.keys(person)**);
//returns: ["name", "age", "available"]
```

**如您所见，该方法允许我们获取对象的键数组。现在，您可以轻松地使用任何数组方法来访问或遍历这些键。**

**例如，由于对象不接受长度属性，您可以使用方法`Object.keys()`来获得一个键数组，然后对它使用长度属性。**

**这是获取对象长度或计算对象内部键数的好方法。**

**下面是一个代码示例:**

```
Object**.**keys(person)**.length;** //returns 3
```

# **4.该对象冻结方法**

**方法`Object.freeze()`允许你冻结一个作为参数传递给它的对象。这意味着您将无法更新或添加新属性到对象中。**

**该方法只是防止对象中的数据突变。看看下面的代码示例:**

```
const person = {
  name: "Alex",
  age: 35,
  available: true
}//Freezing the object
**Object.freeze(person);**//updating and adding new properties.
person.name = "John";
person.newProp = "Developer";**console.log(person);**
//returns {name: "Alex", age: 35, available: true}
```

**正如您在上面的代码中看到的，即使我们更新了对象`person`并添加了新的属性，它也没有改变，因为它已经被方法`Object.freeze()`冻结了。**

# **5.该物体密封方法**

**JavaScript 中的方法`Object.seal()`阻止向对象添加新属性。它类似于`Object.freeze()`，唯一的区别是它允许你更新和改变对象内部的属性。**

**查看下面的代码示例:**

```
const userData = {
  name: "Brad",
  age: 28,
  isOnline: false
}//Using the method
**Object.seal(userData);**//updating a property.
userData.isOnline = true;//Adding a property.
userData.active = false;console.log(userData);
//returns **{name: "Brad", age: 28, isOnline: true}**
```

**如你所见，我们能够将属性`isOnline`更新为真而不是假。但是当我们给对象添加一个新属性`.active`时，什么也没发生。这是因为方法`Object.seal()`阻止添加新属性。**

# **6.该对象创建方法**

**方法`Object.create()`是 JavaScript 中一个很棒的对象方法，允许您基于另一个现有对象的原型创建一个新对象。**

**让我们来看一个简单的代码示例，让您明白一些事情:**

```
const userData = {
  firstName: "Brad",
  lastName: "Traversy",
  age: 38,
  fullName(){
    return `${this.firstName} ${this.lastName}`;
  }
}//New Object
let newObject = **Object.create(userData)**;//Updating properties on new object.
newObject.firstName = "John";
newObject.lastName = "Doe";//We can also use the method fullName() of userData object in this new object.
newObject.**fullName()**; //returns John Doeconsole.log(newObject);
//returns {firstName: "John", lastName: "Doe"}
```

**因此，正如您在示例中看到的，方法`Object.create()`允许我们创建一个新对象，它具有`userData`对象的原型。让我们可以访问新对象中的所有属性和方法，这样我们就不用重复了。**

# **7.对象是()方法**

**方法`Object.is()`是另一个有用的 JavaScript 对象方法，它定义两个值是否相同。如果两个值相等，则返回 true。否则，它返回 false。**

**下面是语法的样子:**

```
**Object.is(val1, val2);**
```

**如您所见，该方法接受两个参数(要比较的值)。**

**查看下面的代码示例:**

```
Object.is(50, 50);        //true
Object.is('foo', 'bar'); //false
Object.is(foo, foo);    //true
```

# **结论**

**这是 JavaScript 中一些有用且重要的对象方法的列表，你应该知道。这些方法使你处理对象变得更加容易。所以你需要利用这一点，并在需要的时候在你的代码中使用它们。**

***感谢您阅读本文。此外，如果您发现我的内容有用，而您不是媒体会员，您可以在此处获取您的媒体会员资格*[](https://mehdiouss.medium.com/membership)**(媒体推荐链接)以无限制访问所有内容并支持我们作为作者。****

***[](https://mehdiouss.medium.com/membership) [## 通过我的推荐链接加入 Medium-Mehdi Aoussiad

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mehdiouss.medium.com](https://mehdiouss.medium.com/membership) 

**延伸阅读:**

[](/9-useful-front-end-web-developer-cheatsheets-to-save-time-2e1fe7495e8) [## 9 个有用的前端 Web 开发人员备忘单来节省时间

### 2022 年每个 web 开发人员都应该知道的惊人的备忘单。

javascript.plainenglish.io](/9-useful-front-end-web-developer-cheatsheets-to-save-time-2e1fe7495e8) [](/9-awesome-css-properties-that-you-probably-have-never-used-8cc4c385c3c6) [## 你可能从未用过的 9 个很棒的 CSS 属性

### 非常有用和有趣的 CSS 属性，你应该知道。

javascript.plainenglish.io](/9-awesome-css-properties-that-you-probably-have-never-used-8cc4c385c3c6) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。****