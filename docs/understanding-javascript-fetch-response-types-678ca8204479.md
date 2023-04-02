# 了解 JavaScript 获取响应类型

> 原文：<https://javascript.plainenglish.io/understanding-javascript-fetch-response-types-678ca8204479?source=collection_archive---------5----------------------->

## 在这篇文章中，我将带你从一个获取 API 调用中获得不同类型的响应

![](img/881cf136f796b98df78766ff5c9bbf36.png)

Photo by [Jason Strull](https://unsplash.com/@jasonstrull?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/thinking?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在这篇文章中，我将试着引导您从一个 Fetch API 调用中获得不同类型的响应——这取决于您的需求是否需要 JSON、文本、状态等。正如我们所知，每个 API 调用都有一个响应对象，它可以包含不同类型的响应对象，下面是一些最常用的响应类型:

## 1.response.text()

这是当您从服务器获取一行文本时将使用的语法。例如，让我们发送一个包含一些文本的非常简单的响应:

`res.send('Succefully Logged in!')`

要访问此回复，您将使用:

```
const resp = await response.text();
// resp = 'Succefully Logged in!'
// Reads the response body as text
```

## 2.response.json()

这是最常用的响应类型，因为它将从任何后端 API 获得 JSON 响应。让我们假设从服务器我们想要发送用户名作为 JSON 的响应:

```
res.json({ username: 'Jane Doe' })
```

确保在获取 JSON 时预先考虑`await`,因为它将返回一个承诺。要在前端访问它，我们可以使用:

```
const data = await response.json();
//data = { username: 'Jane Doe' }
```

## 3.response.status()

每个响应都有一个 HTTP 状态，这个特定的类型将为您提供该状态，然后根据状态，您可以像下面这样改变您的语句:

```
if(response.status() === 200){
  // Do action on success
} else if (response.status() === 400) {
  // Show failure state with 400
} else {
  // Generic error
}
```

## 4.response.headers()

在某些情况下，您可能需要来自标题的数据，在这些情况下，您可以使用此类型:

```
if(response.headers.get('Content-Type') === 'application/json'){
   // Do something
}
```

从这个语法中，您可以访问响应中出现的各种其他头值。

# 结论

对于 blobs、图像等，您可以获得更多类型的响应。但是本文主要关注那些常用的。我希望你喜欢读它。

我希望这篇文章对你有用。请在评论中让我知道你的想法。考虑成为中级[会员](https://utkarshabakshi.medium.com/membership)，继续阅读我所有的优质文章以及数以千计的其他故事。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*