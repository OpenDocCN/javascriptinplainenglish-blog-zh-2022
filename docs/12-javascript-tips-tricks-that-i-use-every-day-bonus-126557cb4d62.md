# 软件开发人员每天使用的 12 个 JavaScript 技巧和诀窍(还有奖金)

> 原文：<https://javascript.plainenglish.io/12-javascript-tips-tricks-that-i-use-every-day-bonus-126557cb4d62?source=collection_archive---------3----------------------->

## 作为软件开发人员，我经常使用的 JavaScript 技巧和诀窍。

![](img/f309f40fd234139b5e465d1497e92f03.png)

在这篇文章中，我将向你展示作为一名软件开发人员每天都会用到的 12 个 JavaScript 技巧和窍门。如果你更喜欢看视频，下面嵌入的视频将包含相同的提示和技巧。

1.  **用过滤器从数组中移除 falsy 值**

给定下面的数组，我们如何轻松地删除 falsy 值？

```
const myArray = [null, "1", "2", undefined, 0, 1, 2];
```

用`Boolean`构造函数

```
console.log(myArray.filter(Boolean)); // [ '1', '2', 1, 2 ]
```

注意，零也被删除了，这是因为在 JavaScript 中，零被认为是错误的。

**2。使用 console.trace 记录堆栈跟踪**

通过使用`console.trace`记录堆栈跟踪，可以很容易地发现应用程序内部在某一点发生了什么

**3。将数组析构为命名属性**

我们都知道你可以析构对象，但是你知道你可以把数组析构成命名的属性，就像对象一样，通过使用项目索引作为键。

**4。使用对象代替 switch 语句**

有时一个冗长的开关盒可以换成一个简单的物体。

上面的 switch case 语句可以用一个简单的对象来简化。您甚至可以通过逻辑 or 运算符`||`使用默认值。

**5。顶级等待**

如果您正在使用 Node.js 14 +,并且您的 package.json 中的类型为`module`,或者您正在使用一个`.mjs`文件扩展名，那么您可以使用顶级 await。

顶级 await 意味着 await 关键字不需要在异步函数中，它们可以在文件中的任何地方找到。

**6。请使用异步 await，而不是。然后&。接住**

这并不是什么技巧，而是 Node.js 中改进的语法。不要在异步函数上调用`.then`和`.catch`，而是使用`async`和`await`关键字。

**7。创建管道功能**

有时您需要将一个值定义为函数的结果，然后在另一个函数中使用该值作为参数。当您的代码需要这种逻辑时，管道函数有助于使您的代码简洁明了。

curried 函数在第一次函数调用中接受一个函数列表，然后在第二次函数调用中，传递初始值。初始值贯穿每个函数，直到最后一个函数返回最终值。

8。使用三元运算符代替 if-else

我经常看到这样的代码，其中定义了一个值，然后用 if-else 语句进行了变异。我对这样的代码有两个问题。首先，结果变量可以在文件中进一步变异，我可能会错过重新声明。其次，给一个变量赋值需要几行代码。

三元运算符允许您根据单行中的真或假条件为变量赋值:

**注意:**如果您需要多个 if-else 语句，那么在 else 部分添加另一个三元运算符可能会很诱人，这会使您的代码非常难以阅读。在这些情况下，我会创建一个函数来计算变量的值。

**9。格式化字符串对象**

`JSON.stringify`是 JavaScript 中最方便的特性之一。在调试 Node.js 应用程序时，我用它将对象打印到 React 中的 DOM，将大对象打印到控制台。但是结果可能非常难以解读。

幸运的是`JSON.stringify`将一个间隔值作为第三个参数，它将在打印之前格式化 JSON 字符串。

**10。有条件地添加到对象**

我经常看到对象被声明，然后根据条件给它们添加属性。如果条件是值为。的确，我们可以用`&&`操作符有条件地将属性添加到对象中。

**11。使用可选链接安全访问深度嵌套属性**

如果您试图在 JavaScript 中访问父对象未定义的对象内部的属性，您将会得到一个错误。有时你不想收到一个错误，你只想收到一个未定义的值。

可选链接可用于安全地访问 JavaScript 对象中深度嵌套的属性。

**12。使用记忆功能**

当用递归求解斐波那契数列时，我们很快就会遇到性能问题。问题是我们需要运行函数来计算第 4 行中每个数字的结果。

但是如果我们两次得到相同的数字呢？难道我们不应该存储结果，这样我们就不需要再次运行函数了吗？

记忆化是一种优化技术，它存储计算值的结果，因此如果我们有了那个结果，我们就不需要再计算它。

现在在第 5 行，我们用结果填充`memo`对象，并在每次调用`fibonacci`函数时传递它，极大地提高了函数的性能。

**加成:异或**

使用 XOR 在一个数字数组中寻找杂散数字。这个技巧使用按位异或(^)运算符来寻找杂散值`2`。虽然这是一个巧妙的技巧，但是根据输入数组的不同，它会产生一些意想不到的结果。

在 MDN 上阅读更多关于 XOR 的内容:[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise _ XOR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR)

如果你喜欢这篇文章，请务必在 https://www.youtube.com/TomDoesTech[](https://www.youtube.com/TomDoestech)*订阅我的 YouTube 频道*

**🌎关注我这里:
不和:*[*https://discord.gg/4ae2Esm6P7*](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbE8tcDdoY2hfbUZRNWg4VFp4X21sU3VVMEdBUXxBQ3Jtc0tsYVNxVk8zWkxYd1BOYndobHo0X00wNk4ybHZBblp1UWtkMENQaUpjbzhoS2lrLTFRN3FmS0xSejNNdms3ZW13Njd0RllCY2tvb0dLZC1ZMTNvS1M4a0RFMmViMVhaM2RmLURVZjRjUjBGTzFWaVkxdw&q=https%3A%2F%2Fdiscord.gg%2F4ae2Esm6P7) *推特:*[*https://twitter.com/tomdoes_tech*](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbGtER2hnYklqVG9CdXFWY3pWSjdQLVdaWWl5UXxBQ3Jtc0tuVjh6YnQyT1FkWWdYM3BtcW5KMzRYc1pJeXNLVXpkMjI5Yjl1dUxtNGRHdkxucW9vbVdtQnlVc2lmTzJWNXBuanBQMWkxZGU5RE9GeFFFbnlxWk1JNUJ1emt5TkZMaUpxd2plckd5NEo2d2VsSU93VQ&q=https%3A%2F%2Ftwitter.com%2Ftomdoes_tech) *脸书:*[*https://www.facebook.com/tomdoestech*](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbkc4MGlyTG82Z0dWalJ2OGxSaDBWUjNjT1p5UXxBQ3Jtc0tteFJHT1c3VDNWdHVKU1hRYWlrR3c1dlF4anBKb0F2YXlLWjNjTE5QUGpuTS1pTUNuSlJKWVFZUG5mdE9HVXY0ZkFNeW9VWU5GeFJGWFJJOHBQekpManFMMlNTSWM4ZVlOS1BDUmNLY0JSbG5SdnluTQ&q=https%3A%2F%2Fwww.facebook.com%2Ftomdoestech%E2%80%8B) *insta gram:*[*https://www.instagram.com/tomdoestech*](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbDI0OWhhdUVPSnVNRG1CQkQyeFFfUW1UMlBRZ3xBQ3Jtc0tuLWlPZl81dHNuRHUxWEZzZDdiTWlxQW9YUjFOeDJkREtWLWpPZW9Fek9EQzZkSDhVYjF3WnMtMW5tZXZQMXMwQnBBT1hCUUxwSm5jV3ZpQWRFeE40MUNlTlVOMmM2TkJ0X3RhSVl1RExxUENLaDNOYw&q=https%3A%2F%2Fwww.instagram.com%2Ftomdoestech%E2%80%8B)*

**https://www.buymeacoffee.com/tomn 请我喝咖啡:*[](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqazRNa0VmZG5lQk5VeUNtcDd1ZkhSR3NObTFDQXxBQ3Jtc0tsNDVwQUNZQmp3SGtwOXdwOWUxd2o4VXl3QjcwTmdtaTJqNGpPRG5US0hqa3hJQTgwdk5EMFNjN3J3aUlvamJhclNoZ3RvYWhhTUNmZ3hwX2FVcGtMYmhJUm85T2tLQk5sOXBEMVZ2ajlvVmg3YmxKNA&q=https%3A%2F%2Fwww.buymeacoffee.com%2Ftomn)*

***更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区获得独家写作机会和建议*](https://discord.gg/GtDtUAvyhW) *。***