# JavaScript 代理初学者指南

> 原文：<https://javascript.plainenglish.io/javascript-proxies-a-beginners-guide-2aceeab0a098?source=collection_archive---------3----------------------->

## JavaScript 中的代理概述。

![](img/20aeed03e2adddb7e77547b96f78d5d9.png)

JavaScript 中的代理是语言中隐藏的瑰宝之一，大多数 JavaScript 初学者和中级开发人员都不知道。根据 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 文档，`Proxy`对象允许你创建一个可以用来代替原始对象的对象，但是它可以重新定义基本的`Object`操作，比如获取、设置和定义属性。

从定义上看，代理可以用来干预对象的底层操作，例如，你可以扩展如何在函数上设置属性，你可以在定义如何设置或打印对象属性之前执行一些操作，等等。

为了解释这一点，请考虑一个场景，其中有一个表示用户配置文件的对象。

```
const profile = {
  username: "Anderson",
  image: "/path/to/img"
}
```

在我们的应用程序中，我们希望能够更新用户名。但是在用户更新他们的用户名之前，您需要验证该名称是否被其他用户使用。一种方法是编写一个函数来验证用户名是否有效，另一种方法是使用代理。

我们首先初始化一个`Proxy`对象的实例。构造函数接受两个参数:

*   **目标**:你要代理的对象。
*   **Handler** :定义哪些操作将被拦截，以及如何重新定义被拦截的操作的对象。

```
let profile_proxy = new Proxy(profile, {/* handler blank for now */}
```

至此，我们已经为概要文件对象创建了一个代理。现在要看的主要是 handler 对象。它用于确定我们想要在对象上定制的行为。首先，让我们定义一个`set`属性。正如你可能猜到的，`set`属性用于定制对象的设置方式。这是一个接受三个参数的函数。

*   对象:这是原始对象
*   Prop:您试图设置的属性
*   值:要分配给属性的值。

所以让我们重新定义我们的处理程序。

```
const handler = {
    set: (obj, prop, value) {
        if (/* certain condition is met */) {
            obj[prop] = value
            return true;
        } else {
            throw new Error("Required condition not met")
        }
    }
}
```

现在，我们可以在启动代理时传递 handler 对象:

```
const profile_proxy = new Proxy(profile, handler)
```

现在，如果您试图将`profile_proxy`对象中的`username`设置为一个新值，它将首先评估您设置的条件，然后尽可能设置该对象，或者抛出一个新错误。

注意:在初始化一个代理后，当试图修改变量时，你可以从代理中修改它，例如在上面的例子中你可以改变`profile_proxy.username`而不是`profile.username`，如果你调用`profile.username`自定义设置器将不会运行。

现在让我们定义 get 方法。

```
const handler = {
  get(obj, prop) {
    return prop in obj ?
      obj[prop] :
      "Not found";
  }
};
```

如果试图访问对象中的属性，将调用 get 方法。就像吸气剂一样。

```
// If we run:
console.log(profile_proxy.some_missing_method)
// Output: "Not found"
```

从上面的例子中，您可能意识到创建一个全新的变量会使代码看起来很奇怪，所以更好的方法是:

```
profile = new Proxy(profile, handler)
// Or instead of first defining the object then create a proxy you can do thisconst profile = new Proxy({/* All values in here*/}, handle)
```

这是代理的一个简单概述，现在让我们看看代理在真实项目中的实际应用。

*   Vue.js 3:根据 Vue.js 文档，vue.js 的最新版本 Vue 3 利用 JavaScript 代理来实现反应式数据。对于`reactive`功能。这里声明:

[](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#script-setup) [## 反应性基础| Vue.js

### API 首选项本页和本指南后面的许多章节包含选项 API 和…的不同内容

vuejs.org](https://vuejs.org/guide/essentials/reactivity-fundamentals.html#script-setup) 

*   [Orbiton JS](https://orbiton.js.org) :也利用 JavaScript 代理创建代理绑定器，其行为方式与 Vue.js 的反应数据相同。

我希望这篇文章能帮助你理解代理。如果您想了解更多信息，可以访问 MDN 文档:

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) [## 代理- JavaScript | MDN

### 代理对象使您能够为另一个对象创建代理，它可以截取和重新定义基本的…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**