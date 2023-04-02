# Next.js:解释了 getStaticPaths 和 getStaticProps

> 原文：<https://javascript.plainenglish.io/nextjs-static-site-generation-getstaticpaths-getstaticprops-b0c3d7f27cd0?source=collection_archive---------9----------------------->

## 使用 getStaticPaths & getStaticProps 在 Next.js 中生成静态站点的教程

![](img/7e98d56340f1002e4286a49f1aa4668b.png)

在本教程中，我们将探索如何在 Next.js 中创建静态站点，并在我们的应用程序中使用它们。

在 Next.js 中，设置**静态路线**和**时，需要在您的**页面**文件夹中为您的路线定义动态路线**。这是在呈现之前创建页面所必需的。

如果您想回忆一下 Next.js 动态路线，我建议您阅读我的另一篇文章:

[](https://melih193.medium.com/how-to-start-adding-new-routes-to-your-next-js-application-f529218f27d) [## 如何开始向 Next.js 应用程序添加新路线

### 在本教程中，我们将探索如何在我们的 nextjs 应用程序中添加新的路线，例如(基本的，嵌套的…

melih193.medium.com](https://melih193.medium.com/how-to-start-adding-new-routes-to-your-next-js-application-f529218f27d) 

## 如何在构建时创建动态页面？

在 Next.js 项目中，当您构建应用程序时，它已经在**中为您创建了动态页面。next/server/pages/{ dynamic path }**

创建这些动态路径对于 SEO 和我们希望在应用程序中显示的内容非常重要。

根据我们想要使用的数据，我们需要使用两个主要函数来创建这些动态页面:

1-***getStaticProps***

2-***getStaticPaths***

让我们回顾一下这些函数，并试着理解我们什么时候需要使用它们。

## getStaticProps

如果您调用并使用 getStaticProps，Next.js 将预先呈现您的应用程序。

```
export async function getStaticProps(context) {
  return {
    props: {}, // props will be passed to component
  }
}
```

当您需要从数据库或 CMS 获取数据时，getStaticProps 是在页面呈现并显示在页面上之前获取数据的方法。

如果必须呈现页面并避免数据提取组件的闪烁问题，您应该在页面呈现之前使用 getStaticProps。

这个函数总是在构建时运行，从不在客户端运行。这意味着无论何时你在你的项目中运行**下一个构建**脚本，它都已经为你获取并准备好了页面。

该功能只能在页面内从**直接**导出**。您不能从其他文件中导出它。**

## getStaticPaths

什么时候应该使用 getStaticPaths？

如果您正在获取一些数据，并且您的页面生成依赖于这些数据，我们应该使用***getStaticPaths***和***getStaticProps***

这些从动态路径生成的静态站点使用并创建 getStaticPaths 中指定的所有动态页面。

## 我们如何使用 ***getStaticPaths 和 getStaticProps 并举例***

假设我们正在应用程序中创建一个包含许多不同产品的产品页面。这些产品细节来自服务器，我们想为这些页面创建一个动态路径。

要在一个动态页面中创建所有这些页面，我们需要创建:

*   这些产品及其相应标识符的动态路径。

为了能够获得所有这些路径，我们需要使用 ***getStaticPaths。***

我们需要使用***getStaticProps****来使用这个标识符，并在我们的动态路径中获取特定产品的相应数据。*

*在本例中，我们将使用[https://dummyjson.com/products](https://dummyjson.com/products)获取产品，并为每个产品创建一个动态产品页面。*

*首先，我们需要创建**页面/产品/索引. tsx** 页面*

*在页面呈现之前，我们已经获取了所有的产品，并且创建了产品页面。*

*现在我们需要用 getStaticPaths 和 getStaticProps 创建每个单独的产品页面。*

*我们应该在这里创建动态页面为**/pages/products/[id]. tsx .***

*我们已经用获取的数据创建了所有的动态页面。*

*如果你想看所有的实现，你可以点击这里:*

*仅此而已:)*

**如果你觉得这篇文章很有帮助，你可以通过使用我的推荐链接注册一个* [***中级会员来访问类似的文章***](https://melihyumak.medium.com/membership) *。*T32*

****关注我的*** [**推特**](https://twitter.com/hadnazzar)*

*[![](img/c012fae801a3ab846a63dc560d09ff17.png)](https://www.youtube.com/c/TechnologyandSoftware)

Subscribe for more on [**Youtube**](https://www.youtube.com/c/TechnologyandSoftware?sub_confirmation=1)* 

## *编码快乐！*

*梅利赫*

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**