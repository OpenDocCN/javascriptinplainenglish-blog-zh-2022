# 高级 HTTP 方法:PUT 和 PATCH 请求之间的区别

> 原文：<https://javascript.plainenglish.io/advanced-http-methods-difference-between-put-and-patch-request-5232bdb0e70b?source=collection_archive---------5----------------------->

## 深入了解上传和补丁请求。

![](img/62868c8da532e7884423b4cfc818d0ec.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

开发人员或程序员应该知道`PUT`和`PATCH`请求之间的区别。似乎两者都在修改资源中的数据。就这些吗？或者这个问题在面试的时候问你，你现在会怎么回答？

今天我们就来聊聊这个话题。让我们开始吧。

```
1\. [Safe and Idempotent HTTP Methods](#a08f)
2\. [PUT Request](#d9bc)
3\. [Why is PUT Request Idempotent](#7ed4)
4\. [PATCH Request](#fe0c)
5\. [Why is PATCH Request Non-Idempotent](#368d)
6\. [When To Use PUT and PATCH Requests](#e7fc)
7\. [Differences Between PUT and PATCH Requests](#99e6)
```

# 1.安全和幂等的 HTTP 方法

## **安全方法**

在 REST APIs 的上下文中，安全方法是不修改资源的 HTTP 方法。例如，在`Request URI`上使用 GET 或 HEAD 永远不应该改变资源。安全方法是可以缓存和预取的方法，对资源没有任何影响。

在实践中，通常不可能实现不改变任何资源的安全方法。例如，GET 请求可能会创建日志或更新统计值，或者触发服务器上的缓存刷新。

不可能确保服务器不会因为执行 GET 请求而产生副作用。这里重要的区别是 API 消费者没有要求副作用，因此消费者不能对它们负责。

> 请求 URI 是请求所应用的资源的统一资源标识符。

## 幂等方法

如果一个或多个 HTTP 方法的调用对资源有相同的预期效果，这个方法被认为是`idempotent`。如果该方法只被调用了一次或三次，应该没有关系。资源上的结果应该总是相同的。

`Idempotency`本质上意味着一个成功执行的请求的结果与它被执行了多少次无关。

> 注意:当您发送多个删除请求时，第一个请求删除资源，响应是 200 (OK)或 204(无内容)。下一个请求返回 404(未找到)。响应不同于第一个请求，但是服务器端的任何资源的状态都没有改变，因为原始资源已经被删除了。所以 DELETE 是幂等的。

```
╔══════════════╦════════════════════╦═══════════════╗
║ HTTP Methods ║     Idempotent     ║     Safe      ║
╠══════════════╬════════════════════╬═══════════════╣
║ GET          ║        YES         ║     YES       ║
║ HEAD         ║        YES         ║     YES       ║
║ OPTIONS      ║        YES         ║     YES       ║
║ TRACE        ║        YES         ║     YES       ║
║ PUT          ║        YES         ║     NO        ║
║ DELETE       ║        YES         ║     NO        ║
║ POST         ║        NO          ║     NO        ║
║ PATCH        ║        NO          ║     NO        ║
╚══════════════╩════════════════════╩═══════════════╝
```

# 2.上传请求

`PUT`方法完全修改现有的资源或者创建一个新的资源。它是怎么做到的？

*   API 消费者发送资源 ID
*   如果资源存在，整个资源将被整个实体替换
*   如果该资源不存在，则会创建一个新资源

例如，当您想要更改数据库中用户的名字时，您需要在发出`PUT`请求时发送整个实体。

```
PUT /users/{user-id}

{"first": "John", "last": "Wick"}
```

要发出一个`PUT`请求，你需要发送所有的参数，而不仅仅是名称；本例中的名字和姓氏。

一个成功的`PUT`请求返回一个`200 (OK)`的`HTTP Status Code`或者一个`204 (No Content)`的`HTTP Status Code`，如果它更新成功，并且如果预期的资源还没有一个当前的表示并且`PUT`请求创建了一个，源服务器必须发送一个`201 (Created)`的`HTTP Status Code`响应给 API 消费者。

# 3.为什么 PUT 请求是幂等的

这里的`PUT`请求包含了这个用户的所有参数。

当使用`PUT`请求时，假设您正在发送完整的实体，并且完整的实体在`Request URI`替换任何现有的资源。`PUT`请求通过替换整个资源来处理它。

由于`PUT`请求包括整个实体，如果您重复发出相同的请求，它应该总是有相同的结果(您发送的数据现在是资源的整个数据)。

如果您发送一个`PUT`请求 5 次，第一个请求将更新资源；其他 4 个请求只会一次又一次地覆盖相同的资源状态——实际上不会改变任何东西。

因此`PUT`请求是等幂的。

> 如果你有任何问题，请在评论中告诉我。

# 4.补丁请求

`PATCH`方法对现有资源进行部分更新。这意味着您只需要发送您想要更新的数据，它不会影响或更改任何其他内容。因此，如果要更新数据库中的名字，只需发送第一个参数。对于上面的例子，这个参数是名字。

```
PATCH /users/{user-id}

{"first": "John"}
```

*   API 消费者发送资源 ID
*   如果资源存在，现有资源将被部分更新(并非所有实体都是必需的)。
*   如果资源不存在，则返回`404 (Not Found)`的`HTTP Status Code`

如果更新成功，成功的`PATCH`请求返回`200 (OK)`的`HTTP Status Code`或`204 (No Content)`的`HTTP Status Code`。

# 5.为什么补丁请求不是幂等的

方法更新一小部分资源。例如，如果您使用`PUT`请求更新一个资源，并且没有设置所有的域，那么您就有丢失空白域中的数据的风险。`PATCH` request 解决了这个问题，因为它只更新请求正文中指定的特定部分。

`PATCH`要求并不总是保证同样的效果，所以不是`idempotent`。换句话说，它会影响`Request URI`不同部分的变化。

```
PATCH /users/{user-id}

{"first": "John"}
```

在上面的示例中，只需更改用户资源的名字字段。然后向同一个`Request URI`发出请求，修改同一个资源的不同字段。

```
PATCH /users/{user-id}

{"last": "Doe"}
```

在前面的两个示例中，第一个请求中修改了名字字段，第二个请求中修改了姓氏字段。因此，对同一个资源发出了两个请求，但每个请求得到了不同的结果。

对`PATCH`方法的这一更改根据您正在更新的资源部分给出了不同的结果。因此，`PATCH`不是幂等的。

> 高级注意:`*PATCH*` 请求可以通过使用`*ETag*`和`*If-Modified-Since*` HTTP 头进行幂等处理。

# 6.何时使用上传和修补请求

当 API 消费者需要完全替换现有资源时，消费者可以使用`PUT`方法。当消费者想要进行部分更新时，他们可以使用`PATCH`方法。

例如，当更新资源的单个字段时，发送整个实体表示可能会很麻烦，并且会使用大量不必要的带宽。在这种情况下，使用`PATCH`方法更有意义。

# 7.上传和修补请求之间的差异

`PUT`和`PATCH`请求的主要区别在于，服务器处理发送的实体来更新由`Request URI`标识的资源。当发出一个`PUT`请求时，发送的实体被视为保存在原始服务器上的资源的修改版本，API 消费者请求对其进行更改。然而，与`PATCH`请求一起发送的实体有一组指令，描述了存储在原始服务器上的资源必须如何被部分修改以创建新版本。

这里要考虑的另一个重要方面是幂等性。`PUT`方法是幂等的，而`PATCH`方法可以是幂等的，但不是必须的。您可以根据它的实现位置选择其中之一。

```
╔════════════════════╦════════════════════╦═══════════════╗
║                    ║        PUT         ║     PATCH     ║
╠════════════════════╬════════════════════╬═══════════════╣
║ Partial Updates    ║        NO          ║     YES       ║
║ Bandwidth          ║        HIGH        ║     LOW       ║
║ Create a Resource  ║        YES         ║     NO        ║
║ Idempotent         ║        YES         ║     NO        ║
║ Safe               ║        NO          ║     NO        ║
╚════════════════════╩════════════════════╩═══════════════╝
```

# 结论

希望你能从这篇文章中得到一些推论！总结一下本文，这些方法之间的主要区别在于幂等性以及它们如何处理来自 API 消费者的请求。面试的时候可能会问到这个问题。

> 如果你喜欢这样的故事，想支持我，请考虑成为[中的会员](https://chntrks.medium.com/membership)，点击拍手👏按钮，以示支持。👇你的支持对我写下一个故事非常重要——谢谢。

![](img/b8305e339c064263f6a7f0eabef7292a.png)

```
Want to Connect?

[LinkedIn](https://www.linkedin.com/in/chntrks/) - [Twitter](https://twitter.com/chntrkss) - [Github](https://github.com/chntrkss) - [Coffee](https://www.buymeacoffee.com/chntrkss)
```

[](https://betterprogramming.pub/advanced-react-hooks-everything-about-the-useeffect-9f065d05f8b7) [## 高级反应钩子:关于使用效果的一切

### 使用这些提示和技巧，让您的 React 代码更加专业和不可思议

better 编程. pub](https://betterprogramming.pub/advanced-react-hooks-everything-about-the-useeffect-9f065d05f8b7) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*