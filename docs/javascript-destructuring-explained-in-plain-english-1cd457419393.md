# 用简单的英语解释 JavaScript 析构

> 原文：<https://javascript.plainenglish.io/javascript-destructuring-explained-in-plain-english-1cd457419393?source=collection_archive---------14----------------------->

## 关于 JavaScript 中的对象/数组析构，您只需要知道

![](img/8342dad8c0fd17f78dc26d30652d5876.png)

Photo by [Stephen Kraakmo](https://unsplash.com/@srkraakmo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

析构赋值是从对象中提取属性或者从数组中提取值到变量中的一种方便的语法。

# 数组析构

数组析构是一种从数组中解包值并将它们赋给变量的简化方法。例如，不这样做

```
const fruits = ['Apple', 'Orange', 'Watermelon'];
const apple = fruits[0];
```

做这个

```
const fruits = ['Apple', 'Orange', 'Watermelon'];// extract the element at 0 index 
// and assign it to a constant variable apple
const [apple] = fruits;console.log(apple); // Apple
```

## 默认值

当你析构一个不存在的值时，这个值被赋值`undefined`。例如

```
const persons = ['John', 'Mark'];
const [person1, person2, preson3] = persons;console.log(person1); // John
console.log(person2); // Mark
console.log(person3); // undefined
```

所以我们可以指定一个默认值，比如

```
const persons = ['John', 'Mark'];
const [person1, person2, **preson3 = 'Sara'**] = persons;console.log(person3); // Sara
```

## 忽略数组元素

如果您对特定索引处的数组元素不感兴趣，可以这样做

```
const fruits = ['Apple', 'Orange', 'Watermelon'];// ingore element at index 1
const [apple, , watermelon] = fruits;console.log(apple); // Apple
console.log(watermelon); // Watermelon
```

## 将其余元素赋给一个变量

```
const fruits = ['Apple', 'Orange', 'Watermelon'];const [apple, ...restFruits] = fruitsconsole.log(apple); // Apple
constole.log(restFruits); // ['Orange', 'Watermelon']
```

## 析构函数参数

我们可以在函数的签名中使用析构来提取所需的值

```
**function addListeners([elem1, elem2, ...rest]) {**
  elem1.addEventListener('click', () => {});
  elem2.addEventListener('click', () => {});
}const elements = [
  document.getElementById('div1'),
  document.getElementById('div2'),
];addListeners(elements);
```

也可以使用数组析构来交换变量

```
let a = 1;
let b = 2;[b,a] = [a,b];console.log(b); // 1
console.log(a); // 2
```

# 对象析构

对象析构允许你将一个对象的属性解包到不同的变量中。

而不是这样做

```
const car = { color: 'White, model: 1998 };const color = car.color;
const model = car.model;
```

做这个

```
const car = { color: 'White', model: 1998 };const { color, model } = car;console.log(color); // White
console.log(model); // 1998
```

## 析构时重命名

我们可以析构属性，同时重命名它

```
const car = { color: 'White', model: 1998 };// extract car color and name it something else
const { color: carColor } = car;console.log(carColor);
```

另一个例子

```
const { test: renamedTest } = require('some-lib');
```

## 默认值

给析构属性赋一个默认值。当析构的属性与对象的属性不匹配时，将使用该值。

```
const car = { color: 'White', model: 1998 };const {
  color,
  model,
  make = 'Toyota'
} = car;console.log(color); // White
console.log(make); // Toyota
```

或者为重命名的属性分配默认值

```
const car = { color: 'White', model: 1998 };const { make: carMake = 'Toyota' } = car;console.log(carMake); // Toyota
```

## 将对象的其余部分赋给变量

在析构的时候，我们可以将对象的剩余属性赋给一个变量，比如

```
const car = { color: 'White', model: 1998, make: 'Toyota' };const { color, ...rest } = car;console.log(color); // White
console.log(rest); // { model: 1998, make: 'Toyota' }
```

## 用动态属性名进行析构

当您不知道要从对象中提取的属性的名称时，这很有帮助

```
const car = { color: 'White', model: 1998 };const key = 'color';
const { [key]: carColor } = car;console.log(carColor); // White
```

## 用无效标识符进行析构

标识符是标识变量、函数或属性的字符序列。我们可以使用析构从一个标识符无效的对象中提取属性

```
const car = {
  color: 'White',
  'make-model': 'Toyota 1998'
};**// extract a property 'make-model'
// and assign it to a constant variable makeModel**
**const { 'make-model': makeModel } = car;**console.log(makeModel); // Toyota 1998// OR
const key = 'make-model'
const { [key]: makeModel } = car;
console.log(makeModel); // Toyota 1998
```

## 析构函数参数

如果你的函数接受一个对象作为参数，那么你可以像这样析构它的属性

```
**function printCarInfo({ color, model, make = 'Toyota' }){**
  console.log(color); // White
  console.log(model); // 1998
  console.log(make); // Toyota
}const car = { color: 'White', model: 1998 };printCarInfo(car);
```

# 组合对象和数组析构

我们可以一起使用对象和数组析构来提取所需的值

```
const cars = [
  { color: 'White', make: 'Toyota' },
  { color: 'Red', make: 'Hyundai' },
  { color: 'Black', make: 'KIA' },
];// ignore first two elements of cars array
// extract color and make from the object at index 2
const [, , { color, make }] = cars;console.log(color); // Black
console.log(make); // KIA
```

# 嵌套解构

我们可以从一个对象中访问嵌套属性，比如

```
const person = {
  name: 'John Doe',
  email: 'johndoe@gmail.com',
  address: {
    city: 'NY'
    country: 'USA',
    coordinates: {
      x: 1,
      y: 2,
    }
  }
};const { name, address: { city } } = person;console.log(name); // John Doe
console.log(city); // NY
```

我们在上面的代码片段中定义了两个变量，`name`和`city`。我们可以到这里的另一个嵌套层次

```
const { address: { city, coordinates: { x, y } } } = person;console.log(city); NY
console.log(x, y); // 1 2
```

更深入地访问嵌套属性会降低代码的可读性和迷惑性，所以要小心使用。

这就是 JavaScript 中的析构。希望这篇教程对你有用。感谢阅读

# 也阅读

[](https://betterprogramming.pub/how-to-create-modern-npm-packages-7c41cf610156) [## 如何创建现代 NPM 包

### 掌握从创建基本包到 CI/CD 和 ES6 支持的所有方法](https://betterprogramming.pub/how-to-create-modern-npm-packages-7c41cf610156) [](https://betterprogramming.pub/10-modern-javascript-tricks-every-developer-should-use-377857311d79) [## 每个开发人员都应该使用的 10 个现代 JavaScript 技巧

### 编写简短、简洁、干净的 JavaScript 代码的技巧](https://betterprogramming.pub/10-modern-javascript-tricks-every-developer-should-use-377857311d79) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*