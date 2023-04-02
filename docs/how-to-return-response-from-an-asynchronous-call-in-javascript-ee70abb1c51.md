# 如何在 JavaScript 中从异步调用返回响应

> 原文：<https://javascript.plainenglish.io/how-to-return-response-from-an-asynchronous-call-in-javascript-ee70abb1c51?source=collection_archive---------6----------------------->

![](img/15336aae87c59f34052fd08b135375a9.png)

Photo by [Dan Burton](https://unsplash.com/@dan__burton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您可以使用 async/await 语法使 foo 函数异步，如下所示:

```
async function foo() {
    try {
        const response = await axios.get('...');
        return response.data;
    } catch (error) {
        console.error(error);
    }
}
```

这段代码使用 axios.get 方法向指定的 URL 发送 get 请求，并使用 await 关键字等待响应。response.data 属性包含服务器返回的实际数据。

如果您喜欢基于回调的方法，可以使用以下代码:

```
function foo() {
    return new Promise((resolve, reject) => {
        axios.get('...')
            .then(response => resolve(response.data))
            .catch(error => reject(error));
    });
} 
```

这段代码返回一个新的承诺，该承诺用服务器返回的数据进行解析，或者如果请求失败，则用错误拒绝。您可以使用 then 和 catch 方法分别处理已解析或已拒绝的承诺。

例如:

```
foo().then(data => console.log(data)).catch(error => console.error(error));
```

这段代码记录服务器返回到控制台的数据，或者在请求失败时记录错误。

使用 async/await 语法使 foo 函数异步的另一个例子是，您可以执行以下操作:

```
async function foo() {
  try {
    const response = await axios.post(‘/some/endpoint’, { some: ‘data’ });
    console.log(response.data);
    return response.data;
  } catch (error) {
    console.error(error);
  }
}
```

这将使用 axios 库向/some/端点发送一个 POST 请求，并在继续下一行代码之前等待响应。如果请求成功，response.data 将被记录到控制台。如果有错误，它将被捕获并记录到控制台。

另一篇文章提到:

[](/promises-and-async-await-are-powerful-tools-for-handling-asynchronous-code-in-javascript-cf3463a4def8) [## Promises 和 async/await 是 JavaScript 中处理异步代码的强大工具

### Promises 和 async/await 是 JavaScript 中处理异步代码的强大工具，它们在工作时特别有用…

javascript.plainenglish.io](/promises-and-async-await-are-powerful-tools-for-handling-asynchronous-code-in-javascript-cf3463a4def8) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****有兴趣规模化你的软件创业*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***