# Vue.js 的 10 个有用的自定义挂钩

> 原文：<https://javascript.plainenglish.io/10-useful-custom-hooks-with-vue-js-37f0fd42ce0d?source=collection_archive---------0----------------------->

![](img/9d9251952998f28edae1418ee00fb499.png)

Photo by [Jamie Matociños](https://unsplash.com/@jamievalmat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/hook?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Vue.js 是我使用的第一个 JavaScript 框架。我可以说 Vue.js 是我进入 JavaScript 世界的第一扇大门。目前，Vue.js 仍然是一个令人敬畏的框架。我觉得有了 composition API，Vue.js 只会增长更多。在本文中，我将向您展示 10 个有用的定制钩子，您可以使用 Vue.js 来制作它们。

# 使用 WindowResize

这是一个基本的钩子。因为它被用在很多项目中，而且用纯 JavaScript 或任何框架来构建它太容易了。Vue 也是一样，只需要几行代码就可以构建它。以下是我的代码:

不仅构建简单，您还可以轻松使用它。只需要调用这个钩子来获得窗口的宽度和高度:

```
setup() {
    const { width, height } = useWindowResize();
}
```

# 使用存储

您希望通过将数据的值存储在会话存储区或本地存储区并将该值绑定到视图来持久化数据吗？用一个简单的挂钩——使用储物件，就能轻松搞定。我们只需要创建一个钩子，返回从存储器中获取的数据，并创建一个函数，在需要修改数据时将数据存储在存储器中。这是我的钩子。

在我的代码中，我使用 JSON.parse 和 JSON.stringify 来格式化数据。如果不想格式化，可以去掉。这是一个如何使用这个钩子的例子。

```
const [token, setToken] = useStorage('token');setToken('new token');
```

# **使用网络状态**

这是一个有用的钩子，它支持检查网络连接的状态。为了实现这个挂钩，我们需要为“在线”和“离线”的事件添加事件侦听器。在事件中，我们只是调用一个回调函数，参数为网络状态。以下是我的代码:

就是好用。目前，我用参数“online”/“offline”调用回调函数。您可以将其更改为真/假或任何您想要的值。

```
useNetworkStatus((status) => { 
    console.log(`Your network status is ${status}`);
}
```

# 使用 CopyToClipboard

将文本复制到剪贴板是每个项目中一个流行的功能。我知道我们可以创建一个函数来代替钩子。但是我喜欢数字 10，所以我决定把这个挂钩放在这篇文章里。这个钩子非常简单，只需返回一个支持将文本复制到剪贴板的函数。

在我的代码中，我已经在函数 **copyToClipboard** 中将逻辑文本复制到剪贴板。我知道我们有很多方法可以做到这一点。您可以在此功能中尝试最适合您的方式。至于怎么用，就叫吧。

```
const copyToClipboard = useCopyToClipboard();copyToClipboard('just copy');
```

# 使用主题

只是一个改变网站主题的短钩。它帮助我们轻松地切换一个网站的主题，只需用主题名调用这个钩子。这是一个我用来定义主题变量的 CSS 代码例子。

```
html[theme="dark"] {
   --color: #FFF;
   --background: #333;
}html[theme="default"], html {
   --color: #333;
   --background: #FFF;
}
```

要改变主题，我们只需要定制一个钩子，它将返回一个函数，通过主题名称来改变主题。下面是我为这个钩子编写的代码:

而且太容易使用了。

```
const changeTheme = useTheme();
changeTheme('dark');
```

# usePageVisibility

有时候，当客户不关注我们的网站时，我们需要做一些事情。要做到这一点，我们需要知道用户是否在集中注意力。这是定制的钩子。我称之为 **usePageVisibility** ，下面是这个钩子的代码:

为了使用这个钩子，我们只需要创建一个回调函数，它带有一个客户端隐藏状态(焦点状态)的参数。

```
usePageVisibility((hidden) => {
   console.log(`User is${hidden ? ' not' : ''} focus your site`);
});
```

# 使用视口

在第一个定制钩子中，我们构建了 **useWindowRezie** ，它帮助我们观察窗口的当前宽度和高度。我认为它对那些想要构建适用于多种屏幕尺寸的东西的人很有帮助。在我处理的案例中，我们经常使用宽度来检测当前的用户设备。它帮助我们在他们的设备上安装一些东西。在这个钩子中，我将用 **useWindowResize** 构建相同的钩子，但是它返回设备名称而不是宽度和高度值。这是这个钩子的代码。

太简单了。除了默认的设备尺寸，当我们用包含手机和平板电脑尺寸的参数对象调用钩子时，用户可以修改它。我们的工作方式是这样的:

```
const { device } = useViewport({ mobile: 700, table: 900 });
```

# 使用点击外部

目前，模态被用于许多应用中。这对很多用例(表单、确认、警告等)真的很有帮助。我们经常处理的一个流行动作是当用户在模态之外点击时。 **useOnClickOutside** 对于这种情况是一个有用的钩子。我们只需要一个 ref 元素，回调函数并将其绑定到窗口事件中。以下是我的代码(桌面和移动):

如我所说，要使用它，我们只需要用参数 ref 元素和回调函数调用它。

```
<template>
    <div ref="container">View</div>
</template>
<script>
import { ref } from 'vue';export default {
    setup() {
        const container = ref(null);
        useOnClickOutside(container, () => {
            console.log('Clicked outside'); 
        })
    }
}
</script>
```

# 使用滚动按钮

除了分页列表，load more(或 lazy load)是一种友好的数据加载方式。特别是对于移动设备，几乎所有运行在移动设备上的应用程序都会在其 UI 中加载更多的负载。为此，我们需要检测用户滚动到列表底部，并为该事件触发一个回调。useScrollToBottom 是一个有用的钩子来支持你这样做。下面是我构建挂钩的代码:

在我的钩子中，我通过条件“**((window . inner height+window . scrolly)>= document . body . scroll height)**在 bottom 上检测。我们有很多方法来检测它。如果你的项目符合其他条件，让我们使用它们。以下是如何使用此挂钩的示例:

```
useScrollToBottom(() => { console.log('Scrolled to bottom') })
```

# 使用计时器

最后，我们到最后一个钩子。这个钩子的代码比其他钩子长一点。 **useTimer** 将支持我们运行带有一些选项的定时器，如开始、暂停/恢复、停止。为了制作它，我们需要使用方法 **setInterval** ，在这个方法中，我们将推送处理函数。在那里，我们需要检查计时器的暂停状态。如果计时器没有暂停，我们只需要调用一个回调函数，这个函数由用户作为参数传递。为了支持用户了解该定时器的当前暂停状态，除了动作 **useTimer，**给他们一个变量 **isPaused** 作为定时器的暂停状态。下面是我构建挂钩的代码:

这里有一个使用我们的 **useTimer** 钩子的方法:

```
function handleTimer(round) {      
    roundNumber.value = round;    
}
const { 
    start,
    stop,
    pause,
    resume,
    isPaused
} = useTimer(handleTimer);
```

# 笔记

在上面，我和 Vue.js 分享了大约 10 个有用的钩子。我认为它们很容易构建和使用。我只是有一些注释给那些想用 Vue.js 使用这些钩子的人。

请记住删除您正在添加到窗口的事件。Vue 为我们提供了一个有用的组合 API **onUnmounted** ，它帮助我们在钩子被卸载之前运行我们的动作。在我构建的每个钩子中，我总是在未挂载的中移除**中的事件监听器。**

只有在真正需要的时候才使用反应变量。如果你想用一个变量来存储一些东西，当它的数据改变时，你想同步它的数据，让我们用反应变量。但如果只是一个变量在我们的 hook (counter，flag…)中存储数据，我觉得你没必要用反应变量。

如果可以，不要在钩子中硬编码(设置固定值)。我认为我们只需要在钩子中存储逻辑。关于配置值，我们应该让用户填写(例如: **useViewport** )。

# 结论

在我的文章中，我已经和你分享了 10 个有用的 Vue 定制钩子。希望对你有帮助。Vue.js 是一个很棒的框架，我希望你可以用它来构建更多很棒的东西。如果你对 Vue 或者其他什么有其他想法，请告诉我。您可以在他们的文档中阅读有关 Vue.js composition API 的更多信息:

[](https://vuejs.org/api/) [## API 参考| Vue.js

### vue . js——渐进式 JavaScript 框架

vuejs.org](https://vuejs.org/api/) [](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/onLine) [## navigator . online-Web API | MDN

### 返回浏览器的在线状态。该属性返回一个布尔值，true 表示联机，false 表示…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/onLine) [](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) [## 页面可见性 API-Web API | MDN

### 页面可见性 API 提供了一些事件，您可以通过观察这些事件来了解文档何时变得可见或隐藏，以及…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) 

以下是我的 10 个定制钩子的源代码:

[](https://github.com/tasynguyen3894/vue-simple-custom-hooks) [## GitHub-tasynguyen 3894/vue-简单-定制-挂钩

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/tasynguyen3894/vue-simple-custom-hooks) 

感谢阅读。

![](img/1a6c1dc61a0379e8a261de92be733a6b.png)

Photo by [Mihai Moisa](https://unsplash.com/@moisamihai092?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/river-city?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

通过 [Linkedin](https://www.linkedin.com/in/thaisangnguyen3894/) 或 [Twitter](https://twitter.com/tasyit) 联系我。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*****[***免费每周简讯***](http://newsletter.plainenglish.io/) ***。*** *在我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***中获取独家写作机会和建议。******