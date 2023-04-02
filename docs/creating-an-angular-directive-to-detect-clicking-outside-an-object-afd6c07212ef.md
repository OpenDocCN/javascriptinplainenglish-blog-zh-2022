# 如何创建角度指令来检测对象外部的单击

> 原文：<https://javascript.plainenglish.io/creating-an-angular-directive-to-detect-clicking-outside-an-object-afd6c07212ef?source=collection_archive---------3----------------------->

![](img/37f9e3f8b944d331fb0f7bcf7ed15af6.png)

我经常发现需要一种方法来检测元素外的点击。无论是下拉菜单、模态还是输入，知道用户什么时候试图点击离开是非常重要的。因为它太普遍了，我已经把我处理它的方式标准化成一个指令，通常，只是把这个指令复制粘贴到每个新项目中。

# 问题是

我发现这个指令最常见的用例是创建自定义下拉菜单。在 Angular 中，用`(click)`事件绑定很容易捕获点击事件，所以打开下拉列表很容易。问题是什么时候关闭菜单。没有简单的事件绑定来捕获元素外部的点击事件。

在过去，我尝试过用本地 HTML 和 CSS 来做这些事情，使用一个隐藏的复选框来设置打开和关闭状态。虽然这消除了对 JavaScript 的需求，但除了最基本的下拉菜单之外，对任何东西进行正确的样式设计都是一场噩梦。此外，如果用户单击菜单本身以外的某个地方，该方法仍然不会关闭菜单。

# 解决方案

可行的解决方案的要求非常简单:我们需要一个可以附加到元素上的指令，它可以轻松地检测元素(或其子元素)之外的任何地方的点击事件。以下是该指令的代码以及一些进一步的解释:

The click-outside directive

该指令有一个输出，当它检测到附加元素外部的单击时，将发出一个事件。通过在文档点击时使用`HostListener`，它调用`onClick`函数。该函数只是检查所单击的目标是否包含在附加元素的子元素中。如果没有，它将发出事件。这就是事情的全部。使用该指令可能如下所示:

```
<div class="dropdown" (click)="dropdownOpen = !dropdownOpen" (clickOutside)="dropdownOpen = false">
...
</div>
```

## 警告:

过多地使用这个指令会导致速度变慢。因为每次点击，不管它在页面的哪个位置，都会调用`onClick`函数，如果指令出现在非常多的元素上，函数调用就会增加。此外，将`onClick`函数修改得更复杂，可以放大这种效果。

我希望你觉得这个指令有用。感谢阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*