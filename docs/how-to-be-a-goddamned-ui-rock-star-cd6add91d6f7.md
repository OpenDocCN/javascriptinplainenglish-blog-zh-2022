# 如何成为一个该死的 UI 摇滚明星

> 原文：<https://javascript.plainenglish.io/how-to-be-a-goddamned-ui-rock-star-cd6add91d6f7?source=collection_archive---------12----------------------->

## 高级 JavaScript 用户界面/UX

## 使用这个 JavaScript 库可以轻松、优雅地制作基本 DOM 变化的动画。

![](img/0b4e35ac98118550a818118efbf24d8e.png)

Image by EdZbarzhyvetsky via DepositPhotos

早在我成为迪士尼的软件工程师之前，我就在编写代码，对 DOM 进行基本的修改，使之成为一个更加优雅和程序员友好的过程。即使在迪士尼的工作室，你也会遇到工程师，他们把 UI 当成编程的私生子。

显示或隐藏内容通常只是用`display: none;`添加或删除一个`.hide`类，这时 BOM 会重新绘制 DOM，突然将内容显示在页面上或页面外，就像尼安德特人的 UX 一样。

这些开发人员宁愿花几个小时编写带有十几个连接的 SQL 查询或建立 API 端点，也不愿尝试简单的 UI 更改来“完美地”插入内容。

但是，没有创建一个流畅的 UX 的借口总是相同的:“它需要太长时间，”或者“它足够好了”，或者“它只需要功能性的，”或者我不太喜欢的借口:“它只会被工作人员中的少数人使用。”我想揍扁有这种想法的 UI 工程师。好像工作人员是*而不是*人类？我们是否需要构建一个“垃圾”UI，因为员工是“垃圾”用户？

我没有得到心态。"我们为该死的迪斯尼工作，伙计们！"我会提醒他们。“我们是精英中的精英！我们应该建造神奇的东西！”他们会看着我，好像它长了第二个头。哦，好吧。

如果你属于我的一些开发伙伴的阵营，他们讨厌花几个小时用精美的 DOM 动画编写优雅的 UI/UX，那就不要再烦恼了！

我将 TigerDOM 作为我个人的首选 JavaScript 库，它轻松、优雅地消除了进行基本 DOM 更新的痛苦，并使您在这个过程中看起来像一个该死的摇滚明星！

# **为什么要使用 DOM 动画？**

简短的回答是:因为人不是机器人。

如果你是一名从事 UI 工作的工程师，我们大多数人都明白我们所构建的不仅仅是计算机与其他计算机的对话；我们还在开发允许计算机与人类交流的软件。作为工程师，我们中的一些人忘记了这一点，或者我们只是不太擅长与人交谈。

人类不是机器；我们有思想和感情，我们与我们使用的机器进行视觉上的“互动”。

不幸的是，作为工程师，我们经常建造“足够好”的东西，意思是“功能性的”，而没有过多考虑使用我们作品的人实际上对我们建造的东西的想法。我们在工程方面很棒——但在设计方面可能没那么好。

我们经常被困在构建 UI 和 UX 上——但我们并不是真正的“设计师”。

没有比 NASA /ESA 和 SpaceX 之间的鲜明对比更好的“工程师不是设计师”范例了。只要看一眼国际空间站的内部，你就会知道它是由工程师设计的。

![](img/47250a8e7187fc23bce2e7d6ea006ab6.png)

Image courtesy NASA

这是 SpaceX 龙太空舱的内部，由真正的设计师设计，然后由工程师实施。

![](img/8149b887b7791757b6f8657335d0d46a.png)

Image courtesy SpaceX

如果让你选择太空交通工具，你会选择哪一种？

我停止我的案子。

这和你如何设计你的用户界面/UX 以及在 DOM 中做改变是一样的。你的用户、产品经理和其他利益相关者更希望你设计的东西看起来和工作起来更像 SpaceX 的图像。

对吗？

所以让我们开始吧！我将通过使用 TigerDOM 的简单而优雅的“设计师”动画，向您展示让您看起来像是为 SpaceX 工作是多么快速和容易。

# tiger DOM——动画制作正确

DOM 动画是 UX 的重要组成部分。而不是对 DOM 进行一些不和谐的改变，只是以用户可能看不到的方式将内容强加到页面上；优雅的 UX 柔和地让用户界面上或界面下的内容生动起来，既能吸引用户的注意力，又不会显得愚蠢或浪费用户的时间。

对于真正优雅的 UI，在 DOM 中显示和隐藏内容应该是一个两步的过程。

首先，您扩展容器；然后淡入内容。移除内容正好相反:首先淡出内容，然后收缩容器。

这个动画的速度需要很快，动画的每一步大约 400 毫秒。这对于大多数人来说已经足够快了，因为 DOM 会随着变化而更新。

这一切都发生在不到一秒钟的时间里。但是最终的动画是一个平滑优雅的 DOM 变化，看起来并不像我说的那样愚蠢或做作。

看看下面的 [**Codepen**](https://codepen.io/webtigers/pen/wvPNyOa) 获得我所说的优雅 UI 变化的全功能页面。*(最好点击上面的链接或“在 Codepen 上编辑”，以便最好地在 Codepen 上查看整个页面的操作。)*

Try out TigerDOM now on Codepen!

您也可以从 [GitHub](https://github.com/WebTigers/tigerDOM) 查看并下载所有代码。`index.html`文件是 Codepen 版本的一个自包含示例，您可以将它放入您的 IDE 以获得“操作”示例。

TigerDOM 非常轻便。缩小版的大小只有 4.9KB，与我们通常为 UI 加载的其他库相比，几乎看不出来。但是它对用户如何与你的页面和内容互动有很大的影响。

# 一行代码中的自动动画

现在让我们看看引擎盖下是什么。

首先，这些不是 CSS 动画——都是 JavaScript。TigerDOM 不需要额外的 CSS 就能工作。虽然一个`.hide {display: none;}`类可能有用。我确实为图标添加了一些 CSS 动画，但那只是我的选择。

TigerDOM 使用起来非常简单和直观。正如我所说的，大多数操作只需要一行代码就可以完成(或多或少)。

## **显示和隐藏**

最简单的操作，如显示(`‘open’`)和隐藏(`‘close’`)内容，可以通过以下方式实现:

```
$('#containerElement').tigerDOM('close');// or$('#containerElement').tigerDOM('open');
```

TigerDOM 淡出容器的内容，然后以用户喜欢的平滑优雅的动画形式折叠容器。现在你看起来很专业！

## 插入和删除内容

TigerDOM 还允许您在一行代码中插入内容:

```
$('#targetContainer').tigerDOM('insert', {content:'<p>Hi!</p>'});
```

删除内容甚至更容易:

```
$('.targetElements').tigerDOM('remove');// Or clear the container$('#targetContainer').tigerDOM('change', {content:''});
```

TigerDOM 在一个平滑的动画中移除元素，在这个过程中自动调整容器元素的高度。

# 高级 TigerDOM 操作

TigerDOM 的主要用途之一是在 Ajax 调用后将引导样式的消息插入页面。

实际上，我更喜欢使用 Bootstrap 的警告，而不是类似于***to str***的消息，因为我可以更好地控制这些消息在哪里出现以及如何消失。

TigerDOM 的核心是一个简单的消息对象，如下所示。请注意可选默认值:

```
*{ 
    content       : string,    // Required
    removeClick   : bool,      // Optional false
    removeTimeout : int,       // Optional 0 = no timeout
    callback      : function   // Optional null
}*
```

以下是将引导警告插入页面消息容器的基本用例:

```
let content = 
'<div class="alert alert-success" role="alert">' +
  'This is a success alert—check it out!' +
'</div>';let callback = function(){ 
    // do stuff
}*let message = { 
    content       : content,
    removeClick   : true,
    removeTimeout : 5000,
    callback      : callback
};*$('#messageContainer').tigerDOM('insert', message);
```

如您所见，一旦我们封送了消息对象的内容和属性，只需一行代码就可以优雅地插入响应消息。内容可以是字符串或 jQuery 元素对象。

如果我们设置了一个`removeClick`，那么当用户点击它的时候，这个消息可以被很好的处理掉。

如果我们设置了一个`removeTimeout`，那么消息将在分配的毫秒数到期后自动消失。

TigerDOM 消息还有一个`callback`属性，可以用可选的回调函数来设置。一旦动画完成，这个函数就会被调用。这给了你一种`completed`事件挂钩，一旦动作完成，你就可以做一些事情。

# 其他公用事业

除了常见的显示动画，TigerDOM 还包括一些其他的细节，比如:

*   **equal heights**—这允许您用一行代码使两个或更多的列容器高度相等。
*   **animate count**—这允许你动画显示数字的递增或递减，非常类似于 Intuit 在他们的 TurboTax 产品中所做的。

# 奖励—专业提示

这里是最后一个摇滚明星提示，你可以用来进一步提高你的 UX:悬停状态转换。这简单的一行 CSS 将把你所有的链接和按钮悬停变成平滑的状态转换，而不仅仅是不和谐的颜色变化:

```
a, button, .btn { transition: 0.8s; }
```

我其实更喜欢长一点的颜色过渡，但这只是我的看法。Bootstrap 的典型悬停状态非常微妙，但转换按钮或链接的颜色是一种很好的方式，可以在 TigerDOM 的优雅的同时为您的 UI 增加一点档次。

# 结论

优雅的用户界面/UX 不必费时、复杂或凌乱。

使用 TigerDOM，您可以轻松地制作简单的 DOM 操作动画，并使您的应用程序的 UI/UX 在前端看起来和在后端一样好。现在你是 UI 摇滚明星了！

____________________

Beau Beauchamp 是一名 web 应用程序架构师，拥有 20 多年在云中开发企业级应用程序的经验；他是[*WebTigers*](https://webtigers.com)*的创始人，也是老虎平台背后的首席开发者。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于**[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。****