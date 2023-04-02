# 为什么我更喜欢在 Web 应用程序中使用 Axios

> 原文：<https://javascript.plainenglish.io/why-i-prefer-axios-in-web-app-9a78d655fd1d?source=collection_archive---------10----------------------->

## 同构和基于承诺的代码使开发更加高效

![](img/c948cdb5875b695f2eaa1d2b024b2dd1.png)

Photo by [Campaign Creators](https://unsplash.com/@campaign_creators?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 前言

在过去的 8 年里，我为三家公司工作过，并为每家公司开发了许多 web 应用程序。创建新项目时，我总是喜欢用 axios 作为 HTTP 请求库。 [axios 网站](https://axios-http.com/docs/intro)介绍了许多功能:

从浏览器发出 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)

从 Node.js 发出 [HTTP](http://nodejs.org/api/http.html) 请求

支持[承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API

拦截请求和响应

转换请求和响应数据

取消请求

JSON 数据的自动转换

客户端支持防止 [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

但我认为我喜欢使用 axios 有三个主要原因:

1.  它是基于承诺的，易于编写异步代码。
2.  它是同构的，可以用相同的代码库在浏览器和 Node.js 中运行。
3.  支持拦截器可以拦截请求和响应。

# 基于承诺的

当我刚开始工作时，没有承诺，需要回调来处理响应。如果我们想从不同的 API 中顺序获取数据，我们必须将请求放入回调中。就像这样:

```
// this function request data from server
function ajax(url: string, successCallback: Function, errorCallback:Function): void {
}// fetch data sequentially
ajax('/url1', function success() {
    ajax('/url2', function() {
        // fetch more data;
        ...
    }, function() {});
}, function error() {})
```

如果我们想从更多不同的 API 获取数据，就会有更多嵌套的回调。代码变得越来越深，越来越难以管理，特别是如果我们有真正的代码，而不是可能包含循环、条件语句等等的`...`。

这被称为“回调地狱”或“末日金字塔”

感谢上帝，承诺很快就出现了，提供连锁电话，以避免这样的金字塔。

通过使用 promise，代码将如下所示:

```
function ajax(url: string): Promise {
}ajax('/url1').then(function() {
    return ajax('/url2');
}).then(function() {
    return ajax('/url3');
})
```

我们可以在承诺上调用`.then`任意多次，与回调相反，承诺给了代码更多的流程和灵活性。

# 同形的

在我的 web 应用程序中，我经常需要使用 Node.js 来提供来自不同 API 的数据聚合。所以需要发送 HTTP 请求来获取 Node.js 中的数据，如果没有 axios，就这样在 Node.js 中取一个 JSON 数据(演示来自 [Node.js 网站](https://nodejs.org/dist/latest-v16.x/docs/api/http.html#httpgetoptions-callback)):

```
const http = require('http');http.get('[http://localhost:8000/'](http://localhost:8000/'), (res) => {
  const { statusCode } = res;
  if (statusCode !== 200) {
    error = new Error('Request Failed.\n' +
                      `Status Code: ${statusCode}`);
  } else if (!/^application\/json/.test(contentType)) {
    error = new Error('Invalid content-type.\n' +
                      `Expected application/json but received ${contentType}`);
  }
  if (error) {
    console.error(error.message);
    // Consume response data to free up memory
    res.resume();
    return;
  }res.setEncoding('utf8');
  let rawData = '';
  res.on('data', (chunk) => { rawData += chunk; });
  res.on('end', () => {
    try {
      const parsedData = JSON.parse(rawData);
      console.log(parsedData);
    } catch (e) {
      console.error(e.message);
    }
  });
}).on('error', (e) => {
  console.error(`Got error: ${e.message}`);
});
```

要使用 HTTP 模块发送请求，您需要侦听许多事件，处理数据块，然后将数据解析为 JSON 格式。而且不是基于承诺的，我们多半会遇到“回调地狱”。

幸运的是，axios 支持 Node.js。我们可以像在浏览器中一样获取数据。不仅代码风格相同，而且我们还可以重用请求逻辑，只需编写一次代码，就可以在 browser 和 Node.js 中运行。重用代码片段非常重要，因为随着项目变得越来越复杂，如果同一请求有许多不同的实现，维护可能会是一场灾难。如果需要修改，很容易漏掉一些，效率非常低。

# 拦截机

这是我最喜欢的 axios 特性，我们可以在请求或响应被`then`或`catch`处理之前拦截它们。无论是浏览器还是 Node.js 提供的请求方法，都只是最原始的请求函数实现，缺乏对 web apps 的适配。在 web app 开发过程中，需要注意开发效率和代码可维护性，所以代码最好是高内聚低耦合的。axios 的拦截器使得与请求相关的代码更具内聚性。

如果没有拦截器，我们可以在每个请求动作之前使用 utils 来处理请求参数。可能是:

```
// processParams method use to serialization params
ajax('/url1', processParams(params1));ajax('/url2', processParams(params2));
```

有了拦截器，我们可以这样做:

```
axios.interceptors.request.use(function (config) {     
  // Do something before request is sent
  processParams(config.params);    
  return config;   
});
axios.get('/urlX', paramsX);
```

使用拦截器可以很容易地实现定制的动作，比如参数序列化、参数验证、异常处理等等。

# 结论

在开发 web 应用时，使用 axios 作为 HTTP 请求库可以使我们的开发更高效，代码更易于维护。在这篇文章中，我分享了我喜欢 axios 的三个原因:

1.  基于承诺的
2.  同形的
3.  拦截机

你也这么认为吗？期待你关注我，我会分享更多的开发技巧，帮助你成为更好的程序员。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*