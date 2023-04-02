# JavaScript 错误的 10 个常见原因以及如何避免它们

> 原文：<https://javascript.plainenglish.io/10-common-causes-of-javascript-errors-and-how-to-avoid-them-85751c339dda?source=collection_archive---------8----------------------->

## 了解如何避免 JavaScript 错误的常见原因。

![](img/874e0464058f1bc03472a6329fae4b7c.png)

# 介绍

JavaScript 是一种灵活且广受欢迎的网络编程语言。它广泛应用于软件开发行业。不正确的 JavaScript 代码会导致意想不到的错误，并影响用户体验。

在本文中，我们将研究 JavaScript 错误的 10 个最常见的原因以及避免它们的实践。我们将了解错误的根本原因，然后寻找纠正错误的方法。

# 1.缺少括号和括号不匹配

这是初学者面临的最常见的错误。当程序员缺少括号、圆括号或大括号时，就会出现此错误。

**不正确:**

```
if(a==b) && (b==c){
 //do something
}
```

**正确:**

```
if((a==b) && (b==c)){
 //do something
}
```

# 2.变量名不正确

JavaScript 作者最常犯的一个错误是使用保留关键字命名变量。JavaScript 包含 60 多个保留字，不能在程序中用作变量名。

例如，“in”是 JavaScript 中的保留字之一，不能用于变量声明。最好使用能很好地解释变量用途的描述性名称。

# 3.未捕获的类型错误:无法读取未定义的属性

当对未定义的变量调用函数或读取属性时，会发生未捕获的类型错误。

```
function myFun( obj ){
 console.log(obj.val);
}var temp;
myFun(temp);
```

这里，temp 变量被声明但没有初始化，因此它是未定义的。试图访问未定义变量的 val 属性会导致错误。

人们总是建议在 javascript 程序中不要有未定义的变量。

# 4.加载页面前的 DOM 引用

文档对象模型(DOM)元素在加载之前不应被引用。Javascript 代码逐行执行。如果当前行代码的执行没有完成，它不会移动到下一行。

最佳实践是在定义 DOM 元素后加载脚本。

**不正确:**

```
<!DOCTYPE html>
<html>
<body>
<script>        
document.getElementsByClassName[0]("myDiv").innerHTML = "This will not     work";
     </script>
     <div class="myDiv"></div>
     </body>
</html>
```

**控制台:**

未捕获的类型错误:无法将属性“innerHTML”设置为 NULL

**正确:**

```
<!DOCTYPE html>
<html>
<body>
     <div id="myDiv"></div>
 <script>        
document.getElementsByClassName[0]("myDiv").innerHTML = "This will  work";
     </script>
     </body>
</html>
```

# 5.未定义的方法

不先定义方法就调用它是 JavaScript 错误的另一个典型来源。

**示例:**

```
var person = {firstName: “John”, lastName: “Doe”,
showName(){
console.log(this.firstName+” “+this.lastName);
}
person.name();
```

在这个例子中,“name”方法没有在 person 对象中定义。因此，它会导致错误。

# 6.Return 语句使用不当

JavaScript 中的 return 语句用于停止函数运行，以便输出其值。

```
function multiplyByTwo(n) {    
var res =  n*2;
    return;
    res;
     }
console.log(multiplyByTwo(7));
//This code gives an undefined error.
```

这可以通过确保在 return 语句之前返回特定的值或执行所有必要的操作来解决。

```
function multiplyByTwo(n) {    
var res =  n*2;
    return res;
     }
console.log(multiplyByTwo(7)); // 14
```

# 7.混淆相等(==，===)和赋值(=)运算符

**不正确:**

```
var name = “John”;
if(name=”Doe”){
 console.log(name)  //Doe
}
```

这里，名称变量不与**【Doe】**进行比较，而是将**【Doe】**赋给名称变量。此外，由于赋值操作总是返回 true，所以可用的 if 块将被执行。

**正确:**

```
//Correct wayVar name = “John”;
if(name==”Doe”){
 console.log(name)  //John
}
```

同样，双**等于(==)** 进行宽松的比较，而三**等于(===)** 进行严格的比较。

```
Const val = “15”;
console.log(val == 15); // true
console.log(val === 15);// false
```

在上面两种情况下，我们都是在比较一个字符串和一个数字。双倍等于**运算符(==)** 忽略变量的数据类型，而三倍等于**运算符(===)** 也检查两个操作数是否属于相同的数据类型，然后比较值。

# **8。将对象视为原始数据类型**

与数字、字符串和其他原始数据类型不同，对象是引用数据类型。

```
const person1 = {
​​    name: "John",
​​};
​​const person2 = person1;
person2.name = "Doe";
​​console.log(person1.name); //Doe
```

在将**人员 1** 分配给**人员 2** 时，**人员 2** 开始指向**人员 1** 存储的地址。因此，两个对象都指向内存中的同一个位置，键值的任何更改都会在两个对象中反映出来。

当我们需要复制对象时，如果我们为新对象创建新的引用，它就会起作用。这可以使用 spread 操作符 **(…)** 来完成，该操作符接受一个可迭代的**(这里是 object)** ，并将其扩展成单独的元素 **(keys)** 。

```
const person1 = {
​​    name: "John",
​​};
​​const person2 = {...person1};
person2.name = "Doe";
​​console.log(person1.name); //John
```

# 9.函数中不使用默认值

在函数的动态变量中设置默认值是一个很好的做法。这有助于防止在传递带有较少参数的函数时出错。

```
function sum(x,y){
return x+y;
}
console.log(sum()); //NaN
```

在上面的例子中，x 和 y 都没有定义。因此，我们得到的不是一个数字(NaN)作为输出。为了防止这种错误，我们可以在函数参数中设置默认值。

```
function sum(x=0, y=0){
return x+y;
}

console.log(sum()); // 0
```

开发人员可以使用相同的方法在缺少预期值的情况下返回错误消息。

# 10.函数中不使用默认值

在 JavaScript 中，这是一个经常被误解的概念。这是引用当前对象的引用关键字。

```
const person = {
 firstName : "John",
    lastName : "Doe",
    completeName : function (){
 console.log(this.firstName+" "+this.lastName);
    },
    showNameAfter3secs : function(){
  setTimeout(function(){
  console.log(this.firstName+" "+this.lastName);
        }, 3000);
}
}

person.completeName(); // John Doe
```

这可以正常工作，因为**“this”**正确地指向对象的 **firstName** 和 **lastName** 属性。在对象的方法内部， **"this"** 关键字指的是调用它的对象。

**person . shownamafter3s ECS()；//undefined 未定义**

这里，**person . shownamafter3s ECS()**中的**“this”**指向 person 对象，而 **setTimeout** 回调函数中的**“this”**没有指向 person 对象。一个对象应该调用 **setTimeout** 函数来引用当前对象。

因为没有对象调用**setTimeout****callback**函数，所以使用默认的窗口对象，它不包含 firstName 和 lastName 属性，因此，我们在控制台中没有定义。

为了保留这个关键字的引用，我们可以使用 arrow **functions(ES6)** 或者使用 apply、bind 或 call 方法。这里，我们将使用箭头函数。

```
const person = {
 firstName : "John",
     lastName : "Doe",
     completeName : function (){
  console.log(this.firstName+" "+this.lastName);
     },
     showNameAfter3secs : function(){
  setTimeout(()=>{  //arrow function used
  console.log(this.firstName+" "+this.lastName);
          }, 3000);
}
}

person.showNameAfter3secs();  // John Doe
```

从[这里](https://www.scaler.com/topics/javascript/)了解更多关于 JavaScript 的知识。

快乐学习！

***更多内容请看*** [***说白了就是***](https://plainenglish.io/) ***。报名参加我们的*** [***免费每周简讯***](http://newsletter.plainenglish.io/) ***。关注我们关于***[***Twitter***](https://twitter.com/inPlainEngHQ)***和***[***LinkedIn******。加入我们的***](https://www.linkedin.com/company/inplainenglish/) [***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***。***