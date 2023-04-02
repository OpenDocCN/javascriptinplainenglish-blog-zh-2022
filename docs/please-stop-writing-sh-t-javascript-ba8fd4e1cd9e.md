# 请停止编写 Sh*t JavaScript

> 原文：<https://javascript.plainenglish.io/please-stop-writing-sh-t-javascript-ba8fd4e1cd9e?source=collection_archive---------2----------------------->

## 你做错了什么，以及如何弥补。

![](img/26f66f1c84979e344b0bca9c25d86c85.png)

无论你是经验丰富的开发人员还是新手，每个人都可以改进他们的代码。这里有一个 9 种方法的列表，你可以用它们来改进你的 JavaScript 代码。这些都是简单的提示和技巧。

我将讨论这 9 个主题:

1.  停止在你的 HTML 中写 JavaScript。
2.  停止导入这么多 JavaScript 文件。使用捆扎机。
3.  停止使用 jQuery
4.  停止支持 Internet Explorer
5.  停止使用 var
6.  使用箭头功能
7.  停止连接字符串。使用模板文字
8.  使用对象/数组析构
9.  停止使用||。使用？？相反。

# 停止在你的 HTML 中写 JS。到外面去。

您可能在学习 JavaScript 时将代码嵌入到了一个`<script>`标签中。这在初学 JavaScript 时很好，但在实践中却很糟糕。

*   你的 HTML 文件会变得很大。
*   当您有大量代码时，会降低可维护性。
*   JS 代码的第一行已经缩进了四次。

将您的 JavaScript 代码移动到外部文件中。你可能已经知道怎么做了，那就去做吧。停止在 HTML 文件中编写 JavaScript 代码。

```
...

<body>
	...

	<script src="path/to/file.js" />
</body>
```

# 停止导入这么多 JavaScript 文件。使用捆扎机。

大多数 web 开发项目都有成千上万行代码。所有这些代码都不能存储在一个 JavaScript 文件中。将代码分成多个具有适当名称的 JavaScript 文件通常是个好主意。

您可能习惯于像这样导入每个 JavaScript 文件:

```
<script src="core.js"></script>
<script src="bootstrap.js"></script>
<script src="utils.js"></script>
<script src="other.js"></script>
```

这有什么不好？

*   脚本加载时间长短不一。
*   一些脚本可能依赖于其他脚本，这些脚本可能无法按时加载(导致崩溃)。
*   HTML 文件中充斥着`<script>`标签。
*   很难跟踪必需的脚本和不推荐使用的脚本。
*   缺乏适当的编辑器支持
*   太多的 HTTP 请求——这也降低了你网站的搜索引擎优化

取而代之的是，研究 JavaScript bundlers。我最喜欢的捆绑器是 [webpack](https://webpack.js.org) 。你也可以看看其他捆绑软件——但 webpack 是最受欢迎的，它提供了开箱即用的令人印象深刻的功能。

使用 bundlers，您还可以将 CSS 和图像文件与 JavaScript 捆绑在一起。你可以去掉你所有的`<link rel="stylesheet" />`标签。

```
// Default import
import DefaultModule from './module.js';

// Non-default import
import { mod } from './module.js';

// Importing CSS
import './style.css';

// Importing an image
import brand from './logo.png';
```

# 停止使用 jQuery

为什么还在用 jQuery？曾几何时，JavaScript 是一种很难掌握的复杂语言。标准没有固化，浏览器之间的兼容性不存在，CSS 严重缺乏。

过去，人们确实需要 jQuery 否则，开发人员将不得不编写成千上万行代码。开发人员使用 polyfills 使不同浏览器的特性一致，`async` / `await`不存在，`fetch` API 缺失，等等。jQuery 解决了所有这些问题。

如今，这些问题都不存在。jQuery 降低了应用程序的性能。在 2022 年编写普通的 JavaScript 比使用 jQuery 容易得多，速度也快得多。

# 停止支持 Internet Explorer

我明白了。您的公司可能需要 IE 来处理一些旧的、过时的业务应用程序。但是，如果内部软件需要 Internet Explorer，它可能就不应该存在了——过时的浏览器没有任何好处，但是有很多缺点。

就连微软也明白，互联网浏览器是一个死亡的浏览器，没有未来。他们否决了浏览器，转而支持 Edge。最近，微软正式终止了浏览器。

IE 已经有了数量惊人的安全漏洞，并且不支持任何新的 web 功能。甚至不支持基本的 ES6 语法功能。**停止支撑 IE** 。

如果您支持工业工程:

*   您必须编写不同的代码来处理 IE(聚合填充)中缺失的功能。
*   您不能使用任何较新的 JS 特性(尤其是 ES6)，所以您必须重写整个代码库，并使用过时的 JS 规范。
*   您的代码库变得更大了——更难维护，也更难阅读。
*   **没人再使用 IE 了**

以下是您应该支持的浏览器目标列表:

*   铬-谷歌铬、Edge、Opera、Vivaldi 等
*   WebKit — Safari、GNOME web、Dolphin、Maxthon 和所有 iOS 浏览器。
*   壁虎——火狐、Tor、Camino 等。

# 停止使用`var`

停止使用`var`！它的存在只是为了支持旧的代码！相反，你可以使用`let`和`const`关键词。

*但* `*let*` *不是块作用域吗？*是。`let`和`var`可以互换，但不一定总是互换。然而，您的变量声明应该是块范围的，除非您不介意编写糟糕的(有时令人困惑的)代码。

```
// 💩 This is confusing – and terrible code
function foo() {
	if (condition)
		let x = 10;
	console.log(x);
}

// ✅ This is easier to understand the logic
function foo() {
	let x;
	if (condition)
		x = 10;
	console.log(x);
}
```

# 使用箭头函数

我见过高级开发人员——我是说老的，没有经验的——仍然经常对匿名函数使用`function`关键字。为什么？它是一个额外的关键词，让你的行更长，而且是多余的。

```
// 💩 Stop using `function`
doSomething(function() {
	// code here
});

// ✅ Use arrow functions
doSomething(() => {
	// code here
});
```

这没什么大不了的，但它是一个更简单的语法。

# 停止串联字符串。使用模板文字。

在大多数语言中，串联几乎是一样的。您有两个字符串(甚至一个数字)，并且想要组合它们。大多数语言中的连接运算符是`+`符号，但是 JavaScript、Python，甚至 Java 已经提出了更好的方法来连接两个字符串。

在 JavaScript 中，您可以使用`\``符号来创建模板文字。然后您可以使用`${ }`符号对其进行格式化:

```
const a = 'Hello';
const b = 'World';

// 💩 Slow, ugly, and old
console.log(a + ' ' + b);	// "Hello World"

// ✅ Fast, beautiful, and new
console.log(`${a} ${b}`);	// "Hello World"
```

# 使用对象/数组破坏

你是否曾经需要从一个对象中获取一个值，但是你给了变量和属性相同的名字？您可能会像这样编写代码:

```
const obj = {
	name: 'The Soggy Waffle',
	age: 22,
	degree: 'Computer Science'
};

const name = obj.name;
const age = obj.age;
const degree = obj.degree;
```

我在这里告诉你，有一个更简单更好的方法。您可以使用对象析构:

```
const { name, age, degree } = obj;
```

使用对象析构的唯一规则是变量名必须与字段名相同。这可以为您节省大量时间，并减少代码的大小。

当用作参数时，也可以使用对象析构:

```
function prettyPrint(props) {
	const name = props.name;
	const age = props.age;
	const degree = props.degree;
}

function prettyPrint({ name, age, degree }) {
	// name, age, and degree will be destructured in here
}
```

另一个可以使用的方法是数组析构。这类似于对象析构，但不是在变量名周围使用`{`和`}`，而是使用`[`和`]`。

假设你有一个包含五个元素的数组。你只关心数组的前两个元素；您通常会像这样编写代码:

```
const arr = [4, 6, 8, 10, 12];

const first = arr[0];
const second = arr[1];
```

使用析构，您的代码将看起来像这样:

```
const arr = [4, 6, 8, 10, 12];

const [ first, second ] = arr;
```

你可以用任意数量的元素来做这件事。

# 停止使用`||`，改用`??`。

JavaScript 有很多类似`false`的值，包括`0`和`''`(空字符串)。当使用`||`操作符分配缺省值(或后备值)时，有一个常见的错误。如果用户提供的值是`0`或空字符串，JavaScript 将默认提供第二个值。**这是个 bug** 。

我为此写了一整篇文章:

[](/stop-using-logical-or-use-null-coalescing-instead-f7668c96b0db) [## 停止使用逻辑 OR，使用？？代替

### 编辑描述

javascript.plainenglish.io](/stop-using-logical-or-use-null-coalescing-instead-f7668c96b0db) 

本质上，当您在提供回退值时使用`||`时，您通常只打算在第一个值为`null`或`undefined`时使用回退。但如果是其他任何 falsy 值，就会发生意想不到的事情。如果第一个值是`null`或`undefined`，那么`??`操作符通过严格默认为第二个值来解决这个问题。

```
function makeTransaction(description, amount) {
	return {
		description: description || 'Unknown purchase',
		amount: amount || 9.99
	}
}

makeTransaction('', 0);
// Returns: {
//		description: 'Unknown purchase',
//		amount: 9.99
// }
```

您应该使用的是:

```
function makeTransaction(description, amount) {
	return {
		description: description ?? 'Unknown purchase',
		amount: amount ?? 9.99
	}
}

makeTransaction('', 0);
// Returns: {
//		description: '',
//		amount: 0
// }
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*