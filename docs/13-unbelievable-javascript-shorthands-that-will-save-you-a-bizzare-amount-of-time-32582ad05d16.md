# 13 个不可思议的 JavaScript 快捷键，将为您节省大量时间

> 原文：<https://javascript.plainenglish.io/13-unbelievable-javascript-shorthands-that-will-save-you-a-bizzare-amount-of-time-32582ad05d16?source=collection_archive---------1----------------------->

## 年轻 JavaScript 程序员的必读书目

![](img/3b34e6c74a8b78033bf4ed45d0b453a6.png)

Photo by [Nicolas Picard](https://unsplash.com/@artnok?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

程序员的时间是昂贵的。

这就是为什么他们的生产力很重要。

有一些快捷方式可以节省开发人员的时间，并使代码看起来更整洁。

在许多速记中，有些也会降低代码的可读性。结果，代码的整体复杂性增加了。

因此，只有当你确定缩写不会在将来引起问题时，你才应该使用缩写。

我在这里提到的 13 个 javascript 速记可以节省你的时间。

# 1.声明变量

在 javascript 中，变量是用关键字`let`声明的。

当你没有用一个`let`语句给任何变量赋值时，变量被声明，但是它的值是`undefined`。

```
let a = 30;let b = 100;let c;console.log(a, b, c) // result : 30 100 undefined
```

您可以使用一个像这样的`let`语句来声明上面的所有三个变量:

```
let a= 30 , b= 100, c;console.log(a, b, c);// result : 30 100 undefined
```

也可以使用数组在一行中声明变量。

```
let [a,b,c] = [30, 100]console.log("value of a", a)console.log("value of b", b)console.log("value of c", c) //result:value of a 30
value of b 100
value of c undefined
```

# 2.使用三元运算符

通常，在 if 中..else 语句，当表达式为真时执行 if 语句，当表达式为假时执行 else 语句。

这里有一个例子:

```
if(num === 2){ console.log("Hello");}else{ console.log("Number not 2");}
```

在上面的代码中，如果表达式`num === 2`为真，将打印消息“你好”，如果表达式为假，将执行 else 语句。

三元语句可以帮助您替换 if…else 语句。三元运算符的语法如下:

```
[condition]? [true output] : [false output]
```

一个例子:

```
const result = x%2 == 0 ? "x is even": "x is not even" 
```

第一个操作数`x%2 == 0` 的计算结果为布尔值。如果第一个操作数的值为真，则计算第二个操作数并返回其值。

如果第一个操作数的值为 falsy，则计算第三个操作数的值并返回其值。

上面的 if…else 语句可以通过使用三元运算符来缩短。

```
num === 2 ?console.log("Hello"): console.log("Number not 2");
```

## 再举一个例子来说明问题

```
//longhandconst rank = 59if (rank <= 10){ return "Good rank"}else{ return "Bad rank"} //shorthandconst rank1 = 59return rank1<= 10 ? "Good rank": "Bad rank"
```

# 3.短路评估

在 javascript 中，一个变量值可以赋给不同的变量。

有时，当您将一个变量值赋给另一个变量时，您希望确保被赋的变量值不为 null、未定义或空。

当你阅读别人的 javascript 代码时，他们大多使用一个`if` 语句来检查这一点。

他们编写这样的代码:

```
if(var1 !== null || var1 !== undefined || var1 !== ""){ let var2 = var1}
```

在 javascript 中，上述代码可以写成:

```
let var2 = var1 || "hello"
```

在代码中，只有当 var1 具有非 falsy 值时，var1 中包含的值才会被赋给变量 var2。

Falsy 值包括`undefined`、`“”`(空字符串)、`null`、`0`和`false`。

如果 var1 包含任何 falsy 值，那么 var2 将被赋予值“hello”。

这里有一个例子:

```
let var1 = "hey"let var2 = var1 || "hello"console.log(var2)//result: hey  let var1;let var2 = var1 || "hello"console.log(var1)
console.log(var2)//result : undefined
hello
```

如果您想要使用多个语句，您可以:

```
let var2;
let var1;let var3 = var2 || var1 || "hello"console.log(var3)//result: hello
```

如果使用||运算符选择第一个非 falsy 值，则`0`、`“”`(空字符串)和`false` 将被忽略。

在某些情况下，需要赋值，如`0`、`“”`(空字符串)、和`false`。

## 将||运算符替换为？？操作员

一个例子:

```
let var1 = 0;let var2 = var1 || "hello";console.log(var2);//result: hello
```

在上面的代码中，由于 var1 的值等于零，并且是一个 falsy 值，所以 var2 被赋给 hello。

现在让我们将运算符||替换为？？。

```
let var1 = 0;let var2 = var1 ?? "hello";console.log(var2)//result: 0
```

在上面的代码中，由于 var1 的值等于 0，而？？运算符与 0 一起工作，这就是 var2 赋给 0 的原因。

当你使用。？操作员记住这一点:

？？运算符不像&&和||运算符那样具有更高或更低的优先级。如果您将运算符与&&和||运算符一起使用，则需要使用括号来更加明确。

以下是一些例子:

```
(x ?? y) || z-> ?? first, then || 
x ?? y || z-> It will give a syntax error: parentheses are required
```

的名字？？该运算符是“无效合并”。

# 4.交换两个变量

大多数程序员使用第三个变量来交换两个变量。

```
let a = 8, b = 48;const temp = a;
a = b;
b = temp;
```

不使用第三个变量也可以交换两个变量，如下所示:

```
let a = 8 , b = 48;[a,b] = [b,a]
```

# 5.箭头功能让事情变得简单

要声明任何函数，我们使用 function 关键字，后跟以下内容:

1.  充当函数名称的标识符。
2.  一对括号，以逗号分隔零个或多个标识符的列表。
3.  这个函数还有一对花括号，里面有一个或多个语句。

```
Example 1:function dis(a1, b1, a2, b2){ let a = b1-a1;
    let b = b2-a2; return Math.sqrt(a*a + b*b);}
```

上述函数可以用箭头函数来表示。

## 箭头功能

在箭头函数中，不需要使用`function`关键字。

arrow 函数是一个表达式，不是一个语句，所以也不需要函数名。

如果您看一下 arrow 函数的一般形式，它由一个或多个逗号分隔的参数列表组成。箭头以一般形式出现。

下面是一个使用箭头函数编写函数的示例:

```
function multiply(a, b){ return a * b;
} //Arrow functionconst multiply = (a, b) => a * b;
```

为了在箭头函数的帮助下编写示例 1，我们将这样做:

```
const dis = (a11, b11, a22, b22) => { let a = b11-a11; let b = b22-a22; return Math.sqrt(a*a + b*b);}
```

# 6.类固醇上的弦

在我们的日常工作中，我们使用`+`操作符将任意数量的字符串值与变量连接起来。

在 ES6 模板文字的帮助下，您可以用一种简单得多的方式来完成它。

```
//Longhand
console.log('Hello I obtained a rank' + rank + 'in this' + year); //Shorthand
console.log(`Hello I obtained a rank $(rank) in this ${year}`);
```

# 7.指数速记

Math.pow()在给定两个参数(base 和 exponent)的情况下，返回基数的指数幂。

```
console.log(Math.pow(7 , 2));console.log(Math.pow(4, 0.5));//result: 49
4
```

Math.pow()还有一个替代品。你可以用它作为这个数学函数的简写。

```
console.log(7**2)console.log(4**0.5)//result:49
2
```

**运算符允许您在不使用任何数学函数的情况下计算指数。

# 8.传播算子

程序员通常使用 for 循环来查找数组中的最小和最大数字。

但是 spread 运算符使得找到最大值和最小值变得容易得多。一行就能搞定。

```
const abc = [4,8,12,27,2,7]console.log(Math.max(...abc));
console.log(Math.min(...abc));//result:27
2
```

## 两个数组的串联

在扩展操作符的帮助下，两个数组可以很容易地连接起来。

你不必使用`concat`来做这件事。

这里有一个例子:

```
const abc = [2,3,4]
const xyz = [7,8,9]//longhand
let mnp = abc.concat(xyz);//shorthand
mnp = [...abc, ...xyz];
```

## 向数组中插入新元素

您可以使用 spread 元素在数组中推送新元素。

您可以停止使用`push`功能来完成此操作。

这里有一个例子:

```
let abc = [2,3,4];//Longhandabc.push(5);
abc.push(6);//shorthandabc = [...abc, 5,6];
```

# 9.将任何值转换为布尔值

借助双感叹号(！！)，可以将任何值转换为布尔值。

```
console.log(!![])console.log(!!3)console.log(!!678)console.log(!!0)console.log(!!"") //result:true
true
true
false
false
```

# 10.可以缩短 for 循环

为了循环遍历一个数组，我们长期以来一直使用传统的 for 循环。

要做到这一点，我们有许多其他选择。我们可以使用 for…of 来迭代数组。我们还可以使用 forEach()方法来遍历数组。

要访问一个特定的索引，我们可以在。

这里有一些例子。

```
const numberList = [5,3,9,4,6] //Longhandfor(let i =0; i < numberList.length; i++){ console.log(numberList[i]);
} //Shorthand using for...of for(const value of numberList){ console.log(value);} //Shorthand using forEach()numberList.forEach(value => console.log(value));//Shorthand using for...in for(const i in numberList){ console.log(`Position: ${i} and Value: ${numberList[i]}`);
}
```

# 11.不带数学的整数。floor

您可以不使用 Math.floor()函数来舍入数字。

为此，我们使用了`~~`操作符。

这里有一个例子:

```
//Longhand
Math.floor(8.75) //Shorthand
~~7.89 //results:
8
7
```

# 12.对象属性分配

如果代码中的变量名和对象键名相同，那么可以选择不写对象文字。

没有必要同时提到键和值。

```
let bookName = 'xyz'
let bookAuthor = 'abc'//Longhand
let Details = {bookName : bookName, bookAuthor : bookAuthor}; //shorthand
let Details = {bookName, bookAuthor};
```

# 13.十进制基数指数

1e5 表示 1 后跟 5 个零(100000)。

同样，1e4 表示 1 后面跟着 4 个零(10000)。

您可以在用 JavaScript 编写代码时使用它。

```
//Longhandfor(let i = 0; i < 100000; i++) { //do whatever you like
} //Shorthandfor(let i = 0;  i < 1e5; i++){ //do whatever you want
} //Here is a list for your convenience1e0 = 1
1e1 = 10
1e2 = 100
1e3 = 1000
1e4 = 10000
1e5 = 100000
1e6 = 1000000
1e7 = 10000000
```

# 你想加速你的程序员生涯吗

加入一群热爱编程和技术的人。

[你可以在这里加入。](https://codertoentrepreneurs.substack.com/)

在我们社区的帮助下，我们将解决程序员生活中的主要问题，并讨论前端和后端工程。

我们将帮助你重新规划你对科技中各种事物的理解。