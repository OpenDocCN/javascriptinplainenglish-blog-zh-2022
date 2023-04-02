# 每个程序员都应该知道的 JavaScript 概念

> 原文：<https://javascript.plainenglish.io/javascript-concepts-every-programmer-should-know-d04731fe7a7c?source=collection_archive---------0----------------------->

## Javascript 工程:背后的科学

## 了解这些 JavaScript 概念可以让你的程序员生活更轻松。

JavaScript 是 web 的头号编程语言，但除此之外，由于许多原因，它也传播到了许多平台。

其中之一是开发的容易程度，以及如何容易地掌握和学习它，但仍然——正如在每种编程语言中一样，总有一些不太复杂的和一些更复杂的概念需要掌握。

![](img/817d725ebadcfc5156d504412ce82360.png)

Image Credit — Workato

“JavaScript 是唯一一种人们觉得在开始使用之前不需要学习的编程语言。”—道格拉斯·克洛克福特

这确实感觉很直观，但仍然有一些基础和要点，无论是新手还是有经验的程序员都应该知道。

让我们开始吧！

# 箭头功能

这个很简单——箭头功能是在 ES6 中引入的，您可能已经知道了。

![](img/ff0ce1f317779608006caa9eacb60a0c.png)

GIF Credit — [ahighmentality / deviantart.com](https://www.deviantart.com/ahighmentality)

与传统函数相比，我们可以用更短的*箭头语法*来编写函数。

```
# Traditional Function
function sum(param1, param2) {
    return param1 + param2;
}let result = sum(1, 1);# Arrow Function
let sum = (param1, param2) => param1 + param2;
let result = sum(1, 1);
```

还有一些事情需要记住。

1.  您可以使用[休息参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

```
# Arrow Function With Rest Parameters
let sum = (param1, param2, ...params) => 
     params.reduce((total, next) => total + next, param1 + param2);let result = sum(1, 1, 2, 3, 4, 5);
```

2.您可以为参数定义[默认值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

```
# Arrow Function With Default Parameters
let sum = (param1, param2 = 2) => param1 + param2;let result = sum(1);
```

3.你可以利用[重组](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

```
# Arrow Function With Object Destructured Parameters
let sum = ({ param1, param2 }) => param1 + param2;let object = {param1: 5, param2: 15};
let result = sum(object);
```

上述概念本身就值得研究，所以请务必阅读:

*   [剩余参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
*   [默认参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
*   [解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

# 数组缩减

上一个示例让我想到了—数组缩减。Reduce 函数不是必须知道的，但是理解它是非常值得的。`**reduce()**`函数对一组元素执行所提供的*“reducer”*，执行一个表达式并将结果提供给下一次迭代。

记住 Reduce 如何工作的最简单的方法是想象它是 1。它*将*一组元素简化为一个*单值* —和 2。类似于递归，它遍历每个元素，为其提供*先前的计算 ie。数值*。

`**reduce()**`函数的结果是单个值。

```
# Reduce
# def. reduce(callbackFn(previous, next);
# def. reduce(callbackFn(previous, next), initialValue);const elements = [1, 2, 3, 4, 5];
const sum = elements.reduce((previous, next) => previous + next, 0);
```

reduce()函数有两个参数。第一个是用户提供的带有两个参数的函数，一个是 **previous，即前面元素迭代**的返回值，另一个是数组中将要计算的**下一个元素。**

它接受第二个参数——initial value，正如您所看到的，这将被用作第一次迭代的 **previous** ，因为前面的元素迭代没有**返回值。**

像`**reduce**`这样的递归函数非常强大，但是通常难以阅读和理解。Array Reduce 在您的技能组合中可能是有用的，因为当您真正需要它或遇到这个函数时，它会让您感觉更舒服，但是在编写它时，请确保您总是权衡好处和可读性，因为通常用简单得多的代码也可以达到同样的效果。

# 异步执行

有很多关于同步执行的历史可以阅读，单线程计算机如何循环运行任务，为每个任务分配较短的时隙，从而实现看起来像“同时”的流。

现在，在现代计算机体系结构中有了多线程，同时执行任务成为可能。然而，async 是如何融入画面的呢？

JavaScript 默认为**同步** **并且是单线程**——但是为了实现异步执行，我们可以使用 async / await。根据定义，异步任务是在*“后台”、*中执行的任务，通常对长时间运行的任务有用，比如 HTTP 请求。

Async / await 以及它在后台的工作方式需要一个独立的帖子，但简单来说，JS 使用 JS 引擎，如 Node 或浏览器引擎，如 Google Chrome 的 V8。引擎本身将从 JavaScript 的单线程中挑选异步任务，并在后台执行它们。这可能仍然发生在同一个线程上，但是有一些操作引擎实际上将在不同的线程上执行，例如 HTTP 请求。

在任何情况下，异步任务对于正在运行的 JS 代码的其余部分都是非阻塞的，这使得它们非常适合于长时间运行的请求以及通常需要更长时间才能完成的功能。

## 异步脚本

首先，不要与`**async / await**`混淆的是异步脚本标签。我们可以通过将 HTML 中包含的脚本声明为`**async**`来实现异步脚本加载。

```
# Async script
<script async src="..."></script>
```

传统上，呈现 HTML 的浏览器会同步加载和执行脚本，除非我们添加了`**async**` 关键字。这将让浏览器知道我们希望脚本异步加载*，而不会阻止*解析有问题的 HTML。

这不要与 async / await 混淆，因为这是一个不同的概念，但对于异步加载 JavaScript 文件还是很有用的。

## 异步/等待

JS 代码块和函数本身的异步执行总是通过`**async / await**` 关键字来引用。

为了在 JS 中声明一个异步函数，我们使用了`**async**`关键字。

```
# Async function
async function sum(param1, param2) {
    return param1 + param2;
}
```

现在，仅仅计算一个总和是一个可怕的例子，正如我们已经说过的——async 主要用于长时间运行的任务，但是为了这个例子，上面是我们如何声明一个异步函数。这个函数可以像其他函数一样使用——但是，这样一个函数是如何执行的，返回值是如何使用的？我们使用`**await**`就是为了这个。

```
# Await an asynchronous function
let result = await sum(1, 2);
```

现在这里有一个小问题——await 只能在异步函数中使用。这可能有点不直观，但是为了从异步函数获得返回值，我们需要使用承诺。

简而言之，如果您检查从`**sum**`返回的值，您会看到它已经是一个承诺了。我们可以在`**then**`方法中使用实际计算值。

```
# Promise - Then
sum(1, 2).then(result => console.log(result)); 
```

JavaScript 中的 Async / await 实际上是建立在承诺之上的，这就引出了下一个问题。

# 承诺

![](img/a518a9a833c2e79f6d25e6bddfb9574e.png)

If you need to give a promise to someone in sign language — Credit [How to sign PROMISE in ASL?](https://www.youtube.com/watch?v=HCFv9ZPJGu0)

理解承诺最简单的方法就是想象这是某人给你的一个字面上的承诺——例如，我答应你我会打扫房子。

任务本身对您来说是异步的，它不是由您执行，而是由我执行——一旦完成，我会通知您结果。还有一点要记住的是，我可能会在任务中失败，但我会告诉你结果。

然而，值得注意的是——JavaScript 首先带来了承诺，然后是 async / await，所以很多人会争论你是否应该坚持这些承诺，但是为了概念的缘故——这里有一个关于承诺如何工作的快速示例。

```
let promise = new Promise((resolve, reject) => {
    // Long running task
    let result = someGetFunction();
    if (result.success) {
        resolve(result.data);} else {
        reject(result.error.message);
    }
});promise.then(result => {
    console.log(result);
}).catch(error => {
    console.log(error);
});console.log("Promise has finished, didn't it?");
```

上面的代码块看起来像是在最后一行之前首先记录了`**promise**`的结果或错误，但实际上，如前所述——异步任务，在这种情况下，承诺意味着长期运行的执行。

发出获取数据的 HTTP 请求是一个长时间运行的任务，解析包括最后一行日志在内的整个代码块肯定会比我们的引擎花费更长的时间。

上面的代码块也很好地说明了任务是如何在后台执行的，而不会妨碍我们的解析器检查其余的代码。

除了上述内容，开发人员还必须了解和学习许多 JavaScript 概念。

有些不太重要，有些更重要，但希望本文突出并关注其中的几个，并帮助您更好地理解它们。

如果你是一个正在阅读这篇文章的开发者，我希望它对你的旅程有所帮助，不管你是刚刚开始还是已经有很多年的经验了。请不吝赐教，提出更多有可能帮助到别人的概念！

感谢您的阅读！🎉

—

如果你喜欢阅读这篇文章，并认为它很有趣，请查看每个程序员都应该知道的 v 1 . 0 . 2JavaScript 概念。

[](https://be-ja.medium.com/javascript-concepts-every-programmer-should-know-v1-0-2-cc87f541e05) [## 每个程序员都应该知道的 JavaScript 概念

### 最近，我在每个程序员都应该知道的 JavaScript 概念中写了一篇关于 JS 的文章，社区反馈非常好。

be-ja.medium.com](https://be-ja.medium.com/javascript-concepts-every-programmer-should-know-v1-0-2-cc87f541e05) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***