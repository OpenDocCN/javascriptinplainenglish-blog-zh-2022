# 您应该知道的 6 个非常棒的 JavaScript DOM 技巧和窍门

> 原文：<https://javascript.plainenglish.io/6-awesome-javascript-dom-tips-and-tricks-you-should-know-d784ef3a5232?source=collection_archive---------0----------------------->

## 作为开发人员，您需要了解的强大的 JavaScript DOM 技巧和提示。

![](img/6fa5a8eba203957d42c6d3dcbb7ac523.png)

Photo by [Stillness InMotion](https://unsplash.com/@stillnes_in_motion?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

DOM 或所谓的*文档对象模型*是一个非常常见的编程接口，它允许我们处理 web 文档并使它们动态化。

它定义一个页面，以便程序可以更新文档的结构、样式和内容。

文档由 DOM 表示为节点和对象，允许编程语言与之交互。在 JavaScript 中，DOM 不是语言的一部分。所以你可以把 DOM 想象成一个 web API，它允许你创建交互式的动态网站。

当然，作为一名 web 开发人员，您只会使用 JavaScript 来操作 DOM。但是，请记住，如果您愿意，也可以为任何其他编程语言构建 DOM 的实现。

就一般的 web 开发而言，JavaScript DOM 非常强大。我们可以使用许多有用的 DOM 方法和属性。你可以用它完成很多事情。

这就是为什么在本文中，我们将向您展示一些作为 web 开发人员需要了解的非常棒的 JavaScript DOM 技巧和诀窍。所以让我们开始吧。

# 1.一个事件只触发一次

在 JavaScript DOM 中，您可以选择只触发一次事件。这意味着你可以允许一个事件在一个特定的元素上只被触发**一次**。

为此，只需将对象`**{ once: true }**` 添加到您的事件侦听器中。

下面是一个代码示例:

```
const elem = document.querySelector('button');elem.addEventListener("click", ()=> {
 console.log("Hello world");
}, **{ once: true }**);
```

因此，在上面的代码示例中，当用户单击按钮元素时，字符串`"hello world"`只会在控制台中打印一次**。它不会被多次打印。只会在第一次点击的时候。**

**这是防止用户多次执行一个动作的好方法。所以现在只需添加`{ once: true }`，你就可以实现与方法`removeEventListener`相同的事情。**

# **2.检测目标元素外部的点击**

**有时在 JavaScript 中使用 DOM 时，您需要检测元素或 div 外部的点击，以便您可以基于此执行操作。**

**我们可以通过使用方法`contains()`和属性`target`在 JavaScript 中实现这一点。这将允许我们检测用户是在目标元素的外部还是内部单击。**

**看看下面的代码示例:**

```
const elem = document.querySelector('div');elem.addEventListener('click', (**e**) => {
 const outsideClick = **!elem.contains(e.target)**;

 console.log(**outsideClick**); *//returns true or fasle*
});
```

**所以返回值是一个布尔值(真或假),由此我们可以知道是在一个元素的外部还是内部点击了鼠标。因此，我们可以使用它来更新我们的应用程序，并根据布尔值执行我们想要的操作。**

# **3.获取计算的样式**

**为了方便地访问和获取给定元素的所有样式及其值，我们可以使用方法`getComputedStyle()`来实现。**

**看看下面的代码示例:**

```
const elem = document.querySelector('h2');
const cssObj = window.**getComputedStyle**(elem, null);
*//returns a CSS object*//get a css value of the element from the object
h2Color = cssObj.**getPropertyValue**('color');
console.log(h2Color); *//returns rgb(0, 0, 0).*
```

**如您所见，您还可以使用方法`getPropertyValue()`来获取元素的特定样式值。**

# **4.查找用户单击的元素**

**在 HTML 代码中的许多情况下，您可能有多个类型相同的元素。例如，您可能有许多按钮元素，并且您想知道用户单击了哪一个。**

**为了知道用户点击了哪个按钮，您需要选择所有的按钮，然后为每个按钮添加一个点击事件。之后，您只需要使用方法`**closest()**`并将元素的类型作为参数传递，以便它返回被单击的元素。**

**下面是一个代码示例，您可以查看一下:**

```
<!DOCTYPE html>
<html>
<body><button class="btn1">First button</button>
<button class="btn2">Second button</button><script>document.querySelectorAll("button").forEach(el => {
 el.addEventListener("click", ()=>{
  console.log(**el.closest("button")**);
 })
});
</script></body>
</html>
```

**现在，每当您单击一个按钮元素时，它都会被打印到控制台中，并带有自己的类和文本内容。结果，你会知道哪个被点击了。**

***注意:您也可以将一个类或一个 ID 作为参数传递给最近的方法()。这将允许你检测更多的特定元素。***

# **5.克隆一个 DOM 元素**

**通过使用方法`cloneNode()`，您可以克隆任何想要的 DOM 节点。该方法采用一个参数(布尔值)，如果您将其设置为 true，它将创建 DOM 节点及其所有子元素的深层副本。**

**下面是代码示例:**

```
<!DOCTYPE html>
<html>
<body><div class="container">
  <button class="btn1">First button</button>
  <button class="btn2">Second button</button>
</div><script>const elem = document.querySelector(".container");**const clone = elem.cloneNode(true);****console.log(clone.outerHTML);** */*
returns
<div class="container">
  <button class="btn1">First button</button>
  <button class="btn2">Second button</button>
</div>
*/*</script></body>
</html>
```

**正如你所看到的，我们还使用了属性`outerHTML`，这样我们就可以在控制台中打印 HTML 元素。**

# **6.将元素滚动到视图中**

**您可以使用方法`scrollIntoView()`让浏览器滚动到给定的元素。**

**您需要将该方法应用于给定的元素，然后给它一个对象作为参数。该对象包含两个属性:**

*   **block 属性:滚动到视图后最后一次滚动的位置*(开始、中心、结束、最近)*。**
*   **行为:过渡的滚动行为*(平滑，自动)*。**

**下面是一个代码示例:**

```
const btn = document.querySelector("button");
const elem = document.querySelector(".container");btn.addEventListener('click', ()=>{
 elem.**scrollIntoView({behavior: "smooth", block: "center"}**);
});
```

# **结论**

**正如你在上面看到的，这些是一些有用的 JavaScript DOM 提示和技巧，你可以作为一个 web 开发人员使用。所以在 JavaScript 中你可以用 DOM 做很多事情，它在 web 开发中非常强大。你只需要多练习，这样你就能掌握它的窍门了。**

***感谢您阅读本文。此外，如果您发现我的内容有用，而您不是媒体会员，您可以在这里获得您的媒体会员资格*[](https://mehdiouss.medium.com/membership)**(媒体推荐链接)以无限制地访问所有内容并支持我们作为作家。****

***[](https://mehdiouss.medium.com/membership) [## 通过我的推荐链接加入 Medium-Mehdi Aoussiad

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mehdiouss.medium.com](https://mehdiouss.medium.com/membership) 

**更多阅读:**

[](/9-awesome-css-games-that-you-should-play-in-2022-6809ca8df058) [## 2022 年你应该玩的 9 款超棒的 CSS 游戏

### 神奇的游戏，帮助开发者轻松学习 CSS。

javascript.plainenglish.io](/9-awesome-css-games-that-you-should-play-in-2022-6809ca8df058) [](/9-useful-front-end-web-developer-cheatsheets-to-save-time-2e1fe7495e8) [## 9 个有用的前端 Web 开发人员备忘单来节省时间

### 2022 年每个 web 开发人员都应该知道的惊人的备忘单。

javascript.plainenglish.io](/9-useful-front-end-web-developer-cheatsheets-to-save-time-2e1fe7495e8) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。******