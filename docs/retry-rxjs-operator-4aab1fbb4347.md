# 如何使用 RxJS“重试”运算符处理错误

> 原文：<https://javascript.plainenglish.io/retry-rxjs-operator-4aab1fbb4347?source=collection_archive---------7----------------------->

## 关于如何使用 RxJS“重试”操作符处理错误的简短指南。

![](img/20562838a616ca43eae79e2cae0d225a.png)

有几种方法可以处理可观测量的错误。可以使用运算符，如`catchError`、`retry`或`retryWhen`。今天我只关注`retry`和它的一种简单使用方式。

![](img/ce471a0245b06a222fe75ac8978d6819.png)

`retry`是一个 RxJS 运算符，可用于处理由可观察值生成的错误。正如名副其实的算子所暗示的那样，在一个可观测值被认为是错误的可观测值之前，它会尝试重放该可观测值指定的次数。

在上面的例子中，如果出现错误，可观察对象将至少进行三次以上的尝试。

`retry`操作符也可以接受两次尝试之间的延迟，以便在应用程序调用服务器之前留出时间。

该延迟可以逐渐使用，即增加每次重试尝试后所花费的时间。

![](img/3cd14da6b4866e75cbd172df46462889.png)

这个题目到此为止。感谢您的阅读。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*