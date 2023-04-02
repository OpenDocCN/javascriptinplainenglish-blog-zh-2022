# 提高网页可访问性的 5 个简单技巧

> 原文：<https://javascript.plainenglish.io/5-easy-tips-to-improve-web-accessibility-74221d40f19a?source=collection_archive---------10----------------------->

## 让我们努力使我们的网络应用程序对有特殊能力的用户来说是可访问的

![](img/2e5c37d444ce0f27566fcdf2691d45d0.png)

Photo by [Ian Parker](https://unsplash.com/@evanescentlight?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们设计或开发一个 web 应用程序时，我们倾向于为所有用户服务。我们考虑或至少尝试考虑不同用户的所有需求。

当一个 web 应用程序被正确地设计和开发时，残疾用户使用我们的 web 应用程序就变得很容易。但不幸的是，大多数时候，我们在 web 开发过程中没有考虑到这一点。

许多网站和产品现在都有可访问性障碍，使得一些人很难或不可能使用它们。

创建网站或在线应用程序时，尽可能使其具有包容性和可访问性是至关重要的。超过 10 亿人患有影响其视觉、运动、听觉、认知、语言或神经功能的障碍。

今天，我们将讨论一些小技巧，我们可以很容易地实现，为每个人提供更容易访问的软件。

## 1.指示当前页面

作为 web 开发人员，我们应该始终确保突出显示当前活动的页面，既要有视觉提示，也要有辅助技术可以识别的提示。

我们可以通过在应用程序的活动导航项目上设置`aria-current=”page”`来实现。

```
<a aria-current="page" href="/">Home</a>
```

即使我们想要样式化当前活动的导航项目，我们现在也可以使用这个 CSS 选择器:

```
[aria-current="page"] {
    /* Active element style */
}
```

要了解更多关于`aria-current`的信息，请访问此处:

[](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-current) [## aria-当前-可访问性| MDN

### 元素上的非空 aria-current 状态表示该元素表示容器中的当前项…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-current) 

## 2.指定文档语言

虽然有些人可以简单地阅读网页内容来确定语言，但并不是所有人都有能力这样做，所以我们应该在 web 文档中指定语言。

首先，确保使用`<html>`标签上的`lang`属性指定语言。

```
<html lang="en-US">
```

如果我们的网站支持或使用多种语言，我们可以在特定的目标上使用`lang`和`hreflang`属性。

```
<a lang="en" hreflang="en" href="/projects" title="Projects">
    Projects
</a>
```

要了解更多关于`lang`的信息，请访问此处:

[](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang) [## 语言- HTML:超文本标记语言

### lang 全局属性有助于定义元素的语言:编写不可编辑元素的语言…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang) 

要了解更多关于 HTML 中的`hreflang`属性，请访问此处:

[](https://www.w3schools.com/tags/att_a_hreflang.asp) [## HTML hreflang 属性

### hreflang 属性指定链接中文档的语言:亲自尝试

www.w3schools.com](https://www.w3schools.com/tags/att_a_hreflang.asp) 

## 3.处理运动首选项

有些人可能对运动很敏感，可能会被我们添加到网站上的过渡或动画所干扰。以下是我们可以提供的帮助！

我们可以使用 CSS `prefers-reduced-motion`媒体查询来改变你的内容风格和停止动画。

```
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms;
        animation-iteration-count: 1;
        transition-duration: 0.01ms;
        scroll-behavior: auto;
    }
}
```

要了解更多关于`prefers-reduced-motion`的信息，请访问此处:

[](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) [## prefers-reduced-motion - CSS:级联样式表| MDN

### 首选减少运动 CSS 媒体功能用于检测用户是否请求系统最小化…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) 

## 4.向图像添加替代文本

为图片添加有意义的替代文本是我们可以采取的最重要的步骤之一，以使我们的网站更容易访问。这有助于使用屏幕阅读器的用户了解与图像内容相关的信息。

```
// Not Good
<img src="penguin.jpg" alt="my img" /> // Good
<img src="penguin.jpg" alt="A lovely penguin enjoying the sunset" /> 
```

## 5.使您的表单易于访问

残疾人在我们的网站上填写表格应该不会有困难，这就是为什么我们应该通过采取以下措施来尽可能地使他们变得无障碍！

*   使用本机 HTML 表单控件，并始终指定它们的类型。

```
<input type="text">
<input type="checkbox"><button>Submit</button>
```

*   输入应该都与屏幕阅读器的标签相关联。

```
<label for="fullname">Full Name</label>
<input type="text" name="fullname" id="fullname">
```

如果你不想要一个可见标签，你可以使用`aria-label`和`aria-labelledby` HTML 属性来指定一个标签。

*这是它的这篇文章。我希望你今天学到了一些新东西。你可以* [*关注我*](https://gouravkajal.medium.com/) *上* [*中*](https://gouravkajal.medium.com/membership) *或者联系我*[*LinkedIn*](https://www.linkedin.com/in/gouravkajal/)*。想看更多这样的文章，敬请期待！*

*感谢阅读！*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*