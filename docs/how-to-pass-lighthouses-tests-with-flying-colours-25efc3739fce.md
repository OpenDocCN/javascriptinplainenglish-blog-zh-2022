# 如何顺利通过灯塔？

> 原文：<https://javascript.plainenglish.io/how-to-pass-lighthouses-tests-with-flying-colours-25efc3739fce?source=collection_archive---------11----------------------->

## 优化 WEB APP 并没有那么难！

## 优化是我们一开始就要考虑的事情

![](img/3d3d38abfc06332ec34b51a0e1b70af0.png)

Photo by [Samuel Ferrara](https://unsplash.com/@samferrara?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/mountains?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在我们进入正题之前，我想感谢摄影师为我们在这里讨论的网站提供了迷雾山脉的图片(上图)。

在探索优化应用程序的工具之前，我们将检查项目结构。这个博客中的站点是[我的作品集](https://alenvlahovljak.com/)，使用纯 HTML、CSS 和 JavaScript 构建。**想象一下构建一个没有 React 或 Angular 的 UI。如今这可能吗？**

你们中的一些人会说这是浪费时间，这是事实。但是，由于该网站是静态的，有几个页面，我决定这是一个避免更高层次抽象的好机会，并走出去学习关于 web 性能指标和 SEO 的一切。

这个机会得到了回报，原因有两个:

*   避免抽象意味着了解隐藏的东西，
*   按时间顺序分析工具，了解需求。

旅程并不容易，因为我们必须处理各种问题([清除 CSS](https://purgecss.com/) 、包大小、图像压缩等等。)已经用*现成的*解决方案— **捆绑器** ( [Webpack](https://webpack.js.org/) 、 [Vite](https://vitejs.dev/) 、 [esbuild](https://esbuild.github.io/) 等解决。).

## 重要的事情先来

在我们处理严肃的问题之前，我们先从一个简单的任务开始。图像优化是最重要的，因为这是灯塔惩罚最多的事情之一。为什么会这样呢？Lighthouse 正在测试第一个模拟慢速 3G 网络的负载，因为这仍然是世界上最常见的网络。

下载 1MB 可能需要 3 秒钟，如果我们有高分辨率的图像呢？用户可能会放弃浏览这个网站，因为需要 50 毫秒来决定他们是否喜欢这个网站。有趣的事实，这是最容易解决的。**解决方法是将所有图片转换成** [**WebP 格式**](https://developers.google.com/speed/webp) **。**

## 第一次加载就去掉无关的东西！

形成分数的两个最有影响力的东西是[最大内容油漆](https://web.dev/optimize-lcp/) — LCP 和[总阻塞时间](https://web.dev/tbt/) — TBT(其携带 50%的性能评级)。

最有内容的油漆是评估显示速度的**核心网页要害**之一。这可以通过遵循[网络生命模式](https://web.dev/patterns/web-vitals-patterns/)来解决。对于技术性贸易壁垒，我们需要一些额外的工作。

**总阻塞时间**是页面不能响应交互的时间范围。它必须低于 50 毫秒。JavaScript 是单线程语言，我们必须小心不要让主线程过载。使用 [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 缓存字体、图像、HTML、CSS 和 JS——所有静态的东西——解决了过载问题。

其他合理的事情是[清除不必要的 CSS 代码](https://purifycss.online/)并将其分成多个文件。我们还必须删除未使用的 JS 代码，但是没有捆绑器这是无法实现的。幸运的是，在这种情况下，JS 代码不会在很大程度上影响它。

# 让我们从灯塔开始测试吧！

如果我们想在 Google 上托管一个索引[高](https://backlinko.com/rank-high-on-google)的站点，必须考虑两件事:

*   搜索引擎优化— SEO
*   可达性。

没有一个就不能工作。SEO 处理网站内容的有用性。那样的话，规则就严格了。另一个重要的功能是为视障人士访问设备进行优化。

谷歌非常注重内容可用性(*座右铭。*[](https://web.dev/accessible/)*所有人都可以访问)所有上网的人，无论这是否包括暂时或永久残疾的人。没有关于解决方案的匹配，因为将会有用于修复问题的明确输入。*

# *加强你的安全！*

*另一个重要的统计数据在“最佳实践”标题下。如果应用程序类型涉及与各种外部服务(如支付处理器)的集成，这可能是最重要的功能。在这种情况下，我们必须特别注意以下事情:*

## *地点必须是 HTTPS*

*一些集成服务在没有安全连接的情况下无法工作，例如 [Stripe API](https://stripe.com/docs/security#https-hsts-secure-connections) 。*

*由于这是一个没有外部提供商的个人网站，除了电子邮件服务提供商，我们不需要实现这里介绍的所有安全协议。但是，考虑到**我们希望遵守所有协议**，我们会这样做。*

*该网站由 Netlify 托管(作为[免费托管计划](https://www.netlify.com/)的一部分)。你唯一需要支付的是一个域名。购买域名后，您必须向您购买的域名指出 Netlify 的域名服务器(NS)——在域名提供商处创建一个 NS 记录。*

*另一个通过 Netlify 提供的现成解决方案是自动分配到您的域的 SSL 证书。这可能会节省您很多时间，因为安装 SSL 认证可能会很耗时。*

## *避免使用有安全风险的库*

*鉴于当今许多软件解决方案依赖于第三方服务，我们必须关注它们的质量。开源库上许多公开的 bug 告诉我们，在将它们并入我们的系统之前，我们应该三思。*

*当我们选择没有严重安全风险的 API 时，我们的工作并没有就此停止。我们必须不时地检查服务的当前版本是否仍然没有安全风险，并在必要时更新版本。*

*有一个[实用工具](https://www.shodan.io/)记录软件安全风险。键入域就足够了，我们将获得所发现的关于风险类型和软件版本的所有信息。*

*美国国家标准与技术研究院(NIST) [网站](https://nvd.nist.gov/)是所有记录的安全风险的有用资源。有时，我们不必消除威胁并更新版本，因为我们可能不会冒险使用服务的一部分。*

## *集成内容安全策略(CSP)*

*CSP 是对抗跨站点脚本( [XSS](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting) )和数据注入的最有效的安全策略。有了“完美”的 CSP 配置，您的网站访问者就不会受到恶意代码的攻击。*

*借助 CSP，您可以控制网站上提供的资源。简单来说，CSP 是一个字符串，它指示浏览器下载资源(HTML、CSS、JS、图片、视频等)。)仅来自策略中定义的可信来源。以下是一个良好的 CSP 政策示例:*

```
*Content-Security-Policy = "
 default-src 'none'; 
 base-uri 'self'; 
 style-src 'self' https://fonts.googleapis.com; 
 script-src https://*.googleapis.com https://*.gstatic.com *.google.com https://*.ggpht.com *.googleusercontent.com blob:; 
 form-action 'self'; img-src 'self' https://*.googleapis.com https://*.gstatic.com *.google.com *.googleusercontent.com data:; 
 connect-src 'self' https://*.googleapis.com *.google.com https://*.gstatic.com data: blob:; 
 font-src 'self' data: https://fonts.gstatic.com; 
 object-src 'none'; 
 media-src 'none'; 
 frame-src *.google.com; 
 child-src 'self'; 
 worker-src 'self' blob:; 
 frame-ancestors 'none'; 
 manifest-src https://alenvlahovljak.com/manifest.json
"*
```

**您可以在* [*链接*](https://content-security-policy.com/) *找到所有指令的列表。日前(12 月 3 日)，W3C 提出了新的* [***CSP 三级策略***](https://www.w3.org/TR/CSP3/)**作为新的标准策略。***

## **添加严格传输安全标头**

****严格传输安全** [策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)是对浏览器的指示，以避免使用 HTTP 加载网站，并自动转换所有仅使用 HTTPS 请求访问网站的尝试。标准配置的示例如下:**

```
**Strict-Transport-Security = "max-age=31536000; includeSubDomains; preload"**
```

**该指令告诉我们，在 HTTPS 连接建立后，该网站在一年内被视为可信来源。不再需要转到 HTTP 并将其升级到 HTTPS 连接。**

**在隐姓埋名模式下，在网络选项卡中尝试一下。首先，浏览器请求一个 HTTP 页面，然后 HSTS 策略通过内部重定向(307)调用另一个请求来请求 HTTPS 页面。在此之后，重新加载页面，您将只看到一个对 HTTPS 的请求(200)。**

**通过*预加载*指令，网站要求将域名纳入 HSTS 预加载列表。[预加载列表](https://source.chromium.org/chromium/chromium/src/+/main:net/http/transport_security_state_static.json)包含默认标记为可信来源的所有站点的列表。换句话说，它永远不会请求 HTTP，而是永远请求 HTTPS，因为域是硬编码到浏览器引擎中的。大多数主流浏览器(Chrome、Firefox、Safari、Edge)都有 HSTS 预加载列表。**

**有一个网站可以让你手动请求将 *加入 Chrome 的 HSTS 预加载列表。***

## **x-XSS-保护**

**X-XSS 保护是一种策略，当检测到 XSS 攻击时阻止加载。在现代浏览器中，这种保护基本上是不必要的，因为在现代浏览器中，站点实现了强大的 CSP。但是，在没有实现 [CSP Level 2 策略](https://www.w3.org/TR/CSP2/)的旧浏览器(当然是 Internet Explorer)的情况下，这是推荐的，并且只有一行代码:**

```
**X-XSS-Protection = "1; mode=block"**
```

## **配置 X 框架选项和 X 内容类型选项**

**X-Frame-Options 是一个安全头，它告诉浏览器站点是否可以在 iframe 中显示。[点击劫持](https://owasp.org/www-community/attacks/Clickjacking)就是利用这一安全问题的一个攻击例子。恶意网站可能会欺骗用户点击您网站上的链接，即使这些链接看起来并不在您的网站上。**

**X-Content-Type-Options 是一个头，它告诉浏览器不要加载脚本和样式表，除非服务器通过 Content-Type 头指示正确的 [MIME 类型](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)。如果没有它，浏览器可能会执行 [MIME 嗅探](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types#mime_sniffing)(通过查看资源的字节来猜测 MIME 类型)，这可能导致 XSS 攻击。**

**两种接头都可以配置如下:**

```
**X-Frame-Options = "SAMEORIGIN"
X-Content-Type-Options = "nosniff"**
```

# **奖金！**

**那几乎是我的一切。我将提供一些有用工具的链接，这些工具可能会帮助您配置您的站点，并帮助您研究浏览器中出现的新标题(例如[权限-策略](https://scotthelme.co.uk/a-new-security-header-referrer-policy/))。以下是工具列表:**

*   **[webhint](https://webhint.io/) (一款针对网络的林挺工具)，**
*   **[VulDB](https://vuldb.com/) (所有记录软件安全问题的数据库)，**
*   **[CSP-Fiddler-Extension](https://github.com/david-risney/CSP-Fiddler-Extension) (根据您的站点需求配置 CSP)，**
*   **[DNS SPY](https://dnsspy.io/) (验证 DNS 记录)，**
*   **[SSL 实验室](https://www.ssllabs.com/ssltest/index.html)(验证 SSL)，**
*   **[Mozilla 的天文台](https://observatory.mozilla.org/)(验证头)。**

## **还有一点**

**这里是一个[脚本](https://gist.github.com/clarkio/32c7dba41dfb3418eaf1)注入到一个未受保护的站点(没有 CSP)的例子。别担心，不会有什么坏事发生——如果你不认为哈莱姆摇摆舞是件坏事的话。**

***更多内容看* [***说白了就是***](https://plainenglish.io/) *。***

***报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****有兴趣缩放你的软件启动*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***