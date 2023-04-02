# 如何在 React 中获取数据

> 原文：<https://javascript.plainenglish.io/how-to-fetch-data-in-react-d59d6ee09aaf?source=collection_archive---------1----------------------->

## 在 React 中从 API 获取数据的 5 种方法(附示例)

![](img/f7d66a13726abdf32132ee65827bac71.png)

在本文中，我将向您展示在 React 中从 API 获取数据的五种不同方式:

1.  获取 API
2.  异步等待语法
3.  Axios 库
4.  自定义挂钩(使用 Fetch)
5.  React 查询库

在示例中，我们将使用随机数据生成器。API 端点如下:[https://random-data-api.com/api/food/random_food](https://random-data-api.com/api/food/random_food)，它返回关于不同食物的随机数据😋。

# 1.获取 API

**获取 API** 可能是 React 中获取数据的最基本方式。
这个工具内置在大多数现代浏览器的窗口对象(window.fetch)上，允许我们使用`GET`、`POST`和其他方法发出 HTTP 请求。

让我们定义一个名为`getData()`的箭头函数，它使用 fetch 发出一个简单的`GET`请求。

```
const getData = () => {
 return fetch('[https://random-data-api.com/api/food/random_food](https://random-data-api.com/api/food/random_food)')
  .then((response) => response.json())
  .then((data) => console.log(data));
};
```

这个函数将 URL 端点传递给 fetch 方法，然后接受`Response`对象，将结果转换成 JSON 对象并打印到控制台。

现在我们知道了它是如何工作的，让我们尝试使用`fetch()`来显示组件内部的一些数据:

Fetch API example

在这个`App`组件中，我们定义了启动请求并返回承诺的`fetchFood()`函数。当请求完成时，用`Response`对象解析承诺。如果响应成功，(`response.ok`)，我们使用`json()`方法将响应转换成 JSON 数据。这将返回一个包含我们从随机食品 API 中获取的数据的承诺。在`then()`方法中，我们使用`setFood()`将食物的状态设置为新数据。

但是，如果请求由于网络问题而失败，则承诺会被拒绝。
使用 fetch，我们需要自己处理错误，所以我们抛出`response`作为要由`catch`回调处理的错误，这里我们将状态中“error”的值设置为承诺的错误值。

当承诺兑现时，无论成功与否，我们都知道它不再装载。
我们使用`.finally()`回调将`loading`设置为 false，因此我们不再看到我们的加载文本。

如果请求成功，我们将在页面上看到数据。否则，将显示带有错误状态的“错误”字样。

为了在我们的反应组件挂载后发出这个请求，我们在`useEffect()`中调用`fetchFood()`函数，并确保提供一个空的依赖数组作为第二个参数，这样我们的请求只发出一次。

点击“新盘”按钮，我们再次调用`fetchFood()`功能，提出新的请求，获取新的数据。

# 2.异步等待语法

`async/await`语法非常适合`fetch()`，因为它通过承诺简化了工作。

主要的好处是，它允许我们删除`then()`回调，并简单地取回异步解析的数据。

事实上，`await`表达式通过暂停执行直到返回的承诺被实现或拒绝，使得承诺返回函数表现得好像它们是同步的。

当我们提出请求时，我们可以在`fetch()`前面添加`await`，等待承诺与结果达成一致。

要使用这个语法，我们必须在`async`内部调用它，所以我们必须在`getchData()`函数前面添加`async` 。

让我们用这个新语法重写我们的`getData()`:

```
*async* function getData() {
 try { 
  const response = await fetch('[https://random-data-api.com/api/food/random_food](https://random-data-api.com/api/food/random_food)');
  if (!response.ok) {
   throw new Error(`HTTP error: ${response.status}`);
  }
  const data = await response.json();
  console.log(data);
 } catch (error) {
  console.error(`Something went wrong: ${error}`);
 }
}
```

现在我们可以对我们的`App`组件进行同样的重构。

Async-await example

`fetchFood()`现在是一个异步函数，因为它用`async`关键字标记，我们可以删除回调，简单地取回异步解析的数据。

需要注意的是，当我们使用`useEffect`钩子时，效果功能不能被`async`实现。

# 3.Axios 库

Axios 是一个基于承诺的 Javascript 库，用于执行 HTTP 请求。它的工作方式与 Fetch API 非常相似，但是主要的好处是它已经将结果作为 JSON 对象返回，所以我们不需要对其进行转换。

要使用这个库，我们必须用 npm 安装它:

```
npm install axios
```

我们现在可以将其导入到我们的项目中，并在相同的函数`getData()`中使用，而不是`fetch()`方法:

```
import axios from "axios"const getData = () => {
 return axios.get('[https://random-data-api.com/api/food/random_food](https://random-data-api.com/api/food/random_food)')
  .then((response) => console.log(response.data));
};
```

使用 Axios，我们可以编写更少的代码，此外，这个库包含了许多简单的 Fetch 所没有的工具和特性。

让我们也使用 Axios 修改`App`组件。

Axios example

与`fetch()`方法相比，这种方法更简单明了。

# 4.自定义钩子(useFetch)

我们可以使用来自`react-fetch-hook`库的`useFetch`钩子来进一步简化数据获取。
这已经包括了我们可以用来处理错误的属性，比如`isLoading`和`error`。

首先，我们必须用 npm 安装库:

```
npm install react-fetch-hook
```

接下来，我们可以将它导入到组件中:

```
import useFetch from "react-fetch-hook";
```

Custom hooks (useFetch) example

现在我们可以将端点 URL 传递给对象的`useFetch`钩子和析构函数`data, isLoading, error`，然后我们可以在渲染中使用它们。

在这种情况下，我们不需要在本地状态中处理数据、加载和错误，而是直接从我们的请求中获取它们。

# 5.反应查询

我最喜欢在 React 中获取数据的方式是使用`react-query`库。它支持缓存和重新提取，帮助开发人员改善整体用户体验，并使我们的应用程序更快。

让我们安装它:

```
npm i react-query
```

首先，在`index.js`文件中，我们必须用从`react-query`导入的`QueryClientProvider`包装我们的`App`组件，并将客户端实例传递给它:

```
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { QueryClient, QueryClientProvider } from "react-query";
import { ReactQueryDevtools } from "react-query/devtools";
import App from "./App";*// Create a client* const queryClient = new QueryClient();const rootElement = document.getElementById("root");
const root = createRoot(rootElement);root.render(
  *// Provide the client to your App* <StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
      <ReactQueryDevtools initialIsOpen={false} /
    </QueryClientProvider>
  </StrictMode>
);
```

React Query 提供了一个定制的钩子，我们可以在组件之间重用它来获取数据。

它还为我们提供了`ReactQueyDevtools`，一种控制何时、如何以及多久获取一次数据的好方法。

让我们看看这个库在我们的`App`组件中的运行情况。

为了获取数据，我们从`react-query`调用`useQuery`钩子，并传递一个惟一的查询键(在本例中为“random-food”)和一个查询用来获取数据的函数:

然后，我们可以析构返回的对象，并在渲染中使用我们需要的信息。

React Query，首先尝试从其缓存中提供我们的数据，然后，如果我们的 API 状态发生了变化，则在后台更新数据以显示变化。

事实上，通过引用我们在钩子中传递的查询键，我们可以重新提取、验证或重置查询，如`refetchData`函数所示:

```
const refetchData = () => {
  queryClient.invalidateQueries("random-food");
};
```

React Query 经常被描述为 React 缺少的数据获取库，因为它使 React 应用程序中的获取、缓存、同步和更新服务器状态变得轻而易举。你可以在这里读到它所有的优点[。](https://tanstack.com/query/v4/docs/overview?from=reactQueryV3&original=https://react-query-v3.tanstack.com/overview)

## **结论**

我希望这篇文章能教会你一些东西。如果你知道从 API 获取数据的其他方法，请在评论中添加！

*考虑* [***成为中等成员***](https://ebelinggianmarco.medium.com/membership)**如果你喜欢看这样的故事，并且想帮助我这个作家。每月 5 美元，你可以无限制地访问媒体内容。如果你通过* [***我的链接注册，我会得到一点佣金。***](https://ebelinggianmarco.medium.com/membership)*

**更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**