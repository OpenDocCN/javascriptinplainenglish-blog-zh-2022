# Promises 和 async/await 是 JavaScript 中处理异步代码的强大工具

> 原文：<https://javascript.plainenglish.io/promises-and-async-await-are-powerful-tools-for-handling-asynchronous-code-in-javascript-cf3463a4def8?source=collection_archive---------7----------------------->

![](img/b88aaca1f020202a8e55151474f111a4.png)[](https://www.youtube.com/channel/UCw7mp55bjIqhSeAVwir7fXg) [## 简易网站

### 朋友们好，欢迎来到我们的频道“易网站”。我创建这个频道的目的是帮助你学习网站…

www.youtube.com](https://www.youtube.com/channel/UCw7mp55bjIqhSeAVwir7fXg) 

Promises 和 async/await 是 JavaScript 中处理异步代码的强大工具，在使用 Node.js 时尤其有用。下面是如何在 Node.js 中使用 Promise 和 async/await 的简要指南:

1.  承诺:承诺是表示异步操作最终完成或失败的对象。您可以使用 promise 来包装一个异步函数，并在它准备好的时候处理它的结果。

下面是一个在 Node.js 中如何使用 promise 的例子:

```
function asyncFunction() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Async function completed');
    }, 1000);
  });
}

asyncFunction().then(result => {
  console.log(result); // 'Async function completed'
});
```

2.Async/await: Async/await 是一种语法，允许您以更同步的方式编写异步代码。它建立在承诺的基础上，使得使用异步函数和处理它们的结果变得更加容易。

下面是一个如何在 Node.js 中使用 async/await 的例子:

```
async function asyncFunction() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Async function completed');
    }, 1000);
  });
}

async function main() {
  const result = await asyncFunction();
  console.log(result); // 'Async function completed'
}

main();
```

正如您所看到的，使用 async/await 使得使用异步函数和处理它们的结果变得更加简单。只要确保在`async`函数中使用`await`关键字，并用`await`关键字包装你调用的任何异步函数。

下面是一个在 Node.js 中使用 async/await 调用 API 的例子:

```
const axios = require('axios');

async function getData() {
  try {
    const response = await axios.get('https://example.com/api/endpoint');
    return response.data;
  } catch (error) {
    console.error(error);
  }
}

async function main() {
  const data = await getData();
  console.log(data);
}

main();
```

这段代码使用`axios`库向指定的 API 端点发出 HTTP GET 请求。`await`关键字用于暂停`main()`函数的执行，直到 API 请求完成。如果请求成功，API 返回的数据将被记录到控制台。如果请求失败，控制台会记录一个错误。

请记住，这只是一个基本的例子，您可能需要根据您的 API 和您想要的用例的具体需求来修改它。例如，您可能需要包含身份验证头、传递查询参数或表单数据，或者处理分页。

我希望这有助于您了解如何使用 async/await 调用 Node.js 中的 API。

使用 async/await 的另一篇文章示例

[](https://easywebsify.medium.com/how-to-return-response-from-an-asynchronous-call-in-javascript-ee70abb1c51) [## 如何在 JavaScript 中从异步调用返回响应

### 您可以使用 async/await 语法使 foo 函数异步，如下所示:

easywebsify.medium.com](https://easywebsify.medium.com/how-to-return-response-from-an-asynchronous-call-in-javascript-ee70abb1c51) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***