# JavaScript 中的一些基本编码挑战

> 原文：<https://javascript.plainenglish.io/some-basic-coding-challenges-in-javascript-1270492687e7?source=collection_archive---------7----------------------->

![](img/0481eb73ac0ed0b6aac1931febc66de2.png)

**1。创建自定义地图功能的程序。**

```
Array.prototype.mymap = function(callback) {
    const newArr = [];
    for (let i = 0; i < this.length; i++) {
        newArr.push(**callback(this[i], i, this)**);
    }
    return newArr;
}const sample = [1,2,3];
const mapResult = sample.mymap((item) => {
    return (item * 2);
});console.log(mapResult);
```

**2 .用于创建自定义过滤器功能的程序。**

```
Array.prototype.myFilter = function(callback) {
    const filterArr = [];
    for(let index = 0; index<this.length; index++) {
        if(**!!callback(this[index], index, this)**) {
            filterArr.push(**this[index]**);
        }
    }
    return filterArr;
}
```

**3 .用于创建自定义缩减函数的程序。**

```
Array.prototype.myReduce = function(callback, accumulator) {
    if(this.length < 1) {
        throw new Error("Array is Empty")
    } if(!accumulator) {
        if(typeof this[0] === "string") {
            accumulator = '';
        } else if(typeof this[0] === "number") {
            accumulator = 0;
        }
    } for(let index=0; index < this.length; index++) {
        accumulator = callback(accumulator, this[index]);
    }
    return accumulator;
}
```

**4 .如何破坏嵌套对象**

```
const user = {
  id: 339,
  name: 'Fred',
  age: 42,
  education: {
    degree: {
      course: {
        value: "Masters"
      }
    }
  }
};const {education: {degree: {course: {value}}} } = user;
console.log(value); // "Masters"
```

**5。检查一个数字是否是质数的程序？**

```
function isPrime(num) {
 if(num < 2) return false;
 for(let k = 2; k < num; k++) {
  if(num % k == 0) {
   return false;
  }
 }
 return true;
}
console.log(isPrime(23));
```

**6 .程序打印前 n 个质数:**

```
function isPrime(num) {
 let flag = 0; for(let i = 1; i <= num; i++) **{**
  for(let k = 2; k < i; k++) {
   if(i % k == 0) {
    flag = 1;
    break;
   }
  } if(flag === 0) {
   console.log(i)
  } **}**
}
isPrime(10)
```

**7 .打印斐波纳契数列的程序:**

```
function fibonacciSeries(number) {
 let fibo = [0, 1]
 for(var i = 2; i <= number; i++) {
  fibo[i] = fibo[i - 1] + fibo[i - 2];
 }
 return fibo;
}
console.log(fibonacciSeries(10))
```

**8。不使用任何内置方法反转字符串:**

```
function reverseString(str) {
    let reverseString = "";
    for (let i = str.length - 1; i >= 0; i -- ) {
        reverseString += str[i];
    }
    return reverseString;
}
const result = reverseString("hello world");
console.log(result); // dlrow olleh
```

**9。使用内置方法反转一个句子及其字符:**

```
function reverseString(str) {
    const reverseString = str.split("").reverse().join("");
    return reverseString;
}
const result = reverseString("hello world");
console.log(result); // dlrow olleh
```

**10。使用内置方法将句子中的所有单词颠倒过来:**

```
function reverseString(str) {
    const reverseString = str.split(" ").reverse().join(" ");
    return reverseString;
}
const result = reverseString("hello world");
console.log(result); // world hello
```

**11。只反转(原地字符串)字符，不反转内置方法的句子:**

```
function reverseString(str) {
    const reverseString = str.split(" ").reverse().join(" ").split("").reverse().join("");
    return reverseString;
}
const result = reverseString("hello world");
console.log(result); // olleh dlrow
```

**12。程序执行嵌套对象的深度复制**

```
let mario = {
    welcomeText:{
        text:'hello'
    },
    health: undefined
};function deepCopy(obj){
  let newObj = {};
  for(i in obj){
    if(typeof(i)==="Object"){
      deepCopy(i);
    }
    newObj[i] = obj[i];
  };
  return newObj;
};console.log(deepCopy(mario));
```

**13。添加泛型 Add 函数(可以接受任意数量的参数),并承诺。**

```
function add(x, y, z, m, cb) {
    setTimeout(() => {
      cb(x +y +z+m)
    }, 2000)
}function promisify(func){
  return function(...args){
         return new Promise((resolve, reject)=>{       
           func(...args, resolve)
})
}
}const addPromise = promisify(add);
addPromise(1,2,3,4).then((data)=>{
  console.log(data);
});
```

**14。给出一个有字母和没有字母的循环中的闭包的例子关键词:**

**在 ES6 中使用 let 关键字:**在 ES6 中，可以使用 **let** 关键字来声明块范围的变量。

如果您在 for-loop 中使用`let`关键字，它将在每次迭代中创建一个新的词汇范围。换句话说，在每次迭代中你都会有一个新的`i`变量。

此外，新的词汇范围被链接到先前的范围，因此`i`的先前值被从先前的范围复制到新的范围。

```
for(let i = 0; i < 10; i++) {
 setTimeout(function() {
  console.log(i);
 }, 1000);
}
```

**使用 IIFE 溶液:**

```
for(var i = 0; i < 10; i++) {
 **(function(i)** {
  setTimeout(function() {
   console.log(i);
  }, 1000);
 **})(i);**
}
```

到此为止，谢谢。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*