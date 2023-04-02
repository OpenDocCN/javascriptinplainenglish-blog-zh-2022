# 如何在 Gatsby 上的代码片段中添加复制按钮

> 原文：<https://javascript.plainenglish.io/adding-a-copy-button-to-code-snippets-on-gatsby-the-lazy-way-e93111e542f8?source=collection_archive---------3----------------------->

## 向 Gatsby 上的代码片段添加复制按钮的懒惰方式。

![](img/508a80cd888accbd89dfdd98e71547d0.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我经常在我的博客文章中写代码和分享代码片段，复制粘贴代码是软件工程师的一项基本技能，因为选择一个文本然后按下`CTRL + C`然后按下`CTRL + V`是一项大量的工作，所以我决定在我的所有代码片段中添加一个复制按钮，以方便我所有软件工程师同事的生活。

# 可能的解决方案

正确的方法是创建一个插件来接入 Gatsby HTML 生成过程，并访问 AST 数据结构中的代码片段对象。有一个[非常好的教程](https://thundermiracle.medium.com/add-copy-button-to-your-gatsbyjs-blogs-code-block-a2711364a229)是由 [@thundermiracle](https://thundermiracle.medium.com/) 提供的，关于如何做到这一点。

当然，我决定用一种糟糕的方式，那就是修改`gatsby-node.js`文件中`createPages`函数的 HTML 字符串。

# 代码

在创建文章页面的循环中，我在`gatsby-node.js`上添加了以下代码:

对于`generateAlternativeHtml`函数，我将使用 [jsdom](https://www.npmjs.com/package/jsdom) 包来解析 HTML 字符串并将其转换为 dom 对象，然后使用`querySelectorAll`方法找到所有代码片段并向它们添加复制按钮。

现在所有的代码片段都有一个复制按钮，但是这个按钮不做任何事情。我将添加`onclick`事件处理程序到复制按钮，将代码片段复制到剪贴板。这需要在代码的`React`部分用`PostTemplate.jsx`文件中的`useEffect`来完成。

为了将代码片段复制到剪贴板，我将使用 [clipboard-copy](https://www.npmjs.com/package/clipboard-copy) 包。

搞定了。虽然粗糙，但在很多方面也很美。

# 结论

这种解决方案给静态站点生成器过程和客户端的一些 DOM 操作增加了一点点开销，但目前这是一个好的解决方案。如果你正在寻找一个快速简单的解决方案，这是正确的选择。

要查看最终结果，请查看我在个人博客上的博文:

[](https://pablo.gg/en/blog/categories/coding/) [## 关于类别编码的帖子

### 又一个开发者个人博客

pablo.gg](https://pablo.gg/en/blog/categories/coding/) 

这个帖子到此为止。我希望你喜欢它。

*最初发布于*[*https://pablo . gg*](https://pablo.gg/en/blog/coding/adding-a-copy-button-to-code-snippets-on-gatsby-the-lazy-way/)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***