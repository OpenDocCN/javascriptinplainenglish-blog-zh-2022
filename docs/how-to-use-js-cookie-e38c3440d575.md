# 如何使用 js-cookie

> 原文：<https://javascript.plainenglish.io/how-to-use-js-cookie-e38c3440d575?source=collection_archive---------4----------------------->

![](img/e7b227e9f9bcff7ebc89a2f3a8e24243.png)

js-cookie 主要是用来方便存储 cookies 的操作。它简单易用。接下来，我们来看看 js-cookie 的用法。

我们都知道，平时使用 cookies 进行缓存时，主要有三种方式:存储、获取、删除。js-cookie 也是如此，它避免了本机操作 cookie 的繁琐。

## 原生 js 操作 cookies 的麻烦

首先，我们必须安装 js-cookie

```
npm install --save js-cookie
```

安装成功后，需要在使用的文件中调用它

```
import Cookies from 'js-cookie'
```

接下来就可以使用了

方法 1:保存(设置)

```
// Let's start with a simple example
Cookies.set('user', 'salted egg', { expires: 3, path: '' });
// Create a valid cookie and then you will have a field named user in the console cookies, and its value is salted egg gentleman
Cookies.set('user', 'salted egg', { expires: 3 });
// Create a cookie that expires 3 days from now
Cookies.set('user', 'salted egg', { expires: 3, path: '' });
// Create a 3-day expired cookie valid for the current page path
// Next store an object
const res = { user: 'salted egg', age: 18 };
Cookies.set('data', res);
// At the same time, another field named data appears in the console cookies and its value is an object
```

方法二:获取(Get)

```
// Now to get the data just stored
const user = Cookies.get('user')
// console.log(Cookies.get('user')) // salted egg
// Next, get the object you just saved
const res = JSON.parse(Cookies.get('data'))  // Note that if you do not add the name you want to get, it will return you all the data in the cookies
// console.log(res) // => { uesr: 'salted egg', ags: 18}
```

方法三:移除(remove)

```
Cookies.remove('user');
// Delete the data with the name user in the cookie
Cookies.remove('user', { path: '' });
// Delete cookies valid for current page path
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****