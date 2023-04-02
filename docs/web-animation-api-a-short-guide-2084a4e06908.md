# 网络动画 API:简短指南

> 原文：<https://javascript.plainenglish.io/web-animation-api-a-short-guide-2084a4e06908?source=collection_archive---------15----------------------->

## 让我们在 web 应用程序页面上制作动画

![](img/90a05f254f9dc68258654d9b19630688.png)

Photo by [Noah Boyer](https://unsplash.com/@emerald_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

动画是改善网络用户体验的一个很好的工具。除了提供视觉上吸引人的体验，动画还可以帮助用户理解组件在网站上是如何出现、移动和消失的。

为了处理动画元素， [Web 动画 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API) 提供了丰富的方法和类。基本功能在浏览器中已经存在很长时间了，但是某些新功能只在最新的浏览器中可用。

[网络动画 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API) 允许你同步和定时改变网页的外观，比如 DOM 元素动画。它通过集成两个模型来实现这一点:T4 计时模型和动画模型。

[Web 动画 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API) 不仅允许您制作项目动画，还允许您查看应用到项目的动画，动态更改动画，等等。

如果您希望动态地动画显示像通知或祝酒词这样的对象，单独使用 CSS 可能不够，这将非常有用。

下面的示例显示了如何将从 DOM 查询的元素制作成动画。这相当于我们如何使用 CSS 关键帧来激活这些元素。

```
<button class="item">HELLO</button>
<style>
  .item {
    background: #3a55d2;
    border: none;
    padding: 0.8rem 0.7rem;
    border-radius: 5px;
    color: #fff;
    font-size: 1rem;
  }
</style>
<script>
  const item = document.querySelector('.item'); item.animate([
    { transform: 'translateX(0px)' },
    { transform: 'translateX(100px)' },
  ], {
    duration: 2000,
    easing: 'ease-in-out',
    direction: 'alternate',
    iterations: Infinity
  });
</script>
```

![](img/cf9aa53f727f82b2536928b2160034e9.png)

Output

Web Animations API 为浏览器和开发人员提供了一种通用语言来描述 DOM 元素上的动画。要获得关于 API 背后的概念以及如何使用它的更多信息，请阅读[使用 Web 动画 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API) 。

*本文到此为止。我希望你今天学到了一些新东西。您可以在* [*上*](https://gouravkajal.medium.com/membership) [*关注我*](https://gouravkajal.medium.com/) *或者在*[*LinkedIn*](https://www.linkedin.com/in/gouravkajal/)*上与我联系。想看更多这样的文章，敬请期待！*

*感谢阅读！*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*