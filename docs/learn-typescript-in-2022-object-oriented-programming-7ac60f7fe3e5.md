# 2022 年学习 TypeScript:面向对象编程

> 原文：<https://javascript.plainenglish.io/learn-typescript-in-2022-object-oriented-programming-7ac60f7fe3e5?source=collection_archive---------15----------------------->

## TypeScript 是纯面向对象的，有类、接口，像 C#或 Java 一样是静态类型的

![](img/89c8bbdf31d3fae25807ad34ec283970.png)

Photo by [Sergey Zolkin](https://unsplash.com/@szolkin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TypeScript 允许您按照自己真正想要的方式编写 JavaScript。TypeScript 是 JavaScript 的类型化超集，它编译成普通 JavaScript。本文旨在向您传授 TypeScript 的基础知识。

# 要求

我建议您在继续学习本教程之前，对 OOP 概念和基本 JavaScript 有一个很好的理解(以便充分利用它)。

# 入门指南

Node.js 是服务器端 JavaScript 的开源、跨平台运行时环境。Node.js 需要在没有浏览器支持的情况下运行 JavaScript。在终端窗口中键入以下命令以安装 TypeScript:

```
$ npm install -g typescript
```

Typescript 可以构建在大量的开发环境上，如 Visual Studio。

## 句法

语法定义了一套编写程序的规则。每种语言规范都定义了自己的语法。类型脚本代码的一个示例:

```
var message:string = "Hello World" 
console.log(message)
```

要编译您的 TypeScript 文件，请输入以下命令:

```
tsc app.ts
```

然后，您可以运行它:

```
node app.js
```

## 变量

变量就像一个储存数据的小容器。变量在 TypeScript 中至关重要。在 TypeScript 中，您需要指定变量的数据类型。

与其他编程语言一样，TypeScript 包含下列数据类型:

*   字符串—字符串是一系列字符
*   整数-整数数据类型是非十进制数
*   浮点—浮点是一个带小数点的数字或一个数字
*   布尔值—布尔值表示真或假。
*   数组—数组在一个变量中存储多个值。

## 声明和初始化变量

```
variableName:type = value;
```

一个例子:

```
var name:string = "Bryan";
```

# 数组

数组用于在单个变量中存储多个值，而不是为每个值声明单独的变量。

## 声明数组

```
var array_name[:datatype];        //declaration
```

## 初始化数组

```
array_name = [val1,val2,valn..]   //initialization
```

**可以访问元素**

```
array_name[subscript] = value
```

# 基本运算符

*   +(加法)
*   -(减法)
*   *(乘法)
*   /(除法)
*   %(模块)
*   ++(增量)
*   -(减量)

# 条件语句

TypeScript 具有以下条件语句:

*   如果
*   其他
*   否则
*   转换

## 如果语句

如果特定条件为真，则执行一段代码。

```
if (*condition*) {
  *// block of code to be executed if the condition is true*
}
```

## Else 语句

如果特定条件为假，则执行一段代码。

```
if (*condition*) {
  *// block of code to be executed if the condition is true*
} else {
  *// block of code to be executed if the condition is false*
}
```

## If Else 语句

如果第一个条件为假，则指定新的条件。

```
if (*condition1*) {
  *// block of code to be executed if condition1 is true*
} else if (*condition2*) {
  *// block of code to be executed if the condition1 is false and condition2 is true*
} else {
  *// block of code to be executed if the condition1 is false and condition2 is false*
}
```

## 转换

switch 语句用于从许多要执行的代码块中选择一个。

```
switch(*expression*) {
  case x:
    *// code block*
    break;
  case y:
    *// code block*
    break;
  default:
    *// code block*
}
```

# 环

只要达到指定的条件，循环就可以执行一段代码。

## While 循环

只要特定条件为真，while 循环就会一直循环。

```
while (*condition*) {
 *// code block to be executed*
}
```

## For 循环

当您确切地知道要在一个代码块中循环多少次时，可以使用 for 循环。

```
for (*statement 1*; *statement 2*; *statement 3*) {
  *// code block to be executed*
 }
```

语句 1 在代码块执行之前执行。

语句 2 定义了执行代码块的条件。

语句 3 在代码块执行后执行。

**对于每个循环**

还有一个“for-each”循环，专门用于遍历数组中的元素:

```
for (*type* *variableName* : *arrayName*) {
  *// code block to be executed*
}
```

# 结论

读完这篇文章后，我希望您现在可以编写一个简单的 TypeScript 代码，并对 TypeScript 的内容有一个很好的了解。

[***点击这里成为正式中等会员！***](https://bryanwriting.medium.com/membership)

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*