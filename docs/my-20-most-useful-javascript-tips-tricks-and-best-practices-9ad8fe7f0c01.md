# 我的 20 个最有用的 JavaScript 技巧、诀窍和最佳实践

> 原文：<https://javascript.plainenglish.io/my-20-most-useful-javascript-tips-tricks-and-best-practices-9ad8fe7f0c01?source=collection_archive---------1----------------------->

![](img/f3c835841bb33cd232dda1b7945d2cb0.png)

你可能已经知道 JavaScript 是世界上使用最广泛的编程语言。它用于 web、移动混合应用、服务器端(NodeJS)和各种其他应用。因为它可以用于在 web 浏览器中显示简单的警告，以及使用 nodebot 或其他程序管理机器人，所以它可以作为许多新开发人员的编程入门。在就业市场上，精通 JavaScript 并能编写干净、高效代码的开发人员需求量很大。

不管他们的浏览器/引擎或 SSJS(服务器端 JavaScript)解释器如何，所有 JavaScript 开发人员都应该熟悉我将在本文中分享的技巧、诀窍和最佳实践。

1.  永远用`===` 代替`==`

如有必要，使用==(或！=)运算符。当使用===(或者！==)运算符。有人可能会说，它比较值和类型的速度比==更快。

```
[5] === 5   // is false
[5]  == 5    // is true
'5' == 5     // is true
'5' === 5    // is false
 []   == 0     // is true
 [] ===  0     // is false
 '' == false   // is true but true == "a" is false
 '' ===   false // is false
```

2.第一次确定变量值时，不要忘记 **var** 关键字。

在给未声明的变量赋值时，会自动建立一个全局变量。防止使用全局变量。

3.使用**`typeof`**`instanceof`******时要小心。**********

*   *****typeof* :一个 JavaScript 一元运算符，产生一个表示变量基本类型的字符串。****
*   *****构造函数*:是一个可以覆盖内部原型属性的属性的代码。****
*   *****instanceof* :又是一个 JavaScript 操作符，它搜索构造函数链中的每个原型，如果找到则返回 true，否则返回 false。****

****4.False 值包括 undefined、null、0、false、NaN 和“(空字符串)”。****

****5.创建一个自调用函数****

****自调用匿名函数或立即调用函数表达式是这个(IIFE)的常用名称。它是以下形式的函数，创建后立即运行:****

```
**(function(){
    // some private code to be executed automatically
})();  
(function(d,y){
    var result = d+y;
    return result;
})(20,20)**
```

****6.打乱一组数字****

```
**var numbers = [6, 650, 140 , -225 , 233 , 500 , 152300, -81451];
numbers = numbers.sort(function(){ return Math.random() - 0.5});**
```

****7.验证给定参数是一个数字****

```
**function isNumber(n){
    return !isNaN(parseFloat(n)) && isFinite(n);
}**
```

****8.将`arguments` 对象转换成数组****

```
**var argumentsArray = Array.prototype.slice.call(arguments);**
```

****9.清空数组****

```
**var newArray = [12 , 222 , 1000 ];  
newArray.length = 0; // newArray will be equal to [].**
```

****10.使用 map()函数方法遍历数组中的项****

```
**var squares = [1,4,6,2].map(function (val) {  
    return val * val;  
}); 
// squares will be equal to [1, 16, 26, 4]**
```

****11.不要随意使用**【评估】******

****JavaScript 中的 **eval()** 方法允许在运行时执行任意代码。最好的做法是永远不要使用它。如果它已经在你的脚本中，试着换成一个更有效的策略。****

****12.让使用**严格**成为习惯。****

****如果您想在每次编写代码时违反 JavaScript 时得到提醒，您必须使用 **strict** 。通过执行诸如声明变量、限制保留字的使用以及在代码中包含语句等规则，它有助于维护编程礼仪。****

```
**"use strict"; // Things might go chaotic

(function (){
    "use strict";
    // You are in control and write a better piece of code
})();**
```

****13.逗点算符****

```
**var a = 0; 
var b = ( a++, 88); 
console.log(a);  // a will be equal to 1 
console.log(b);  // b is equal to 88**
```

****14.避免使用`with()`****

****通过使用 with()，变量被添加到全局范围。因此，如果两个变量共享相同的名称，可能会引起混淆，值可能会被替换。****

****15.使用 switch/case 语句，而不是一连串的 if/else 语句。****

****16.一个 HTML 转义函数****

```
**function escHTML(text) {  
    var repl= {"<": "&lt;", ">": "&gt;","&": "&amp;", """: "&quot;"};                      
    return text.replace(/[<>&"]/g, function(character) {  
        return repl[character];  
    }); 
}**
```

****17.编码时，不要忘记使用代码美化器。在上线之前，使用 JSLint 和 mini 化(例如 JSMin)。****

****18.利用内嵌注释****

****通常，JavaScript 和大多数脚本和编程语言都允许添加行内注释。通过包含有用的文本，它有助于降低代码的复杂性。但是当使用内联风格时，要保持简洁，在一行之下。****

****19.在循环中缓存[array.length]****

****这个建议乍一看似乎很基本。但是，如果您的代码在一个循环中遍历一个大型数组，它可以显著提高性能。****

```
**var iMediumlen = stories.length;  
for (var iter = 0; iter < iMediumlen; iter++) {  
    console.log(stories[iter]);
}**
```

****20.验证对象是否具有属性****

```
**for (var prop in testObj) {
    if (testObj.hasOwnProperty(prop)) {
        // do something with prop
    }
}**
```

****JavaScript 是一种很棒的语言，这里有一些很棒的网站可以免费学习 JavaScript:****

1.  ****[FreeCodeCamp](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/)****
2.  ****[Mozilla 开发网络(MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide?ref=hackr.io)****
3.  ****[简单英语的 JavaScript](https://javascript.plainenglish.io/)****

*****更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*******