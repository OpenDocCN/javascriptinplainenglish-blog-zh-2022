# 停止在 Angular 中单击和双击之间的可怕冲突

> 原文：<https://javascript.plainenglish.io/stop-the-horrible-clash-between-single-and-double-clicks-in-angular-5798ce90fd1a?source=collection_archive---------3----------------------->

## 关于如何使用 RxJS 主题解决事件冒泡的指南。

![](img/da8a94819110bdfd4fccb718116c525b.png)

Photo by [Drew Hays](https://unsplash.com/@drew_hays?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你曾经希望你的应用程序在单击和双击时有不同的表现吗？听起来很容易实现，对吗？不对！

问题是，浏览器将双击解释为两次单击，导致两个 ***事件处理程序都触发，导致流血和破坏😭***

我们可以通过使用 [RxJS Subjects](https://rxjs.dev/guide/subject) 的能力和使用人体工程学指令防止事件冒泡来巧妙地解决这个问题:

## 解释:

*   我们已经将点击处理策略转移到一个指令中，这样我们就可以在 Angular 模板中的任何 DOM 节点上轻松地重用它
*   我们已经声明了一个`Subject`来保存我们的点击事件流
*   通过使用指令`[HostListener](https://angular.io/api/core/HostListener)`绑定到这两个事件，我们防止了这些事件的冒泡和默认行为，并将事件注入到我们的点击主题中
*   问题是`click`和`dblclick`事件都向上冒泡，所以双击时，单击处理程序将触发两次，然后双击处理程序将触发一次。我们需要停止这种冒泡！
*   [浏览器规格](https://w3c.github.io/uievents/#:~:text=This%20event%20type%20MUST%20be%20dispatched%20after%20the%20event%20type%20click%20if%20a%20click%20and%20double%20click%20occur%20simultaneously%2C)保证了`dblclick`事件总是在`click`事件之后 ***发生的顺序。因此，通过使用`debounceTime`操作符，我们可以控制双击的“速度”。这将帮助我们区分`click`和`dblclick`事件。在去抖窗口之后，如果 clicks 主体发出的值不是双击，那么肯定是单击。***
*   该指令的“选择器”也匹配输出事件名称。这使得我们的使用 API 符合人体工程学，简洁明了，如下所示:

我们结束了🎉🎉🎉

希望你觉得这有用

快乐工程！

***如需更多此类文章更新请订阅*** [***我的免费简讯***](https://www.bytelimes.com/#/portal/signup/free) ***。***

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*