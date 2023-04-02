# 通过基于项目的学习介绍 Web 开发

> 原文：<https://javascript.plainenglish.io/introduction-to-web-development-through-project-based-learning-f894833917c2?source=collection_archive---------11----------------------->

## 第 1 部分:从基础开始——用 HTML 和 CSS 重新创建网页。

![](img/a3bc7377e8a159e9db8b9cf883dda707.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming-girl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 前言

本文是基于 web 开发项目的学习系列的第一部分。本指南的目标是让您重现我在进入 web 开发，以及现在在云上为客户创建 web 应用程序的经历中走过的旅程。

简单介绍一下我——两年前，我开始了我的网络开发之旅，目标是创建我自己的作品集网站。在大学里呆了 3 年，那时，我觉得我只是在完成我的课程，没有任何实际的东西可以在我的简历上展示。毕竟，不是我的成绩让我找到了工作，而是经历和创建自己的项目所带来的奉献精神。

事情是这样的——除了基本的 HTML、CSS 和 JavaScript(尽管知道 Java 确实有助于这一点),大学没有教我任何与 web 开发相关的东西——所以我几乎是从零开始。一晃 7 个月过去了，我在 SaaS 的一家初创公司获得了一个助理软件工程师的职位，现在我在一家咨询公司工作，从头开始在云上构建 web 应用程序。

虽然有数不清的网络开发课程唾手可得，但我相信它们会剥夺你的批判性思维能力，而这种能力对你未来的成长至关重要。自己做科学实验和把黑板上写的东西抄到笔记本上是有区别的。你更有可能在一年后记住你的科学实验，而不是在一个月后，甚至一个星期后回忆你写了什么。这篇文章是接下来的许多文章中的第一篇，它将引导你踏上基于项目的学习之旅。目标不是为你做工作，而是给你一个手头的任务，并提供你完成它所需的所有资源。还要注意:所有东西都是免费的——包括我们将在本系列的后面建立的 AWS 基础设施！

你可能会问，这篇文章是为谁写的，整个系列将涵盖哪些内容？正如我上面提到的，我一开始没有 web 开发背景，因此，我将在本系列中重新开始这段旅程(额外的好处是现在知道我应该做什么)。这包括但不限于:

*   使用 HTML 和 CSS 重新创建现有网页(本文)
*   了解前端 JavaScript 技巧和窍门
*   使用前端框架(Vue.js)重建网页
*   AWS 简介(这对于许多人来说是一个巨大的入门挑战。我们将慢慢来，只关注我们需要的服务)
*   介绍 CloudFront，将我们的网站推向世界！
*   介绍 NoSQL (DynamoDB)并将其连接到我们的网页上
*   为后端引入 Lambda 和 ApiGateway
*   (可选)CloudFormation 和 Azure DevOps 简介—将您的代码简化到生产中

是的，它看起来开始很容易，难度指数上升，但事实并非如此！所以不要觉得不知所措，慢慢来！一步一个脚印。

所以事不宜迟，我们开始吧！

## 使用 HTML 和 CSS 重新创建现有页面

我一直对网页设计很感兴趣，也很想知道所有的东西是如何作为一种艺术形式结合在一起的——比如排版、字体大小、图像和动画——然而，在无数次尝试设计自己的网页后，所有的东西都崩溃了。你看，当你希望一切都尽善尽美时，你会在项目中投资回报率极低的小部分投入大量精力。几天过去了，你意识到你仍然处于计划阶段，仍然没有开始实际的编码。因此，我发现重新创建一个我欣赏的网页是更好的开始方式，而不是设计一些你还不习惯的不切实际的代码。

我偶然发现了安德鲁·麦卡锡的[作品集网站](https://andrevv.com/)，它融合了创造性的视觉设计和对初学者友好的外观，并以此为模板开始。我使用 Django 重新创建了整个页面，我错误地选择了这个框架来开始我的 web 开发之旅。我的想法是，通过这个项目，尽可能多地学习工具和服务。如上所述，这包括 Django(因此也包括一点 Python)、MongoDB 和 AWS。虽然这似乎不是一个坏主意，但整个过程需要更长的时间来实现，在这段时间里，任何事情都可能发生，包括因缺乏进展而感到气馁，或在工具之间的[兼容性问题](https://jacobsood.medium.com/integrating-mongodb-atlas-with-django-using-djongo-962dfd1513eb)上遇到麻烦。因此，我在整个旅程中学到的是，使用 ***一个*** 新工具/框架/服务，缓慢而稳定地进行，并看到你的努力成果转化为你以前做过的事情。

因此，我认为未来的任务应该是你未来一周的主要关注点。

> 使用普通的 HTML 和 CSS 重新创建安德鲁·麦卡锡的工作页面。没有 JavaScript，没有框架。只是保持它简短，只有 5 件作品。这些单独的工作项目可以是你以前做过的，或者是 lorem ipsum 的图片和/或视频。

***提示:*** 不用担心得到确切的造型。如果页面从远处看都差不多，那就足够好了！

如前所述，本指南适用于基于项目的自学。我不会为你写代码，相反，我已经提供了下面的资源来帮助你完成任务，通过自己阅读这些资源，你将教会自己成为一名优秀的软件工程师/开发人员所必需的重要技能。

## 帮助你完成任务的资源:

**HTML**

以上是我推荐的 HTML 学习的资源。虽然可能有相当多的降价元素，但我建议只学习对这项任务有用的元素。其中包括以下元素:`<a>`、`<head>`、`<h1 to h6>`、`<p>`、`<html>`、`<body>`、`<img>`、`<video>`、`<button>`、`<nav>`、`<header>`、`<footer>`、`<link>`、`<title>`、`<hr>`、`<br>`、`<article>`、`<li>`、`<style>`和`<section>.`请注意，您还应该了解 CSS 开始使用时标签和类是如何工作的！

*   [https://html.com/](https://html.com/)
*   [https://digital.com/tools/html-cheatsheet/](https://digital.com/tools/html-cheatsheet/)

**CSS**

CSS 是这样一种东西，如果你不知道如何按照你想要的方式设计一个东西，其他人可能以前也有过同样的问题，并把它带到网上问它。你通常只需在谷歌上搜索一下就能找到你的答案！下面的链接是为初学者和高级学习者准备的——掌握 CSS 可能需要几年甚至更长时间。为了避免掉进兔子洞，要知道你想学什么。你想知道如何改变字体或增加空白吗？目录应该对你有所帮助。如果你不认为你会需要它们，不要什么都读！

*   [https://www.w3schools.com/css/](https://www.w3schools.com/css/)—伟大的起点
*   [https://www . freecodecamp . org/news/the-CSS-handbook-a-handy-guide-to-CSS-for-developers-b 56695917d 11](https://www.freecodecamp.org/news/the-css-handbook-a-handy-guide-to-css-for-developers-b56695917d11)
*   https://css-tricks.com/——我发现如果你对某件特定的事情感兴趣，这是一个必去之地。比如，你想了解 [flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 的一切

## 总结一下

本文给出的任务应该可以帮助您开始 web 开发；从使用 HTML 和 CSS 创建一个现有页面开始，这避免了知道要创建什么和网站的设计方面的压力。

给自己一周的时间来学习和完成这个练习，并且不要忘记评论你的 GitHub repo 的链接，这样每个人都可以看到你的代码并留下一两条改进的消息！

**想要保持联系？** 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***