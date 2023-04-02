# JavaScript 工程:背后的科学

> 原文：<https://javascript.plainenglish.io/javascript-concepts-every-programmer-should-know-v1-0-2-cc87f541e05?source=collection_archive---------3----------------------->

## 软件工程

## 每个程序员都应该知道的 JavaScript 概念

![](img/e61b3044ea6e5d3ff132c29bbcbb642b.png)

Image Credit — Workato

最近我在 [*中写了关于 JS 的每个程序员都应该知道的 JavaScript 概念*](https://be-ja.medium.com/javascript-concepts-every-programmer-should-know-d04731fe7a7c) ，社区反馈非常好。

[](https://be-ja.medium.com/javascript-concepts-every-programmer-should-know-d04731fe7a7c) [## 每个程序员都应该知道的 JavaScript 概念

### JavaScript 是网络的头号编程语言，但除此之外，它也传播到许多平台…

be-ja.medium.com](https://be-ja.medium.com/javascript-concepts-every-programmer-should-know-d04731fe7a7c) 

我注意到相当多的开发人员和读者觉得这很有趣，所以为什么不就这个主题写一个系列呢，因为如果你正在学习 JavaScript 或者甚至在工作中使用它，有更多有用的概念可以掌握和利用。

所以，让我们开始吧！

# 原型

![](img/96504caab1b9682c89e538da9b6de0ea.png)

Image Credit — [helloimnik unsplash.com](https://unsplash.com/@helloimnik)

在 JavaScript 中，每个对象都从原型继承属性和方法。一个*原型*，简单来说，可以看作是一个默认情况下与所有函数和对象相关联的基础对象。

例如，一个`Date`对象继承了`Date.prototype`，一个`Array`继承了`Array.prototype`，一个`Person`对象将继承一个`Person.prototype`。

此外，所有这些对象都将继承`Object.prototype`

这对 JavaScript 的内部非常有用，我们知道它允许我们使用 JavaScript，但一般来说，理解我们使用的所有对象属性和方法都是在原型级别定义的是很好的。您可以通过简单地注销*原型*来验证这一点，如下所示:

```
# Log prototype on type
console.log(Array.prototype);# Log prototype on instance
let fruits = new Array("apple", "strawberry");
console.log(fruits.__proto__);
```

通过记录数组*的原型，*您应该能够看到它的属性和方法，比如:

```
keys: ƒ keys()
entries: *ƒ entries()* every: *ƒ every()* filter: *ƒ filter()* forEach: *ƒ forEach()* indexOf: *ƒ indexOf()
length: value
...*
```

如果您想知道`__proto__`属性是什么，它只是一个*获取器/设置器*，它定义在`Object.prototype`中，您也可以通过登录控制台来检查它。

# 班级

很多人不记得了，但是几年前，JavaScript 主要被视为一种*函数式语言(不是今天的函数式语言)*，主要是因为缺乏基于类的特性。没有定义类的方法，如果你想定义，你基本上是在滥用函数，你会得出这样的结果:

```
function Person(name) {
    this.name = name
}var person = new Person("Medium");
```

幸运的是，多亏了 ECMAScript 标准及其背后的委员会，在过去几年中引入了许多特性，其中之一就是*类。*

为了将属性和函数封装到一个单独的*模板*中，您应该像这样声明和使用一个类:

```
class Person {
    constructor(firstname, lastname) {
        this.firstname = firstname;
        this.lastname = lastname;
    }

    get name(){
        return this.firstname + this.lastname;
    }

    sayHello(){
        return `Hello my name is ${this.name}!`
    }
}let person = new Person("Medium", ".com");
let fullname = person.name;
let hello = person.sayHello();
```

显然还有很多课程，请务必查看:

*   [静态方法和属性](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#static_methods_and_properties)
*   [私有和公共字段](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#static_methods_and_properties)
*   [扩展类](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#field_declarations)

我强烈建议阅读 Mozilla 的 MDN Web Docs 上的课程。

# 通过值或引用传递

在每种编程语言中，都存在参数是按值传递还是按引用传递的问题。

JavaScript 主要是*按值传递，这意味着所有参数都是变量的副本。例如，在函数内对参数所做的任何更改都不会反映在函数外传递的变量中。*

上一段中的“*大多”*部分是因为对于原始值来说这是真的。例如，下面的代码说明了值是如何被复制的，并且对变量`firstname`和`lastname` 所做的更改不会反映在函数之外。

```
# Pass by value for primitives
function changeName(firstname, lastname) {
    firstname = "something";
    lastname = "else";
}let firstname = "First";
let lastname = "Last";changeName(firstname, lastname);console.log(firstname, lastname); // Still prints "First" and "Last"
```

对于复杂类型，这有一点不同——我们传递给函数的对象不会被复制，*或者它们的数据本身*。

简单地说，将一个对象传递给一个函数只会创建该引用的另一个副本，它指向该对象的内存部分。

```
# Passing an object results in copying the reference only
function changePerson(obj) {
     obj.name = "New Name";
     obj = {name: "Another New Name"};
}let person = {name: "Medium"};
changePerson(person);
console.log(person); // Prints {name: "New Name"}
```

在上面的例子中，在调用`changePerson`并传递`person`的时候，一个*新的引用将被创建*——这意味着任何*对该对象内的字段的改变，将在函数*之外被反映，但是分配一个新的对象 ie。*改变* `person` *所指，不起任何作用*。通过分配一个新的对象，我们分配了一个新的内存块，并且只改变了*新复制的引用*指向的内容，而不是原来的那个。

为了说明上述内容，还可以用一个等式或身份检查来实现。

```
# Passing an object results in copying the reference only
function changePerson(obj) {
     obj.name = "New Name";
     console.log(person === obj); // Results in true
     obj = {name: "New Name"};
     console.log(person === obj); // Results in false
}let person = {name: "Medium"};
changePerson(person);
console.log(person); // Prints {name: "New Name"}
```

第一次检查将导致*为真*，因为它是所讨论的同一个对象，并且不是副本，即使某个字段已被更改，但是第二次检查将导致*为假*，因为由`person`和`obj`指向的对象不再相同。

# 收集

![](img/2714df7f7dc88c4c3e5f69dc1f1ac40b.png)

Image Credit — [unsplash.com](https://unsplash.com/)

在大多数编程语言中，集合是非常重要的东西。有数组、集合、映射、散列表、树等等。这些都是不同的数据结构，用于不同的目的。

JavaScript 和其他的相比如何——我们可以利用哪些集合？

## 数组——或者我应该称之为列表

首先，有些数组和其他数组列表是一样的。*是的，JavaScript 数组实际上更像列表而不是数组。*只需运行 next 就可以显示所有可以在数组上使用的属性和方法，否则这些属性和方法只能在其他语言的列表中找到。

```
# JS Array is more like a List
let fruits = ["apple", "strawberry"];
console.log(fruits.__proto__); // join, filter, map, forEach etc.
```

现在，我经常听到别人说 JavaScript 中的数组和对象是一样的，数组的索引只是对象*中的*键*。*

```
# Arrays and Objects
let fruits = ["apple", "strawberry"];
let fruitsObj = {0: "apple", 1: "strawberry"};
```

以上可能导致持有相同的索引/键和值，但是再次检查类型，这将是清楚的，或者甚至更好地记录这些实例的`__proto__`字段，您将看到*所有的差异*。同样，这也适用于将对象与以下任何集合进行比较。

## 设置

与大多数语言一样，JavaScript `Set`是一个可迭代的集合，允许您存储唯一的值。JavaScript 是一种非常动态的语言，允许我们存储任何类型的值，无论是原语还是对象。

在大多数语言中，当有人提到一个集合时——他们可能会想到一个散列集合——它通常不保持插入的顺序，这同样适用于映射/散列表。

然而，JavaScript 的`Set`确实保持了插入的顺序，这一点值得注意，而且与人们的预期大相径庭。

除此之外，同样重要的是，如前所述，集合中的值可能只出现一次。

还有一件非常重要的事情是，集合的`has`方法比数组的`includes`方法更快，但是它缺乏通过数组索引的直接访问，考虑到如果您想要实现对元素的快速直接访问，您首先会使用一个对象或一个映射，这可能不是那么重要。

```
# Sets
let fruits = new Set(["apple", "strawberry"]);fruits.add("pear");
let containsPear = fruits.has("pear"); // truefruits.delete("apple");
let containsApple = fruits.has("apple"); // falsefruits.clear();
let size = fruits.size; // 0
```

除了上面的例子，谢天谢地，对于原型，你还可以在 set 上使用`forEach`、`entries`、`keys`、`values`方法！

## 地图

个人最喜欢的收藏— `Map`

![](img/57639ce5dcac1838da324fb5784c2c02.png)

Image Credit — [geojango_maps unsplash.com](https://unsplash.com/@geojango_maps)

正如已经提到的，当有人说*映射*时，他们可能指的是*哈希映射，*是的，JavaScript 映射基本上都是哈希映射。map 是键控集合的一种类型，它是可迭代的，和 set 一样，它保持插入顺序。

除此之外，使用地图的最大好处之一是可以快速直接访问元素。

给定一个人员数组，为了过滤并找到一个特定的值，您必须迭代每个元素，并根据您需要的属性检查它的姓氏属性，只有当您找到第一个匹配时，您才会返回值。

还有你要做多少次迭代和运算？嗯，在一个一千长的数组上——可能有一千次迭代。这基本上就是所发生的事情，不仅仅是数组上的 for 循环，大多数搜索方法都是如此，比如`find`或者`includes**.**`

有了地图，你可以存储以姓氏为关键字的*个人*，这样当你搜索一个人的时候——你基本上可以使用地图的`get`方法在一个操作中检索到。

```
# Maps
let john = {name: 'John', dob: '1990-10-12'};
let mary = {name: 'Mary', dob: '2001-06-09'};
let alex = {name: 'Alex', dob: '2000-05-10'};let persons = new Map();
persons.set(john.name, john);
persons.set(mary.name, mary);
persons.set(alex.name, alex);let name = 'John';
let person = persons.get(name);
```

这种函数的复杂性、效率和极限通常用数学表达式来描述，称为大 O 符号。在以后的一些主题中会有更多关于这方面的内容，但我建议阅读一下它以及它与执行和内存所需时间的关系。

此外，传统上——几年前，物体基本上被用作地图。您可以获得将值映射到字符串的类似功能，但是映射的一些好处是:

*   映射中的键可以是任何值，而不仅仅是字符串
*   贴图有大小属性，而你必须在对象上计算它

我强烈建议阅读更多关于地图的内容，例如在 Mozilla 的 MDN Docs 上，因为在你的技能组合中拥有地图是非常重要的，不仅是在 JavaScript 中，在所有编程语言中都是如此。

如果你是一个正在阅读这篇文章的开发人员，我希望它能帮助你，不管你是刚开始还是已经工作了很多年。请不吝赐教，提出更多有可能帮助到别人的概念！

我希望您觉得这很有用，并且喜欢 JavaScript 概念系列的第二篇文章。如果你喜欢它的内容，点击 follow，和我一起踏上研究和撰写更多关于 JavaScript 背后的科学和工程的旅程。

感谢您的阅读！🎉

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*