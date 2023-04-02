# 初学者打字稿入门

> 原文：<https://javascript.plainenglish.io/an-introduction-to-typescript-ecd8953452?source=collection_archive---------17----------------------->

## 什么是 TypeScript？TypeScript 是一种基于 JavaScript 的 ***强类型*** 编程语言，在任何规模下都能为您提供更好的工具。

![](img/ad813a13d0f141b33aea41df97f2c843.png)

前端 React 开发人员热衷于使用类型脚本而不是 JavaScript。尽管不建议所有类型的项目都使用它，但它克服了 JavaScript 的许多缺点，并对其进行了改进。

在这篇对初学者友好的文章中，我们将了解 TypeScript 到底是什么，它如何成为一种强类型语言，它与 JavaScript 相比如何，以及它的一些突出特性。当然，我们将会写我们的第一部*。ts* 码也！

# 什么是 TypeScript？

TypeScript 是一种 ***强类型*** 编程语言，它构建在 JavaScript 之上，在任何规模下都能为您提供更好的工具。这是一个由微软创建的免费开源项目。

它是 JavaScript ''的'T12 超集，这意味着您可以继续使用您已经开发的 JavaScript 技能，并添加某些您以前无法使用的功能。与 JavaScript 相比，它是一种强类型语言，而 JS 是一种松散类型的语言。你可以把这当成有超能力的 JavaScript！

现在这是这种语言真正闪耀的地方…还记得我们在上面使用的术语“强类型”吗？在这个上下文中是什么意思？嗯，这意味着变量/函数的*数据类型*和其他原语*必须是* ***预定义的*** 。这是 TypeScript 最重要的特性之一(这就是它如此关注“类型”的原因)。

在幕后，它编译成 JavaScript，为您提供 JavaScript 平台的好处以及类型的预期优势。

# TypeScript 的主要功能

现在您已经对这种语言有了一些了解，是时候看看它为开发人员提供的所有重要而有用的特性了。以下是其中的几个例子:

1.JavaScript 等等:TypeScript 为您的 JavaScript 代码添加了额外的语法糖，以支持与您的编辑器更紧密的集成。

2.**可以在 JavaScript 可以运行的任何地方运行**:类型脚本代码转换成 JavaScript，然后可以在浏览器、Node.js 或 [Deno](https://deno.land/) 以及您的应用程序中运行。

3.**安全性和可伸缩性**:它使用类型推断，无需编写任何额外的代码，就能为您提供强大的工具。

4.**编辑器支持**:大多数现代 ide 和代码编辑器，如 [VS Code](https://code.visualstudio.com/) 都内置了对类型脚本文件的支持。您可以在 VS 代码中获得现成的自动完成和自动导入支持。

5.**独特的语言特性**:这里有一些你只能在打字稿代码中找到的特性；接口、名称空间、泛型、抽象类、数据修饰符等等！

6.**逐步采用率**:您可以将类型应用到任何以前的 JavaScript 项目或代码库中。有了强大的编辑器支持，TypeScript 可以在编辑器内部捕捉错误！

7.**描述数据容易**:在你的代码中描述对象和函数的形状真的很容易。这使得在编辑器中查看文档和问题成为可能。

所有这些应该会让您对什么是 TypeScript 以及它的特性有一个大致的了解，现在是时候编写我们的第一个 TypeScript 代码了，并看看如何将它与 JavaScript 一起使用。

# 从 JavaScript 到 TypeScript

我们不会直接进入打字稿代码。相反，我们希望您熟悉已经存在的 JavaScript 知识，并使用它将小的 JS 代码转换成 TS 代码。

假设我们有以下 JavaScript 代码:

```
// @ts-check
function compact (arr) {
  if (orr. length > 10)
    return arr. trim(0, 10)
  return arr
}
```

现在你会看到一个类似“找不到名字'【T0]'”的错误接下来，假设我们犯了另一个错误，比如使用

`trim` 而不是`slice` 上了一个阵:

```
function compact (arr: string[]) {
  if (arr.length > 10)
    return arr.slice(0, 10)
  return arr
}
```

我们为`arr` 参数添加了一种类型的`string[]`(字符串数组),因此它应该总是接受一个基于字符串的数组，除此之外什么都不接受。因此，我们称 TypeScript 为“强类型”。

# 安装和设置 TypeScript

是时候在我们的机器上写一些 TS 代码了！您可以通过以下 NPM 命令全局安装 TypeScript:

```
npm install -g typescript
```

接下来，您可以通过运行`tsc –v`来检查系统中安装的 TypeScript 版本，从而确认安装。
注意，在你写了一个类型脚本代码并想要运行它之后，简单地用 file 运行`tsc` ，这个名字就不起作用了，因为`tsc` 只是一个类型脚本编译器。我们需要 [Node.js](http://nodejs.org/) 来获得实际的日志输出。我们可以通过为“Hello World”程序运行以下命令来实现:

```
tsc hello.ts && node hello.js
```

**你的第一首“你好，世界！”在机器上全局安装 TypeScript 后，在 TypeScript**
中。你可以打开一个合适的代码编辑器，比如 VS Code，它对 TypeScript 工具有很好的支持。

1.  创建一个名为 *helloWorld.ts* 的新的类型脚本文件。然后像在 JavaScript 中一样简单地编写一个控制台日志语句:

```
console.log("Hello World!");
```

2.打开命令提示符或终端窗口，运行`tsc helloWorld.ts`。您将看到什么也不会发生，因为这里没有分配类型，因此没有类型错误。

3.相反，您将看到 TypeScript 编译器在同一个目录中生成一个新的 *helloWorld.js* 文件。这是相同的 TS 代码，但它是生成的 JS 文件输出。

4.是时候让我们的控制台声明更好了。假设我们希望通过让用户通过欢迎功能输入姓名和日期来记录该人的姓名和日期:

```
function greet(person, date) {
  console.log(`Hello ${person}, today is ${date}!`);
}greet('Brendan');
```

注意我们调用`greet` 函数的方式。如果您运行这个，您将会得到这个错误，因为我们只传递了 1 个参数，而不是预期的 2:

```
// TS ERROR: Expected 2 arguments, but got 1.
```

greet()函数的参数没有任何显式定义的类型，所以 TS 会给它任何类型。

1.  让我们用下面的有效代码来修复我们的函数:

```
// "greet() takes a person of type string, and a date of type Date"
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}`);
}greet('Maddison', new Date());
```

现在我们已经明确定义了所有的数据类型，我们可以高兴地看到 log 语句打印出我们需要的确切输出。

如果您想知道它的等价 JS 代码是:

```
// "greet() takes a person of type string, and a date of type Date"
function greet(person, date) {
    console.log("Hello " + person + ", today is " + date.toDateString() + "!");
}
greet('Maddison', new Date());
```

至此，我们已经涵盖了您需要了解的关于 TypeScript 语言的最基本的基础知识。如您所见，它非常接近 JavaScript，因此如果您已经在使用 JavaScript，那么学习并将项目迁移到 TypeScript 应该很容易。为了简化您的工作，我们创建了一些[仪表板模板](https://www.wrappixel.com/templates/category/dashboard-templates/)。现在就退房吧！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***