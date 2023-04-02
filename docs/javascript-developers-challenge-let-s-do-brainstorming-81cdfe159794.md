# JavaScript 开发人员的挑战:面试实践头脑风暴

> 原文：<https://javascript.plainenglish.io/javascript-developers-challenge-let-s-do-brainstorming-81cdfe159794?source=collection_archive---------8----------------------->

![](img/06006fae2fd7c98e879e1f0a35adcc68.png)

如果您正在寻找用于面试练习或头脑风暴的基于 JavaScript 代码的问题，那么我会说您是在正确的地方学习。我将尝试涵盖所有棘手和关键的问题，这些问题不是 JavaScript 的理论部分。

为了更好的理解，我建议拿起纸和笔，试着先解决它们，这将是一个好的开始。

## 1.下面代码行的输出会是什么？

```
console.log("11"-1);                          // 10console.log("11"+1);                          // "111"console.log(0 === [[[0]]]);                   // falseconsole.log(0 == [[[0]]]);                    // trueconsole.log(0 === "0");                       // falseconsole.log(0 == "0");                        // trueconsole.log([1,[2,[3,[4,[5]]]]].toString())   // 1,2,3,4,5
```

## 2.如何高效地将多维数组转换成一维数组？

```
const arr = [1,[2,[3,[4,[5]]]]]
const dArray = arr.toString().split(',').map((num) => Number(num))
```

在第一行声明测试数组来测试我们的代码。在下一行中，在我们的结果看起来像“1，2，3，4，5”之后，我们将测试数组转换为字符串格式。最后一步是根据'，'进行拆分，并转换成数字。

## 3.创建 1 到 10 个随机延迟的数字承诺，并将它们打印成 1 到 10 的连续序列。

```
const delay = (val, ms) => new Promise(resolve => setTimeout(resolve(val), ms));const promiseArr = []
for(let i=1; i<=10;i++) {
    promiseArr.push(delay(i, Math.random()%5));
}const result = Promise.all(promiseArr)
result.then(res => {
    console.log(res) // [1,2,3,4,5,6,7,8,9,10]
})
```

延迟功能创建一个具有给定值和延迟的新承诺。

Promise.all()方法接受一个可迭代的承诺作为输入，并返回一个解析为输入承诺结果数组的单个[承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)。当输入的所有承诺都实现时，或者如果输入 iterable 不包含任何承诺，则返回的承诺将被实现。它在任何输入承诺拒绝或非承诺抛出错误时立即拒绝，并且将拒绝第一个拒绝消息/错误。

## 4.如何检查对象值是否为对象？

```
typeof yourVariable === 'object' && yourVariable !== null
```

## 5.如何用 JavaScript 创建自定义开关？

```
const match = (expr, allCases) => {
  return allCases[expr] || allCases?.default;
}const allCases = {
  Hi: 'good morning',
  Red: "color",
  BMW: "my favourite",
  default: "not available"
 }const matched = match('Hi', allCases)
const notMatched = match('Not', allCases)console.log(matched)      // Good Morning
console.log(notMatched)   // not available
```

match 函数将所有大小写和您的表达式进行匹配；如果你的表达式不存在，那么它会找到默认的。allCases 是一个包含所有事例的键值对象。

## 6.下面代码的输出会是什么？

```
const a = Number(1)
const b = Number(2)
const c = "1"
const d = "2"console.log(typeof a * b)          // NaN
console.log(typeof c * d)          // NaN
console.log(typeof a * c)          // NaN
console.log((a*b) == (c*d))        // true
console.log((a*b) === (c*d))       // true
console.log(typeof Number(a * b))  // number
console.log(typeof Number(c * d))  // number
```

## 7.下面代码的输出会是什么？

```
const arr = [1,2,3,4]
arr.length = 0;   // don't do this in your lifeconsole.log(arr)  // []console.log("1" - "2" + "3" + "4" * "5")
// first * occurs and result will be 
// "1" - "2" + "3" + "20"
// now left to right flow goes
// "-1" + "3" + "20"
// "-1320"
```

## 8.我们有三个带有名称和延迟的承诺，(慢速，200)，(快速，50)，(即时，0)，所有承诺都应该同时解决，并且顺序应该保持为慢速，快速和即时系列。

```
const slow = new Promise(resolve => {
 setTimeout(resolve, 200, 'slow');
});
const instant = new Promise(resolve => {
 setTimeout(resolve, 0, 'instant');
}); ;
const quick = new Promise(resolve => {
 setTimeout(resolve, 50, 'quick');
});const result = Promise.all([slow, quick, instant])result.then((res) => {
    console.log(res)
})
```

## 9.下面代码的输出会是什么？

```
var a={name:"RKstar"}
var b={name:"RKstar"}console.log(a===b); // false
console.log(a==b);  // false
```

## 10.如果数组是对象的实例，那么如何区分对象或数组呢？你将如何编写一个程序来演示它们之间的区别？

```
console.log(diff([]))   // Array
console.log(diff({}))   // Object
console.log(diff(null)) // Null or Undefinedfunction diff(obj) {
    if(Object.prototype.toString.call(obj) === '[object Array]') {
        return 'Array'
    } else if(typeof obj === 'object' && obj !== null) {
        return 'Object'
    } else {
        return 'Null or Undefined'
    }
}
```

有几个*理论上的*和*基于代码的*问题给你，请随时在这里*评论*你的解决方案。

【null 和 undefined 有什么区别？

*写一个 JSON 解析器，不用内置 JSON 解析器。*

这就把我们带到了终点！非常感谢你一直读到最后——如果这篇文章在任何意义上有所帮助，我会很感激一个跟随来帮助我达到我的目标。:)

请随时访问我的网站，如果您有任何关于 JS/DevOps 的疑问，请随时与我联系。

[https://ritikchopra . netlify . app](https://ritikchopra.netlify.app/)

祝你好运！
里提克·乔普拉😘

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*