# 如何优雅地封装 Axios，可以这样做

> 原文：<https://javascript.plainenglish.io/how-to-encapsulate-axios-elegantly-you-can-do-this-a81da0b0bf1c?source=collection_archive---------3----------------------->

![](img/e2f21688a2b3f0ffa8a9ad9951a5d8d3.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

看过很多类似的文章，但是付诸实践的时候总是有疑问:**这些看似高级的二次封装会不会让 Axios 的调用方法变得更加复杂**？

我认为优秀的二次包装具有以下特点:

*   **可以改善原生框架的不足**:明确原生框架的不足，在二次打包后可以消除这些不足，同时不会引入新的不足。
*   **保留原函数**:新框架的 API 在进行二次封装时，可能会改变原生框架的 API 的调用方法(比如传递参数的方法)，但我们必须保证原生 API 上的所有函数都可以通过新 API 调用。
*   **理解成本低**:有使用原生框架经验的开发者，面对重新封装的框架和 API 时，可以快速理解并上手。

下面我将首先描述底层封装，然后描述如何优雅地封装。

# 1.低级包装

## 1.1 将一个特定的方法封装到一个新的 API 中，但是只暴露很少的参数

例如下面的代码:

```
export const post = (url, data, params) => {
  return new Promise((resolve) => {
    axios
      .post(url, data, { params })
      .then((result) => {
        resolve([null, result.data]);
      })
      .catch((err) => {
        resolve([err, undefined]);
      });
  });
};
```

上面的代码中封装了`method`为`post`的请求方法，用来解决原生 API 中处理错误时需要使用`try~catch`的问题。但是这种封装有一个缺点:整个`post`方法只公开了三个参数`URL`、`data`和`params`，通常这三个参数可以满足大多数简单的请求。但是如果我们遇到一个特殊的`post`接口，响应时间很慢，需要设置一个很长的超时，上面的`post`方法就会立刻打嗝。

`axios.post`上述特殊场景可以通过原生方法轻松处理，如下所示:

```
axios.post("/submit", form, { timeout: 15000 });
```

类似的特殊场景还有很多，比如:

*   需要上传一个表单。表单不仅包含数据，还包含文件。只能设置`headers["Content-Type"]`到`"multipart/form-data"`进行请求。如果要显示上传文件的进度条，还必须设置`onUploadProgress`属性。
*   有一个接口需要防止数据竞争，只能设置`cancelToken`或`signal`。有人说拦截器可以用来避免种族并发`interceptors`。我举一个场景来反对这个:如果同一个页面上有两个或更多的下拉框，两个下拉框都会调用同一个接口来获取下拉选项，那么你的避免拦截器实现的数据竞争的机制就会有问题，因为这些下拉框中只有一个请求不会被中断。

有的开发者会说这种接口不会出现，约定好的`post`接口都只需要这三个参数。对此我想反驳一下:有潜力的项目总会增加更多的要求，如果你觉得你的项目没有潜力，那我没说。但是如果你不确定将来是否会有更多的特性添加到你的项目中，或者你是否会遇到这样的特殊场景，那么请在第二个包中尽可能地保持与原来的`API`一致，并确保**原来的** `**API**` **能做到的一切，第二个包** `**API**` **后的新包也能做到**。为了避免遇到以上特殊情况`API`时的尴尬修改，为了兼容，会有特别难看的写法。

## 1.2 封装`Axios is` 创建一个实例的方法，或者封装一个自定义的`Axios` 类

例如下面的代码:

```
const createAxiosByinterceptors = (config) => {
  const instance = axios.create({
    timeout: 1000,
    withCredentials: true,
    ...config,
  });
  instance.interceptors.request.use(xxx, xxx);
  instance.interceptors.response.use(xxx, xxx);
  return instance;
};

class Request {
  instance: AxiosInstance
  interceptorsObj?: RequestInterceptors
  constructor(config: RequestConfig) {
    this.instance = axios.create(config)
    this.interceptorsObj = config.interceptors
    this.instance.interceptors.request.use(
      this.interceptorsObj?.requestInterceptors,
      this.interceptorsObj?.requestInterceptorsCatch,
    )
    this.instance.interceptors.response.use(
      this.interceptorsObj?.responseInterceptors,
      this.interceptorsObj?.responseInterceptorsCatch,
    )
  }
}
```

以上两种编写方法用于创建不同配置和不同拦截器的多个`Axios`实例，以应对多种场景。对此我想表达一下我的观点:**一个前端项目中只能存在一个** `**Axios**` **实例**。多个`Axios`实例会增加代码理解的成本，让参与或接手项目的开发者花更多的时间去思考和接受每个实例的`Axios`用途和场景，就像拥有多个`Vuex`或`Redux`同样无用的项目一样。

那么有些开发者会问，如果有相当数量的接口需要使用不同的配置和拦截器怎么办？我来分析两种场景:**多配置**和**多拦截器:**

## 1.3 多种配置下的处理方式

如果有两个或更多不同的配置，这些配置中的每一个都由接口的一部分使用。然后你要声明不同配置对应的常数，然后`Axios`调用时传入对应的配置常数，如下:

```
const configA = {
  // ....
};
const configB = {
  // ....
};
axios.get("api1", configA);
axios.get("api2", configB);
```

相比不同配置的多个`Axios`例子，上述写法更直观，让看代码的人直接看出区别。

## 1.4 多拦截器下的处理方法

如果有两个或更多不同的拦截器，这些拦截器中的每一个都被一些接口使用。然后，**我们可以将这些拦截器挂载到一个全局唯一的** `**Axios**` **实例**上，然后允许拦截器通过以下两种方式被选择性地执行:

**推荐** : `config`增加一个自定义属性来决定拦截器是否被执行。代码如下:

调用请求时，书写方法如下:

```
instance.get("/api", {
  enableIcp: true,
});
```

在拦截器中，我们这样编写逻辑

```
instance.interceptors.request.use(
  (config: RequestConfig) => {
    const { enableIcp } = config;
    if (enableIcp) {
      //...
    }
    return config;
  },
  (error) => {
    const { config } = error;
    const { enableIcp } = config;
    if (enableIcp) {
      //...
    }
    return error;
  }
);

instance.interceptors.response.use(
  (response) => {
    const { config } = response;
    const { enableIcp } = config;
    if (enableIcp) {
      //...
    }
    return response;
  },

  (error) => {
    const { config } = error;
    const { enableIcp } = config;
    if (enableIcp) {
      //...
    }
    return error;
  }
);
```

通过上面的编写，我们可以`config.enableIcp`来判断注册的拦截器是否被执行了。以此类推，我们`config`在编写拦截器时，通过插入自定义属性和协作，可以完美地控制单个或多个拦截器的执行。

**二级推荐**:使用`Axios`官方`runWhen`属性来决定是否执行拦截器。**注意该属性只能决定请求拦截器是否执行，不能决定响应拦截器是否执行**。用法如下:

```
function onGetCall(config) {
  return config.method === "get";
}
axios.interceptors.request.use(
  function (config) {
    config.headers.test = "special get headers";
    return config;
  },
  null,
  { runWhen: onGetCall }
);
```

# 2.优雅的包装

使用方法如下:

```
apis[method][url](config);
```

对应接口的`method`请求方法是`url`接口路径，`config`是`AxiosConfig`，即配置。

返回结果的数据类型是:

```
{
  data: null | T;
  err: AxiosError | null;
  response: AxiosResponse<T> | null;
}
```

我们来展示一下使用效果:

## **2.1** 支持 url 智能推导，根据输入的 url 推导出所需的参数和数据。当请求参数丢失或写入错误时，将出现 ts 错误消息

以两个接口为例:

*   路径是`/register`，方法是`post`，`data`类型是`{ username: string; password: string }`
*   路径是`/password`，方法是`put`，`data`类型是`{ password: string }`，`params`数据类型是`{ username: string }`

这样我们就不再需要通过一个函数来执行请求接口逻辑，而是可以直接`API`通过调用来执行请求接口逻辑。如下所示:

```
function register(
  data: { username: string; password: string },
  config: AxiosConfig
) {
  return instance.post("/register", data, config);
}

const App = () => {
  const registerAccount = async (username, password) => {
    const response = await register({ username, password });
    //...
  };

  return <button onClick={registerAccount}>sign</button>;
};

const App = () => {
  const registerAccount = async (username, password) => {
    const response = await apis.post["/register"]({ username, password });
    //... 
  };

  return <button onClick={registerAccount}>sign</button>;
};
```

以前我们要在一个组件中调用前端代码写的接口，需要先知道接口`url`(如上`/register`)，然后`url`在前端代码`register`中找到接口(如上)对应的请求函数。而如果在本文中使用这种方法，我们只需要知道`url`。

这样做的另一个好处是防止接口的重复记录。

## 2.2 支持返回结果的智能推导

以一个接口为例:

*   路径为`/admin`，方法为`get`，返回结果的数据类型为`{admins: string[]}`

## 2.3 支持错误捕获，无需编写`try~catch`包处理

调用时的书写方法如下:

```
const getAdmins = async () => {
 const { err, data } = await apis.get['/admins']();
 if (err) {
   //.. 

   return
 };
 setAdmins(data!.admins);
};
```

## 2.4 支持路径参数，也将智能导出路径参数

以一个接口为例:

*   路径为`/account/{username}`，方法为`get`，需要`username`路径参数

书写方法如下:

```
const getAccount = async () => {
  const { err, data } = await apis.get["/account/{username}"]({
    args: {
      username: "123",
    },
  });
  if (err) return;
  setAccount(data);
};
```

# 最后

**感谢阅读**。期待您的关注，阅读更多高质量的文章。

![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----a81da0b0bf1c--------------------------------)

## 更好的编程

[View list](https://medium.com/@omgzui/list/better-programing-9b4c9bb174aa?source=post_page-----a81da0b0bf1c--------------------------------)109 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----a81da0b0bf1c--------------------------------)

## Java Script 语言

[View list](https://medium.com/@omgzui/list/javascript-48bfc7b5f93c?source=post_page-----a81da0b0bf1c--------------------------------)57 stories![](img/64fcf15e27c514ec49d62966b68dbc15.png)![](img/3e6ce891363c151131c5993ca0dcc526.png)![](img/a7dd413de22f319a3c4729c9e737feb8.png)![omgzui](img/113db82933227743d0067a68e250ac93.png)

[omgzui](https://medium.com/@omgzui?source=post_page-----a81da0b0bf1c--------------------------------)

## 新闻

[View list](https://medium.com/@omgzui/list/news-67ec0a972660?source=post_page-----a81da0b0bf1c--------------------------------)23 stories![](img/c3f36b36bf050f98fd5a8e3c89103cad.png)![](img/8459df5aae62dc00f04377e09544be88.png)![](img/2864058bcedc8c1cd6492624ba9671c6.png)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*