# 如何将您的 Angular 应用程序转换为 PWA (2022)

> 原文：<https://javascript.plainenglish.io/this-is-how-to-convert-your-angular-app-into-a-pwa-2022-694a086effc5?source=collection_archive---------5----------------------->

## 关于如何将 Angular 应用程序转换为渐进式 web 应用程序(PWA)的教程。

你听说过 PWA 的成功故事吗？

例如，当星巴克从 iOS 应用程序转换到 PWA 时，他们能够将应用程序的大小减少 99.84%。您可以在此阅读详细的案例研究[。](https://formidable.com/work/starbucks-progressive-web-app/)

Pinterest 的广告收入增长了 44%。

更不用说 Spotify、优步、Twitter 和其他已经在渐进式网络应用上取得巨大成功的公司了。

![](img/6f60cfb033808dbf7174d5ce00ccf999.png)

但即使有这些诱人的成功故事，我仍然遇到一些公司正在使用 Angular，但没有将他们的 Angular 应用程序转换为 PWA——即使只需要 5 分钟或更少。😲

例如，我最近为丹麦一家名为 [Relion](https://relion.dk) 的初创公司做了一些[角度咨询](https://danielk.tech/consulting)。他们遇到了运行时性能问题，打电话给我来帮助他们。有一次，我不经意地提到考虑使用 PWA 来提高他们的加载时性能，并惊讶地发现他们对 Angular 的渐进式 web 应用程序功能了解不多。

![](img/5d4057014a36602dc50e00a6beaee89a.png)

所以…

今天，我们将讨论使用 Angular service workers 来创建 PWA(渐进式 web 应用程序)。

准备好了吗？

让我们深入研究一下，从优势开始。

# 有什么优势？

以下是将 Angular 应用程序转换成渐进式 web 应用程序的一些好处。

*   疯狂的负载速度性能(如果做得好)。
*   一个类似原生的应用程序，可以通过移动浏览器或谷歌 Play 商店(如果你知道怎么做，还有苹果商店)访问。
*   App store 独立性。
*   能够离线操作(感谢服务人员)。
*   通过服务人员发送推送通知的能力。
*   有一个自定义闪屏(在 Angular 中也称为[应用外壳)](https://danielk.tech/home/angular-app-shell-ultimate-guide)
*   令人敬畏的搜索引擎优化得分——作为快速响应的网页，PWAs 的平均搜索引擎优化得分为 85 分。
*   更小的文件大小(本地应用比 PWA 需要更多的数据来下载)。
*   无痛更新(服务人员会在后台自动更新应用，无需用户做任何事情)。

# 缺点是什么？

缺点？

坦率地说，我知道的缺点很少。

我所知道的最大的缺点是苹果商店的政策不允许开发者将他们的渐进式网络应用程序作为一个应用程序来部署。

你的应用应该包括功能、内容和用户界面，使其超越一个重新包装的网站。如果你的应用不是特别有用、独特或“像应用一样”，它就不属于应用商店。— 苹果应用商店

如果你知道任何其他突出的缺点，那么请在这篇文章的底部留下评论。👇

# 怎么做？

第一步是[使用 Angular CLI](https://danielk.tech/home/how-to-install-and-use-the-angular-cli) 安装 [@angular/pwa](https://npmjs.com/@angular/pwa) 包。

```
ng add @angular/pwa
```

过去，专家们需要几个小时甚至几天来创建一个 PWA——现在，一个 3 岁的剃须刀可以在你阻止他之前安装这个。

刚刚发生了什么？

![](img/f0b164ff7a6b502d766b0b57f0a40a0a.png)

`@angular/pwa`包是一个 Angular 示意图，它将[渐进式 Web 应用](https://web.dev/progressive-web-apps)支持添加到 Angular 应用中。简而言之，这里有一些你应该知道的事情:

*   在 app 模块中自动导入并注册服务人员。
*   更新`index.html`以包含`manifest.json`文件，该文件包含关于渐进式 web 应用程序的详细信息。
*   创建图标文件以支持 PWA。这些都放在`src/assets/icons`文件夹中，应该用应用程序的图标进行更新，以便进行品牌推广。
*   创造了`src/ngsw-config.json`。该文件用于配置服务人员。

这就是如何将你的 Angular 应用程序转换成 PWA。

如果您对如何配置缓存行为有疑问，请查看 Angular 文档中的[页面。](https://angular.io/guide/service-worker-config)

# 有角度的 PWA 是如何工作的？

如果你正在努力理解正在发生的一切，让我花点时间来解释一下。

首先，渐进式 web 应用程序只不过是一个美化了的网页，它使用[服务工作者](https://en.wikipedia.org/wiki/Progressive_web_application#Service_workers)来缓存资产和数据以供离线使用或加快加载速度。

我们刚刚做的是使用`@angular/pwa` schematics 包创建一个服务工作器，它将缓存我们配置的任何内容。默认情况下，服务人员将自动缓存以下文件。

*   `favicon.ico`
*   所有的构建工件(JavaScript 和 CSS 包)。
*   位于资产文件夹中的任何文件。
*   配置的`outputPath`或`resourcesOutputPath`正下方的图像和字体。

现在，当我们部署我们的 Angular 应用程序时，服务人员将与它一起部署，并将缓存上面的资产。下次用户加载您的 web 应用程序时，它会加载得更快，因为您的 CSS、JavaScript 和其他资产已经被服务人员缓存了。

情况越来越好。

当您部署新版本时，服务人员将检测到这些更改，并在后台静默更新缓存，以便下次重新加载您的应用时，用户将运行最新版本。

如果您想订阅这些更新，并在缓存更新后提示用户重新加载，那么下面是如何做的。

```
import { Component, OnInit } from '@angular/core';
import { SwUpdate } from '@angular/service-worker';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit{

  constructor( private swUpdate: SwUpdate) {}

    ngOnInit() {
      if (this.swUpdate.isEnabled) {
        this.swUpdate.available.subscribe(() => {
          if(confirm("You're using an old version of the control panel. Want to update?")) {
            window.location.reload();
          }
        });
      }
    }
}
```

# 你完了！

现在我想听听你的意见:

你打算把你的 Angular 项目转换成一个渐进式的 web 应用程序吗？

又或许你觉得不值得？

请在下面的评论区告诉我。

**关注我:** [GitHub](https://github.com/dkreider) ，[中型](https://dkreider.medium.com/)，[个人博客](https://danielk.tech/)

![](img/95331bea99429ddad97fd233e334b403.png)

*最初发布于*[*https://danielk . tech*](https://danielk.tech/home/angular-pwa)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/)***[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。****