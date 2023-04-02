# 使用 postMessage 跨浏览器选项卡进行通信

> 原文：<https://javascript.plainenglish.io/communicate-across-browser-tabs-using-postmessage-fd1e37169952?source=collection_archive---------1----------------------->

## 在 JavaScript 中实现一个简单而强大的特性，该特性源自浏览器的窗口对象，称为 postMessage。

![](img/ab598948aafa9d6cc0ae98acfb6ffbfa.png)

嗨伙计们！在这篇文章中，我们将学习并实现 JavaScript 中一个最简单但功能强大的特性，它来自于浏览器的窗口对象 postMessage。在进一步探讨这个问题之前，让我展示一个用例，在这个用例中，这个漂亮的特性非常有用。

# 使用案例

让我们假设一旦用户登录到你的应用程序(例如:example.com)并保持空闲(为了简单起见，让我们认为用户在没有 API 调用时是空闲的)持续 10 分钟，我们希望用户强制注销，否则我们可以照常继续会话。

在另一个场景中，用户登录应用程序，通过点击当前标签上的某个链接导航到新标签(这可以是不同的域，例如:random.com ),并继续在新打开的标签上工作。(由于两个选项卡共享同一个会话，用户无需重新登录新选项卡)。

现在，在新选项卡上持续处于活动状态(API 调用被触发)后，用户在 10 分钟后从原始选项卡注销，因此会话在其他打开的选项卡上也过期。

简而言之，新打开的选项卡上的活动不会被视为原始选项卡/应用程序上的活动。然而，由于某种原因，原来的选项卡没有被通知新选项卡中正在执行的活动。

这正是我们想要解决的问题，这可以通过两个标签之间的沟通渠道来实现。让我们试着解决这个问题，看看 window 的 postMessage 如何成为我们的救星。

> `**window.postMessage()**`方法安全地启用了`Window`对象之间的跨原点通信；*例如，*在页面和它产生的弹出窗口之间，或者在页面和嵌入其中的 iframe 之间。
> 
> *语法:*
> postMessage(消息，目标来源)

# 活动发送者:新打开的选项卡

我们将利用`**window.opener**`派生`postMessage`方法。所以我们可以定义如下:

```
const winRef = window.opener;// NOTE: if you want to communicate from an iframe and winRef is coming as undefined, try below-
// const winRef = top.window.opener;
```

现在我们有了窗口引用对象，我们可以利用 postMessage 函数来发送数据:

```
winRef.postMessage("hello from nTab!", "http://example.com");// where, [http://example.com](http://example.com,) is targetOrigin where the message will be sent, our original tab (lets call it oTab)
```

> 请注意，出于安全原因，提供特定的 targetOrigin 非常重要，因为 postMessage 会将消息发送到浏览器中所有打开的标签，因此任何人都可以监听发送的数据(不太安全！).

在我们的例子中，我们已经从 oTab 窗口中打开了 nTab，所以我们也可以从`document`对象中获得 targetOrigin 值:

```
const targetOrigin  = document.referrer;winRef.postMessage("hello from nTab!", targetOrigin);
```

现在我们的目标是知道新选项卡上发生了一个活动(让我们用 domain random.com 称之为 nTab)。因为我们认为用户只有在 API 被触发时才是活动的，所以我们需要拦截 nTab 上发生的任何 API 调用。我们可以通过使用 XMLHttpRequest 实现这一点，如下所示:

```
XMLHttpRequest.prototype.send = function() { 
// intercept the request here 
}
```

因此，我们现在可以创建一个计数器，每当触发 API 时重置它，然后我们可以检查 setInterval，如果计数器值重置，则每隔 30 秒向 oTab 发送一次活动报告，然后递增计数器。代码如下:

```
const winRef = window.opener;const targetOrigin  = document.referrer;
const counter = 0;setInterval(function() {
    winRef.postMessage({tab: "nTab", isActive: counter === 0}, targetOrigin);
   couter++;
  }, 30000);XMLHttpRequest.prototype.send = function() { 
   counter = 0; 
}
```

# 活动接收者:原始页签

现在，在我们原来的选项卡 oTab 上，我们可以连续监听来自 nTab 的事件，并采取必要的措施:

```
window.addEventListener("message", (event) => {
  if (event.origin === "http://random.com") {
      if (event.data.isActive) {
         // activity happened in nTab
  }
 }    
}, false);
```

然后我们也可以在这里维护一个计数器来跟踪 oTab 上发生的活动。

```
const winRef = window.opener;
const counter = 0;setInterval(function() {
  window.addEventListener("message", (event) => {
      if (event.origin === "http://random.com" && event.data.isActive) {
         counter = 0;
   } else {
      couter++;
     }   
}, false);
  }, 60000);XMLHttpRequest.prototype.send = function() { 
   counter = 0;
}
```

现在，基于计数器值，我们可以注销用户，或者更新/继续会话。

```
if(counter > 9) { // 10min 
   window.location.href = '/logout'; 
   // we can also ask the user to re-login via a popup
  } else { 
      // session continues 
  }
```

我们现在有解决问题的方法了！

# 附加部分:通过`window.open`引用识别新打开的标签

当我们从 oTab 打开一个链接时，我们最有可能使用的是`window.open`方法。因此，我们可以将该引用与接收到的`event`源进行比较，并识别新打开的标签。现在，我们的接收器代码看起来像这样:

```
document.getElementsByClassName('goto-nTab').onclick = function () {
        const ref = window.open('http://random.com');
    }
```

现在我们可以比较`ref`和`event.source`来识别它是 nTab。这里:

```
const winRef = window.opener;
const counter = 0;
let ref = null;document.getElementsByClassName('goto-nTab').onclick = function () {
        ref = window.open('http://random.com');
    }setInterval(function() {
  window.addEventListener("message", (event) => {
      if (ref == event.source && event.data.isActive) {
         counter = 0;
   } else {
      couter++;
     }   
}, false);
  }, 60000);XMLHttpRequest.prototype.send = function() { 
   counter = 0;
}
```

您还可以进一步探索`window`对象，深入了解并展示它所包含的内容(使用调试器帮助！).

感谢阅读！如果你有任何问题/建议，请写在评论里。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***