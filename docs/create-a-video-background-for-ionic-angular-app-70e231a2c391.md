# 为 Ionic Angular App 创建一个视频背景

> 原文：<https://javascript.plainenglish.io/create-a-video-background-for-ionic-angular-app-70e231a2c391?source=collection_archive---------7----------------------->

## 创建一个以视频为背景的 Ionic Angular 应用程序

![](img/f30208cb0c982dd3a5eca6b9f1ee9450.png)

Photo by [Emmanuel Ikwuegbu](https://unsplash.com/@emmages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你知道什么是酷吗？一个有视频背景的 app。它提供了深度，看起来很专业，而且有一种技术/酷的感觉。

本说明中显示的步骤与典型的基于 HTML web 的项目非常相似，因为这里使用的标签是直接从 HTML5 中提取的。

## 步骤 0:开始离子角度项目

如果你对 Ionic 不熟悉，那就熟悉它，因为这是开发移动或网络应用最简单的方法。如果你至少熟悉一些基于 web 的开发，不管是 HTML、CSS 还是 JavaScript，那么用 Ionic 开发移动应用程序是最简单的方法:

[](https://www.ionicframework.com) [## 跨平台移动应用开发:Ionic 框架

### Ionic Framework 的应用程序开发平台构建了令人惊叹的跨平台移动、web 和桌面应用程序，只需一个…

www.ionicframework.com](https://www.ionicframework.com) 

我正在为此应用程序使用的版本:

*Ionic CLI 版本 6.20.1*

*爱奥尼亚版本 6.2.2*

## 第一步:确定你的应用是横向还是纵向

如果你在一个风景视图中构建一个应用程序，显然你需要获得一个在风景模式下拍摄的视频，最好没有任何信箱——因为我们不会在阿拉伯的劳伦斯电影中使用它，请注意，它将出现在我们应用程序的背景中。反之亦然，如果你是在肖像模式下创建一个应用程序，一个在肖像模式下拍摄或准备的视频将是完美的。

一旦你确定了构建应用的模式，你就需要找到一个合适的视频。谷歌快速搜索推荐 pexels.com。如果你知道去哪里找，YouTube 是另一个很好的免费视频资源。当然，不言而喻，为了避免法律追索，要确保你有许可和/或确保视频是无版权的。

最终，你在哪里获得视频取决于你自己。我个人推荐使用 Canva，因为它适合我轻松找到人像或风景视频的需求，或者，你知道，你可以随时拿起手机相机拍摄蚂蚁行进、风中落叶或日落时的交通堵塞等类似情况。没有什么太*引人注目的*，因为这个视频将在背景中。

对于视频文件类型，我一般用`.webm`或者`.mp4`格式的视频。不，我没有试过`.gif`，我也不确定`.gif`在这种情况下是否有效，但请试一试。

确保视频文件不要太大(小于 1mb 或 2MB 是理想的)，并确保它是*循环友好的*，因为我们将一遍又一遍地循环这个视频。

## 步骤 2:将视频放入资产文件夹

在 assets 文件夹中，创建一个新文件夹，在本例中，我们将创建一个`videos` 文件夹。将您选择的视频放入刚刚创建的`assets/videos/`文件夹中。

仅供参考，将视频放在`assets` 文件夹中的任何地方都会使视频文件可以在你的 Ionic 应用程序中本地使用，但为了有条理，我建议将脚手架中的东西放入文件夹中。

## 步骤 3:创建一个 div 并在 scss 中修改它

在 html 文件中，执行以下操作:

home.component.html:

```
<ion-content style="overflow: hidden"><div class="backgroundLayer"><video #videoPlayer preload="auto" autoplay="true" width="100%" height="100%" muted="muted" loop="true"> <source src="../../assets/backgroundVid.mp4" type="video/mp4" /></video></div><!--Rest of you app goes here--></ion-content>
```

自动播放，循环和静音道具将确保视频会自动播放，循环和静音时，页面进入。

在其对应的 scss 文件中确保一切，为`backgroundLayer`类添加一些样式:

主页.组件. scss

```
.backgroundLayer { z-index: -1; position: absolute; top: 0; left: 0; width: 100%; height: auto;}
```

将 scss 中的 z-index 设置为-1 将确保视频停留在任何图层下方的背景中。

为了确保视频将自动播放时，用户每次进入页面，而不仅仅是在第一次。我们将以下代码添加到 home.page.ts 中:

```
...export class HomePage implements OnInit {@ViewChild('videoPlayer') mVideoPlayer: any;...async ionViewWillEnter() { const video = await this.mVideoPlayer.nativeElement; await video.muted; await video.play();}
```

作为一个 Ionic app，秉承 Ionic 的生命周期，我们使用 ionViewWillEnter()在每次进入这个页面时播放和静音视频。

就是这样！现在，你有了一个背景视频，使你的应用程序更酷、更生动。使用`<video>`标签，我们可以在 Ionic Angular 应用程序中创建一个背景视频。

*Selamat Mengaturcara*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***