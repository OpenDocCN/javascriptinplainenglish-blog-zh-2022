# 掌握 JavaScript 对象继承很容易

> 原文：<https://javascript.plainenglish.io/as-you-can-see-mastering-js-object-inheritance-is-so-easy-d39113fe8ec3?source=collection_archive---------10----------------------->

![](img/8e35e6e074cd7bd9d4e8a984c295a161.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**原型链传承**

继承是通过将子类的原型指向父类的实例来实现的。*如果一个父类有一个引用类型的私有属性，那么这个属性在被继承为公共属性时，就被所有子类共享，任何子类对当前属性的任何改变都会影响到所有其他继承的子类。*

**优点**

*   子类可以访问父类添加的原型方法和属性。
*   简单易用。

**缺点**

*   子类只能从一个父类继承，不可能有多个继承。
*   原型对象的属性由所有实例共享。
*   子类实例不能动态地将参数传递给父类的构造函数。
*   子类的新方法必须放在原型替换之后。

**实例**

```
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.children = [1, 2];
    this.setName = function() {};
}Person.prototype.addChild = function() {};function Student(score) {
    this.score = score;
    this.setScore = function() {};
}// The prototype of the child class is used as an instance object of the parent class to achieve the inheritance relationship
Student.prototype = new Person();
// The prototype will be overridden and the newly defined methods need to be placed after the prototype replacement.
Student.prototype.sayName = function() {};var student1 = new Student(1000);
var student2 = new Student(2500);student1.children.push(3);console.log(student1);
console.log(student2);
console.log(student1.children); // [1, 2, 3]
console.log(student2.children); // [1, 2, 3]
console.log(student1.__proto__ === student2.__proto__); // true point to Student
console.log(student1.__proto__. __proto__ === student2.__proto__. __proto__); // true points to Person
```

**构造函数继承**

父构造函数通过`call()`从子类型构造函数中调用。

**优点**

*   解决了原型链继承中子类实例共享父引用属性的问题。
*   允许单个子类从多个父类继承。
*   子类实例可以动态地传递参数给父类。

**缺点**

*   函数复用性差，每个子类都创建父实例函数的副本，影响性能。
*   实例只是子类的实例，而不是父类的实例。
*   子类只能继承父类的实例属性和方法，不能继承原型上的属性和方法。

**示例**

```
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.children = [1, 2];
    this.setName = function() {};
}Person.prototype.addChild = function() {};function Student(name, age, score) {
    Person.call(this, name, age);
    this.score = score;
    this.setScore = function() {};
}var student1 = new Student('Jhon', 26, 1000);
console.log(student1);
console.log(student1.addChild); // undefined
console.log(student1.__proto__); // Student
console.log(student1.__proto__. __proto__); // Objectfunction Student(name, age, score) {
    Person.call(this, name, age);
    this.score = score;
    this.setScore = function() {};
}var student1 = new Student('Jhon', 26, 1000);
console.log(student1);
console.log(student1.addChild); // undefined
console.log(student1.__proto__); // Student
console.log(student1.__proto__. __proto__); // Object
```

**组合遗传(原型链+构造函数组合遗传)**

组合继承是使用原型链继承原型属性和方法，使用构造函数继承实例属性。

**缺点**

*   子类型不能动态地将参数传递给超类型。
*   超类型构造函数将被调用两次。

**例子**

```
function Parent(username, password) {
    this.password = password
    this.username = username
}Parent.prototype = {
    login() {
        console.log(`login as , ${this.username}, password is ${this.password}. `)
    }
}function Child(username, password) {
    Parent.call(this, username, password) // second call
    this.articles = 30
}
Child.prototype = new Parent() // first call
// Child.prototype = Object.create(Parent.prototype) // This approach avoids the problems with the current inheritance approachconst user = new Child('jweboy', 'jl0630')
// user.login()
// console.log(user.articles)
```

**原型继承**

原型继承意味着创建一个临时构造函数，然后使用传入对象作为该构造函数的原型，最后返回临时类型的新实例。`ECMAScript5`增加了`Object.create`方法来标准化原型类型继承。

```
// The following method is also a concrete implementation of Object.create
function object(obj) {
    function F() {}
    F.prototype = obj;
    return new F();
}
```

**寄生遗传**

寄生继承是创建一个只用于封装继承过程的函数，它以某种方式在内部增强对象并最终返回该对象。

**缺点**

*   类似于构造函数，函数很难重用。

```
function createObject(obj) {
    const clone = Object.create(obj); // create a new object
    clone.run = function() { // some way to enhance the object
        return this.name;
    };
    return clone; // return the object
}
const obj = createObject({ name: 'tao' });
// obj.run(); // 'tao'
// console.dir(obj);
```

**寄生组合遗传**

寄生组合继承是通过构造函数继承属性，通过原型链继承方法。

**优势**

*   子类型可以动态地将参数传递给超类型。
*   超类型的构造函数只执行一次。
*   子类型属性是在它们自己的原型链中创建的，子类型之间不共享属性。

```
function inheritPrototype(child, parent) {
    // Create a copy of the supertype prototype
    const prototype = Object.create(parent.prototype)
    // Override the missing constructor property for the created copy
    prototype.constructor = child
    // the created copy is assigned to the prototype of the subtype
    child.prototype = prototype
child.prototype = prototype }function Parent(username, password) {
    this.password = password
    this.username = username
}Parent.prototype.login = function() {
    console.log(`login as , ${this.username}, password is ${this.password}. `)
}function Child(username, password) {
    Parent.call(this, username, password) // property inheritance
    this.articles = 30
}// Inheritance
inheritPrototype(Child, Parent)Child.prototype.read = function() {
    console.log('read article at', this.articles)
}const user = new Child('jweboy', 'jl0630')
// console.dir(user)
```

**参考资源**

*   [*深入探讨 JavaScript 继承的原理*](https://juejin.im/post/5a96d78ef265da4e9311b4d8?utm_medium=fe&utm_source=weixinqun#heading-7)
*   [*JavaScript 继承方法讲解*](https://segmentfault.com/a/1190000002440502#articleHeader10)

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*