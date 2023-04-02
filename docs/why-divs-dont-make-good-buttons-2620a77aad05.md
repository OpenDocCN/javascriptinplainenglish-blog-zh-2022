# 为什么 div 做不好纽扣

> 原文：<https://javascript.plainenglish.io/why-divs-dont-make-good-buttons-2620a77aad05?source=collection_archive---------7----------------------->

![](img/134ca83bec0a9788ddd06f5404da0076.png)

[Photo by Andrea Piacquadio](https://www.pexels.com/photo/portrait-photo-of-woman-in-red-top-wearing-black-framed-eyeglasses-holding-out-her-hand-in-stop-gesture-3762802/)

在网络上，按钮无处不在。它们允许我们与网络内容互动。它们有助于给我们一种动态体验。因为按钮是网络的核心，所以我们必须把它们做好。

许多开发者抱怨不同浏览器的按钮风格不同。使用这些默认值是一件令人头疼的事情。

所以创建按钮时最常见的反模式是使用`div`标签，然后通过 javascript 使其可点击。

假设您创建了一个 div 并添加了`onclick`方法使其可点击。

```
<div onclick="doSomething();">
    Click me!
</div>
```

按钮工作正常吗？你可以点击它，那么问题在哪里？

# 焦点

并不是每个访问你网站的人都使用鼠标导航。许多用户将改为使用键盘导航。

例如，可能有一个有缺陷的用户限制他使用鼠标，或者用户只是用他用来操作鼠标的手吃饭。

键盘导航最重要的方面是***焦点*** ，它表示当前活动的元素，可以用键盘按键操作。

所以现在你看到这显然是一个问题。如果用户够不到按钮，他们将如何与它交互？

幸运的是，有一个简单的解决方法。您可以在 div 上添加属性`tabindex="0"`。

```
<div tabindex="0" onclick="doSomething();">
    Click me!
</div>
```

我们为什么用“0”呢？`tabindex`接受三种类型的输入—

*   **0:** 元素根据 DOM 顺序获得焦点。
*   **负值:**该元素不能通过连续的键盘导航来访问，但是可以通过 JavaScript 或用鼠标点击来聚焦。这不能解决我们的问题。
*   **正值:**元素获得焦点，其顺序由数值定义。例如，`tabindex="4"`在`tabindex="5"`之前聚焦。这使得很难浏览页面。

所以现在我们已经解决了焦点问题，我们一定要好好的。

但是等等，仍然有一个问题:键盘用户可以够到按钮，但是实际上不能用任何键按下它。

# 键

我们的`onclick`方法只适用于鼠标点击和移动点击。通过键盘导航的用户会期望通过`space`或`enter`键按下键盘。

这意味着，我们的 div 也需要处理按键事件。

```
const ENTER = 13;
const SPACE = 32;
// Select for your button and store it in `myButton`
myButton.addEventListener('keydown', function(event) {
    if (event.keyCode === ENTER || event.keyCode === SPACE) {
        event.preventDefault(); // Prevents unintentional form submissions, page scrollings, the like
        doSomething(event);
    }
});
```

啊，开始了。现在，我们可以使用鼠标和键盘与按钮进行交互。

等等，还有一个问题。辅助技术不会将`div`视为按钮。

# 作用

目前，我们的按钮没有向辅助技术提供任何它是按钮的指示。所以屏幕阅读器错过了两个重要的东西，它们可以通过一个按钮得到。

首先，每当屏幕阅读器通过一个按钮时，它会宣布它是一个按钮。例如，当用户关注我们的按钮时，他们会听到*“点击我”*，而当他们关注一个真正的按钮时，他们会听到*“按钮点击我”*。

其次，您还可以为屏幕阅读器启用其他类型的导航。对于屏幕阅读器来说，从一个标题跳到另一个标题、从一个按钮跳到另一个按钮是很常见的。这是导航页面的有效方式。但是，只有当屏幕阅读器知道页面上的每个元素应该表示什么时，这才是可能的。

幸运的是，有一种方法可以解决这个问题。你只需要将`role="button”`添加到我们的 div 中。

```
<div tabindex="0" role="button" onclick="doSomething();">
    Click me!
</div>
```

# 状态

按钮很少孤立存在。它们通常存在于表单的上下文中。并且它们可能被一些复杂的形式逻辑所约束。例如，应该根据某些输入验证来启用或禁用按钮。

为了在我们可点击的`div`中实现这一点，我们必须通过编程来切换`onclick`和`tabindex`。当然，这是可以做到的，但是这会给你带来很多麻烦。

在这一点上，我们已经投入了大量的时间来使我们的 div 表现得像一个按钮。

如果我们使用`<button>`元素，我们可以摆脱这一切，它给了我们所有现成的东西。

让我们来解决按钮在不同浏览器中有不同风格的问题。处理这些违约让人感觉很痛苦。

你可以使用这个[优秀的按钮重置](https://archive.hankchizljaw.com/wrote/introducing-the-button-element/)，它让我们的`button`看起来像只有 11 行代码的`div`。从那里你可以随心所欲地设计它。

# 包扎

今天，您了解到用户希望他们的按钮具有以下功能-

*   它应该可以用鼠标点击，在手机上点击。
*   它应该是可聚焦的。
*   应使用`enter`或`space`键触发。
*   它应该可以被辅助技术识别。
*   它应该能够处理不同的状态，如禁用。

您可以通过使用`button`元素免费获得所有这些。希望这篇文章已经说服你在你的应用程序和网站的按钮中使用`<button>`元素而不是`<div>`元素。

你还有什么问题吗？如果你愿意，请在下面留下你的评论，我会尽快回复你。

***如果你喜欢这个，请看看我的其他作品***[](https://tahajiru.start.page/)****。****

**报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***