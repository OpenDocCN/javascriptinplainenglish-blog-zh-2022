# 重定向链会伤害 SEO 吗？是的，这就是我们要做的

> 原文：<https://javascript.plainenglish.io/do-redirect-chains-hurt-seo-yes-and-heres-what-to-do-about-it-a96a55173228?source=collection_archive---------13----------------------->

## 了解什么是重定向链，重定向链是否会损害 SEO，以及如何修复它们。

![](img/89dfd346dfc690a1e6e17d76f143611c.png)

即使对于经验丰富的 SEO、开发人员和网站所有者来说，跟上搜索引擎算法或网站维护最佳实践的不断变化的需求也具有挑战性。

网站所有者面临的最常见的问题之一是重定向链。重定向链是当一个 URL 被发送到一个不同的 URL，然后被发送到第三个不同的 URL，等等。通常，网站所有者不知道如何正确设置重定向，或者当它们堆积在一起时忽略它们。这可能会导致排名惩罚，越长时间被忽略越糟糕，并造成缓慢和令人沮丧的用户体验。

在这篇博文中，我们将讨论什么是重定向链，重定向链是否会损害 SEO，以及如何修复它们。

# 什么是 301 重定向链，它们是如何发生的？

301 重定向链是一串链接在一起的 URL 序列或循环。这种情况发生在网站所有者没有充分设置重定向，导致他们的预期，最终目的地的网址。

重定向链向浏览器发出信号，表明 URL 已被移动，它会将浏览器定向到新位置。因此，以前 URL 的所有网站权限现在都转移到新 URL。

# 重定向的用途是什么

虽然重定向链很容易发生，如果网站管理员不小心或草率，301 重定向本身有很多优势。使用它们的最常见原因是:

## 将用户导向主页

网站类型多种多样——看似很小的变化 *HTTP* 或者 *HTTPS* 和 *WWW* 。非 WWW 可以彻底改变 URL 对网络浏览器的意义。无论用户在网址栏中输入什么，重定向都会将他们带到正确的网站。

例如，如果用户键入“HTTP://www.example.com”，301 重定向会自动将他们带到“HTTPS://example.com”。这一点很重要，因为它确保了用户总是停留在正确的网站上。

## 没有重复的内容

重复的页面只会给你的用户和谷歌搜索引擎机器人带来混乱。因此，网站所有者将使用重定向将用户导向正确的页面，避免任何[重复内容问题](https://prerender.io/blog/how-to-fix-duplicate-content-issues/)。

## 保持旧网站的流量

如果你已经建立了一个有流量和网站权威的网站，但是转到了一个不同的领域，你不想失去你辛辛苦苦为旧网站获得的所有流量。因此，网站所有者将使用重定向将用户从旧的域名引导到新的域名。这确保用户仍然能够找到他们正在寻找的内容，同时仍然保持你的旧网站的流量和排名。

例如，Hotmail 被 Outlook.com 取代，但是用户会被自动重定向到新的网站，这样他们仍然可以找到他们的电子邮件。

## 将多个域合并成一个域

拥有多个域会让用户感到困惑，还会导致内容重复的问题。因此，网站所有者将使用重定向将用户从多个域定向到一个域。这有助于简化用户体验，并避免任何重复内容问题。

# 301 重定向链如何从 URL A -> B -> C

![](img/66537f61af461706a6f8dc9c4e64a6e2.png)

下面是一个 301 重定向链如何发生的示例:

1.  用户在他们的 web 浏览器中键入“example.com”。
2.  web 浏览器向服务器发送对“example.com”的请求。
3.  服务器以 301 重定向代码作为响应，并将 web 浏览器定向到"example.com/index.html"。
4.  web 浏览器向服务器发送"example.com/index.html"请求。
5.  服务器以 301 重定向代码作为响应，并将 web 浏览器定向到"example.com/home.html"。
6.  web 浏览器向服务器发送"example.com/home.html"请求。
7.  服务器以 301 重定向代码作为响应，并将 web 浏览器定向到"example.com/"。
8.  web 浏览器向服务器发送"example.com/"请求。
9.  服务器用所请求的网页进行响应。

这是一个非常漫长且毫无必要的过程。用户不仅要花很长时间才能到达想要的网页，还浪费了大量资源。此外，这可能导致[技术 SEO 问题](https://prerender.io/blog/technical-seo-issues/)，我们将进一步探讨。

# 301 和 302 重定向的区别

虽然 [301 和 302 重定向](https://developers.google.com/search/docs/advanced/crawling/301-redirects)都是流行的选择，但它们在持久性和对 SEO 的影响上有所不同。

301 重定向是一种永久重定向，这意味着该 URL 已被永久移动到一个新位置。这是最常见的重定向类型，通常在网站所有者想要更改域名或将网站移到新位置时使用。

302 重定向是一种临时重定向，这意味着 URL 已被临时移动到一个新位置。当网站所有者希望对他们的网站进行一些维护或进行一些更改时，通常会使用这种类型的重定向。

# 301 重定向如何影响 SEO

虽然 301 重定向是拥有一个网站的必要组成部分，但如果管理不善或允许无限期链接在一起，它们会损害网站的 SEO 健康。这是因为每次建立 301 重定向而不删除中间 URL 时，都会创建一个所谓的“重定向链”。重定向链是指一行中有多个 301 重定向。例如，如果用户键入“example.com”并被重定向到“example.com/index.html ”,然后被重定向到“example.com/home.html ”,这就是一个重定向链。

重定向链会损害 SEO，因为它们会使搜索引擎难以索引你的网站，因为搜索引擎网络爬虫会迷失在你的重定向链中，耗尽你的[爬虫预算](https://prerender.io/benefits/bigger-crawl-budget/)。重定向链也会降低你网站的速度，这也会影响你的搜索引擎优化，因为它们会影响你的用户指标。

你必须确保你的网站加载迅速，否则你将受到谷歌的惩罚。像 [Google Page Speed Insights](https://prerender.io/blog/google-pagespeed-insights/) 这样的工具为你网站的加载速度提供了有价值的见解，并提供了可行的建议，告诉你如何改进。

在 2016 年之前，人们认为一个网站会随着链中的每次重定向而失去 Pagerank。然而，谷歌已经声明事实并非如此，并且[网站不会因为每次重定向](https://www.searchenginejournal.com/301-redirect-pagerank/275503/#:~:text=In%20other%20words%2C%20the%20301,topic%20of%20the%20old%20page.&text=This%20is%20interesting%20because%20it's,a%20canonical%20URL%20is%20handled.)而损失 Pagerank。

# 如何修复重定向链

如果你的网站上有重定向链，你可以做一些事情来修复它。

# 删除不必要的重定向

第一步是始终删除任何不必要的重定向。如果有不再需要的重定向，请将其删除。一旦您删除了 301 链中不必要的重定向，它将确保只有一个 301 重定向发送访问者从起始 URL 到最终目的地 URL。这将有助于减少重定向链的长度，使搜索引擎更容易索引您的网站。

# 尖叫青蛙重定向报告

尖叫青蛙是一个免费的工具，可以用来检查你的网站重定向链。将您网站的 URL 输入该工具，它将抓取您的网站并生成报告。该报告将列出您网站上的所有重定向，并显示您是否有任何重定向链。它还列出了所有重定向的状态，因此您可以很容易地确定哪些需要修复。

如果你想对你的网站做一个快速的技术搜索引擎优化审计，尖叫青蛙是一个很好的工具。但是，需要注意的是，它最多只能免费抓取 500 页。如果你有一个大型网站，你可能需要使用升级版本来做一个完整的检查。

你也可以选择使用众多[尖叫青蛙的替代品](https://prerender.io/blog/screaming-frog-alternative/)中的一个来找到一个符合你需求的技术搜索引擎优化工具。

# 在 WordPress 中设置重定向

许多新手或业余网站管理员不知道[如何用 WordPress](https://www.elegantthemes.com/blog/tips-tricks/how-to-create-redirects-with-wordpress) 创建重定向。这个插件，简单的网站重定向，允许你在 WordPress 中设置一个重定向，而不需要编辑你的。htaccess 文件。这个插件很棒，因为它简单易用。此外，这个插件保留了 URL 路径和查询字符串，因此您不必担心丢失任何 SEO 值。

# 掌握重定向而不失去搜索引擎优化

重定向是拥有一个网站的必要部分，但如果使用不当，它们会损害 SEO。重定向链会使搜索引擎很难索引你的网站，也会降低你的网站速度。

然而，你可以做一些事情来修复重定向链和提高你的搜索引擎优化。如果你遵循上述步骤，你可以利用重定向的功能，而不会危及你的网站的搜索引擎优化或用户体验。

只需一点点努力，你就可以掌握重定向而不牺牲 SEO。完成后，您可以通过使用 Prerender 的功能再前进一步。Prerender 允许您利用 Javascript 网站的预渲染，这样您可以提高页面的加载速度，而不会损害您的整体用户体验。[立即开始免费使用 Prerender！](https://dashboard.prerender.io/signup?_gl=1*u6ykf1*_ga*NzIwNTI3MDA2LjE2NTc1MTEwNDA.*_ga_5C99FX76HR*MTY1NzUxMTAzOS4xLjAuMTY1NzUxMTAzOS4w)

最初发表于 Prerender.io: [重定向链会伤害 SEO 吗？是的，下面是要做的事情](https://prerender.io/blog/do-redirect-chains-hurt-seo/)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***