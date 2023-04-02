# 面试官:如何在 forEach()中修改原数组

> 原文：<https://javascript.plainenglish.io/interviewer-how-to-modify-the-original-array-in-foreach-fd36a08c6ce1?source=collection_archive---------1----------------------->

![](img/c0383beb9d1c354e40418d83666d34c5.png)

这是一个面试官的真题，有一半的受访者回答不好。今天，我们一起来深挖一下。

# forEach()可以修改原数组吗？

案例 1:元素是原始数据类型

```
let arr = [1, 2, 3];
arr.forEach((item) => { item = item * 2; });
console.log(arr); // result：[1, 2, 3]
```

结果:`Failed`

案例 2:元素是引用数据类型

```
let arr = [
{"name": "David", "age": 20},
{"name": "Peter", "age": 21},
{"name": "Bruce", "age": 22}];
arr.forEach((item) => { item = {"name": "Bob", "age": 23}; });
console.log(JSON.stringify(arr));
// result
// [{"name":"David","age":20},
// {"name":"Peter","age":21},
// {"name":"Bruce","age":22}]
```

结果:`Failed`

案例 3:元素是引用数据类型(当事人修改)

```
let arr = [
{"name": "David", "age": 20},
{"name": "Peter", "age": 21},
{"name": "Bruce", "age": 22}];
arr.forEach((item) => { item.name = "bob"; });
console.log(JSON.stringify(arr));
// result
// [{"name":"bob","age":20},
// {"name":"bob","age":21},
// {"name":"bob","age":22}]
```

结果:`Success`

所以，其实`forEach()`不会直接改变调用它的对象，但是那个对象可能会被回调函数改变。如果你理解基本数据类型赋值是值传递，引用数据类型赋值是引用地址的传递，那么上面的逻辑就很好理解了。

# *修改原数组的正确方法*

案例 1:元素是原始数据类型

```
let arr = [1, 2, 3];
arr.forEach((item, index, array) => { 
    array[index] = array[index] * 2; 
});
console.log(arr); // result：[2, 4, 6]
```

案例 2:元素是引用数据类型

```
let arr = [
{"name": "David", "age": 20},
{"name": "Peter", "age": 21},
{"name": "Bruce", "age": 22}];
arr.forEach((item, index, array) => { array[index] = {"name": "Bob", "age": 23}; });
console.log(JSON.stringify(arr));
// result
// [{"name":"Bob","age":20},
// {"name":"Bob","age":21},
// {"name":"Bob","age":22}]
```

案例 3:元素是引用数据类型(当事人修改)

```
let arr = [
{"name": "David", "age": 20},
{"name": "Peter", "age": 21},
{"name": "Bruce", "age": 22}];
arr.forEach((item, index, array) => { array[index].name = "bob"; });
console.log(JSON.stringify(arr));
// result
// [{"name":"bob","age":20},
// {"name":"bob","age":21},
// {"name":"bob","age":22}]
```

# 结论

如果只想枚举数组，可以使用 forEach()方法

但是，如果你想在枚举时改变数组中元素的内容，那么最好使用`map()`方法。`map()`方法本身将在处理后返回一个全新的数组，给出了一个明确的预期，即修改后的数据将被返回，不要使用`forEach()`方法以避免一些低级错误。

# 最后

**感谢阅读。**期待期待您的关注和阅读更多高质量的文章。

[](/the-difference-between-pseudo-classes-and-pseudo-elements-of-css-properties-e408fcbd68a0) [## CSS 属性的伪类和伪元素的区别

### 首先，让我们看看 W3C 对伪类和伪元素的定义:

javascript.plainenglish.io](/the-difference-between-pseudo-classes-and-pseudo-elements-of-css-properties-e408fcbd68a0) [](/identify-javascript-data-types-two-methods-are-enough-882e2c238e6b) [## 识别 JavaScript 数据类型:两种方法就足够了

### 我们知道，JavaScript 数据类型包括原语类型和对象类型。

javascript.plainenglish.io](/identify-javascript-data-types-two-methods-are-enough-882e2c238e6b) [](/regexp-is-hard-to-write-easy-to-use-2cd94236e48d) [## 正则表达式很难写，很容易使用

### 10 个有用的正则表达式。

javascript.plainenglish.io](/regexp-is-hard-to-write-easy-to-use-2cd94236e48d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*