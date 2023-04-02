# 全屏 API:完全指南

> 原文：<https://javascript.plainenglish.io/fullscreen-api-a-complete-guide-9be8614cbd39?source=collection_archive---------13----------------------->

## 一个简单而强大的 Web API。

![](img/2a3c09de4a85fe40b033bf644140cbf7.png)

Photo by [imso gabriel](https://unsplash.com/@imsogabriel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着我们向更真实的 web 应用程序发展，我们的 JavaScript APIs 正在努力保持领先。全屏 API[是一个既简单又有用的新 JavaScript API。这个 API 允许你向用户请求全屏，然后当你完成时离开全屏。](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API)

这是一个很棒的 API，允许你在用户已经习惯的用户体验中全屏显示部分甚至整个网站。它只在现代浏览器中可用(不在 IE 中)。

> 全屏 API 适用于视频和视频游戏。

下面是如何让这个非常简单的 API 为您服务的方法！

为了理解这个 API，让我们看一下下面的例子。

```
<button (click)="enterFullScreen" class="item">Enter Fullscreen</button>
<br>
<br>
<br>
<br>
<video controls id="video">
  <source src="nature.mp4" type="video/mp4">
</video><style>
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
  const button = document.querySelector('.item');
  const video = document.querySelector('#video');
  button.addEventListener('click', () => {
    video.requestFullscreen()
      .then(() => { console.log('Success'); })
      .catch(err => { console.log('Error : ', err); })
  });
</script>
```

![](img/25c31bf646a16252f8b923c9161efefc.png)

Output

这里，我们有一个按钮和一个视频元素。我们希望一点击按钮就全屏打开视频。所以在点击按钮时，我们为`video`元素调用了`requestFullscreen`。这就是了。视频现在将全屏播放。

要以编程方式退出全屏，我们可以使用:

```
video.exitFullscreen();
```

> 我们也可以按`F11`或`Esc`退出全屏模式。

> 如果我们想使用 CSS 样式，`:fullscreen`伪类选择全屏显示的元素。

## 全屏属性

`Document`界面具有可用于识别全屏模式是否受支持和可用的特征，以及全屏模式激活时哪个元素当前正在使用屏幕。

*   **document . full screen element**:已经被推至全屏的元素
*   **document . full screen enabled**:注意当前是否启用全屏

## 全屏事件

根据官方[文件](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API)，

> [全屏 API](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API) 定义了两个事件，可用于检测全屏模式何时启用和禁用，以及从全屏模式转换到窗口模式期间何时出现问题。
> 
> **1。全屏改变**:当一个`Element`进入或退出全屏模式时发送给它。
> 
> **2。全屏错误**:当试图将一个`Element`切换到全屏模式或从全屏模式切换出来时，如果出现错误，则发送给这个`Element`。

## 结论

全屏 API 既容易使用又非常有益。这个 API 包含了进入和退出全屏模式的方法，以及一个检测全屏状态变化的事件，因此您可以在所有方面都有所了解。为将来的项目记住这个有用的 API 你永远不知道它什么时候会派上用场！

*这是它的这篇文章。我希望你今天学到了一些新东西。您可以在* [*上*](https://gouravkajal.medium.com/membership) [*关注我*](https://gouravkajal.medium.com/) *中* *或在*[*LinkedIn*](https://www.linkedin.com/in/gouravkajal/)*上与我联系。想看更多这样的文章，敬请期待！*

*感谢阅读！*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*