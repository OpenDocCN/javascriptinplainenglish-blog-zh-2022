# 高级 JavaScript:数据类型的判断方法和转换方法综述

> 原文：<https://javascript.plainenglish.io/advanced-javascript-summary-of-judgment-methods-conversion-methods-of-data-types-896c5b496f81?source=collection_archive---------9----------------------->

![](img/4b79219dbd77243f27877f7358605b18.png)

# 内容

介绍了几种常用的数据类型判断方法，并手写了一个通用的判断方法
常见的强制和隐式类型转换的方法和规则，以及常见的面试问题

# 数据类型检查

## 方法 1:类型

*   typeof 通常用于确定基础数据类型，但引用类型可能会有问题
*   typeof null 打印对象，但这只是一个长期存在的 JS Bug。这并不意味着空值是引用数据类型，空值本身不是对象
*   无法确定引用数据类型。如果使用 typeof，则除了 function 之外，它将是“object ”,这是正确的

```
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof null // 'object'
typeof [] // 'object'
typeof {} // 'object'
typeof console // 'object'
typeof console.log // 'function'
```

## 方法 2:实例

*   instanceof 用于确定引用数据类型
*   instanceof 运算符用于检查构造函数的 prototype 属性是否出现在实例对象的原型链上。

```
let Car = function() {}
let benz = new Car()
benz instanceof Car // truelet car = new String('Mercedes Benz')
car instanceof String // true
let str = 'Covid-19'
str instanceof String // false
```

## 手写实例

typeof 用于确定基础数据类型。如果是，则返回 false

获取参数的原型对象，并向下循环，直到找到相同的原型对象

```
function myInstanceof(left, right) {
  // typeof is used to determine the underlying data type. If so, return false
  if(typeof left !== 'object' || left === null) return false;
  // getProtypeOf is the API that comes with the Object object and can get the prototype object for the parameters
  let proto = Object.getPrototypeOf(left);
  while(true) {                  //Loop down until you find the same prototype object
    if(proto === null) return false;
    if(proto === right.prototype) return true;//Find the same prototype object and return true
    proto = Object.getPrototypeof(proto);
    }
}
//Verify that your implementation of myInstanceof is OK
console.log(myInstanceof(new Number(123), Number));    // true
console.log(myInstanceof(123, Number));                // false
```

*   可以准确确定复杂引用数据类型，但不能正确确定基础数据类型的 instanceof。
*   typeof 还有一个缺点，就是虽然可以确定底层数据类型(null 除外)，但是除了函数类型之外，不能确定任何被引用的数据类型。

## 方法三:对象。原型。ToString

*   toString()是 prototype Object 方法，它返回格式为“[object Xxx]”的字符串，其中 Xxx 是对象的类型。
*   对于 Object 对象，调用 toString()直接返回[Object Object]；对于其他对象，您需要调用它们

```
Object.prototype.toString({})       // "[object Object]"
Object.prototype.toString.call({})  // Same result as above, plus call also ok
Object.prototype.toString.call(1)    // "[object Number]"
Object.prototype.toString.call('1')  // "[object String]"
Object.prototype.toString.call(true)  // "[object Boolean]"
Object.prototype.toString.call(function(){})  // "[object Function]"
Object.prototype.toString.call(null)   //"[object Null]"
Object.prototype.toString.call(undefined) //"[object Undefined]"
Object.prototype.toString.call(/123/g)    //"[object RegExp]"
Object.prototype.toString.call(new Date()) //"[object Date]"
Object.prototype.toString.call([])       //"[object Array]"
Object.prototype.toString.call(document)  //"[object HTMLDocument]"
Object.prototype.toString.call(window)   //"[object Window]"
```

## 最优解:写一个全局通用的判断方法

原则:

如果是基类型，则返回该类型

如果是对象类型，则使用对象。原型。ToString 判断方式，常规匹配

```
function getType(obj){
  let type  = typeof obj;
  if (type !== "object") {    // typeof is performed first, and if it is an underlying data type, it is returned directly
    return type;
  }
  // For typeof return result is object, perform the following judgment, the regular return result
  return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1');  // Notice the space between the RE
}
/* Code validation, case sensitive, which are typeof judgments and which are toString judgments? Think about */
getType([])     // "Array" typeof [] is object, so toString returns
getType('123')  // "string" typeof returns directly
getType(window) //"The Window" toString returns
getType(null)   // The first letter of "Null" is uppercase. typeof null is an object and must be determined by toString
getType(undefined)   // "undefined" typeof returns directly
getType()            // "undefined" typeof returns directly
getType(function(){}) //"function" typeof can be determined, so the first letter is lowercase
getType(/123/g)      //"The RegExp" toString returns
```

# 类型转换

## 先从一个小问题来体验一下吧

```
'123' == 123   // false or true?    
'' == null    // false or true?     
'' == 0        // false or true?   
[] == 0        // false or true?   
[] == ''       // false or true?    
[] == ![]      // false or true?    
null == undefined //  false or true?  
Number(null)     // What does it return?         
Number('')      // What does it return?          
parseInt('');    // What does it return?         
{}+10           // What does it return?          
let obj = {
    [Symbol.toPrimitive]() {
        return 200;
    },
    valueOf() {
        return 300;
    },
    toString() {
        return 'Hello';
    }
}
console.log(obj + 200); // What does it print out here?
```

**答案在底部。看看你能答对多少题**

# 强制类型转换

强制转换方法包括 Number()、parseInt()、parseFloat()、toString()、String()、Boolean()

## 隐式类型转换

由逻辑运算符&&，| |，！运算符+、-、*、/、关系运算符>、 =、相等运算符==、或 if/while 条件都是隐式转换

# ==和+的几个隐式类型转换规则

## ==的隐式类型转换规则

1 如果类型相同，则不需要转换。

2 如果其中一个运算符为空或未定义，那么另一个运算符必须为空或未定义才能返回 true，否则两者都返回 false

3 如果其中一个是符号类型，则返回 false

4 如果两个运算值都是 string 和 number 类型，那么 string 转换为 number；

5 如果一个运算值是一个布尔值，就把它转换成一个数字；

6 如果一个操作的另一端有一个对象值和一个字符串、数字或符号，则该对象被转换为其原始类型(调用该对象的 valueOf/toString 方法进行转换)。

```
null == undefined       // true  Rule 2
null == 0               // false Rule 2
'' == null              // false Rule 2
'' == 0                 // true  Rule 4 The string transfer is implicitly converted to Number and then compared
'123' == 123            // true  Rule 4 The string transfer is implicitly converted to Number and then compared
0 == false              // true  Rule 5 The Boolean type is implicitly converted to Number and then compared
1 == true               // true  Rule 5 The Boolean type is implicitly converted to Number and then compared
var a = {
  value: 0,
  valueOf: function() {
    this.value++;
    return this.value;
  }
};
// Notice here a could be 1, 2, 3 again
console.log(a == 1 && a == 2 && a ==3);  //true Rule 6 Object implicit conversion
// Note: However, after 3 times, reexecuting a==3 or the number before is false, because the value has been added, which should be noted here
```

## +的隐式类型转换规则

“+”运算符不仅可以用作数字加法，还可以用作字符串连接。只有当“+”号两边都有数字时，你在做加法；如果两端都是字符串，则在不进行隐式类型转换的情况下执行串联。

除了上述更常规的情况外，还有一些特殊的规则，如下所示。

*   如果其中一个是字符串，另一个是未定义的、null 或 Boolean，那么调用 toString()方法字符串串联；在纯对象、数组、正则表达式等情况下。，默认情况下调用该对象的转换方法将被优先考虑(在下一讲中讨论)，然后被连接。
*   如果其中一个是数字，而另一个是未定义的、null、Boolean 或 number，它将被转换为数字，用于加法运算、对象或引用最后一个规则。
*   如果一个是字符串，另一个是数字，则根据字符串规则执行连接。

```
The following is a combination of code to understand the above rules, as shown below.
  1 + 2        // 3  normal situation
  '1' + '2'    // '12' normal situation
  // Let's look at special cases
  '1' + undefined   // "1undefined" rule 1, undefined conversion string
  '1' + null        // "1null"  rule 1, null conversion string
  '1' + true        // "1true"  rule 1, true convert string
  '1' + 1n          //'11'      compares special strings and adds BigInt, BigInt is converted to string
  1 + undefined     // NaN      rule 2, undefined conversion numbers add NaN
  1 + null          // 1        Rule 2, null is converted to 0
  1 + true          // 2        Rule 2, true is converted to 1, and the sum of the two is 2
  1 + 1n            // Error    Cannot directly mix and add BigInt and Number types
  '1' + 3           // '13'     Rule 3, string concatenation
```

## 回答

```
'123' == 123   // false or true?    true
'' == null    // false or true?     false
'' == 0        // false or true?    true
[] == 0        // false or true?    true
[] == ''       // false or true?    true
[] == ![]      // false or true?    true
null == undefined //  false or true?  true
Number(null)     // What does it return?         0
Number('')      // What does it return?          0
parseInt('');    // What does it return?         NaN
{}+10           // What does it return?          10
let obj = {
    [Symbol.toPrimitive]() {
        return 200;
    },
    valueOf() {
        return 300;
    },
    toString() {
        return 'Hello';
    }
}
console.log(obj + 200); // What does it print out here?  400
```

最后，如果以上文章有什么不清楚的地方，请指出来，希望能在一定程度上帮助到大家，也期待您的关注，谢谢支持~

[](/12-common-javascript-functions-you-need-to-know-3d3a3ab712fc) [## 你需要知道的 12 个常见 JavaScript 函数

### 本文收集了日常开发中非常常用的 12 个函数。其中一些可能很复杂…

javascript.plainenglish.io](/12-common-javascript-functions-you-need-to-know-3d3a3ab712fc) [](/understand-es6-in-20-minutes-8ab8f958e379) [## 在 20 分钟内了解 ES6

### 不要让任何人告诉你:“你不知道 ES6 怎么敢说你知道 JS！”

javascript.plainenglish.io](/understand-es6-in-20-minutes-8ab8f958e379) [](/how-to-better-use-conditional-judgment-in-javascript-5aa1d2981e08) [## 如何在 JavaScript 中更好地使用条件判断

### 本文花很短的时间介绍如何用 JavaScript 编写更简单的条件判断，帮助您…

javascript.plainenglish.io](/how-to-better-use-conditional-judgment-in-javascript-5aa1d2981e08) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****