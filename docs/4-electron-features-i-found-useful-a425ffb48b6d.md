# 我发现有用的 4 个电子特征

> 原文：<https://javascript.plainenglish.io/4-electron-features-i-found-useful-a425ffb48b6d?source=collection_archive---------5----------------------->

## 在使用电子 JS 时，我发现一些有用的电子特性列表

![](img/5dcec10defefff0348324931cf8e1b52.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我一直在寻找一种工具或框架来帮助我开发跨平台的桌面应用程序。我想到的另一件事是，这个工具应该提供与硬件设备交互的方式。在那里我找到了电子，它满足了我的两个要求。

在这篇文章中，我将回顾一些我在使用电子时发现有用的特性。我希望你也会发现它们对你的发展有所帮助。我们最喜欢的代码编辑器 Visual studio 代码也有电子做后盾！

使用 electron，我们可以创建在 Windows、Mac 和 Linux 上运行的跨平台应用程序。它将拥有自己的 Chromium 浏览器来呈现用户界面。我假设您对 JavaScript、HTML 和 CSS 有很好的了解，并且知道如何创建基本的电子应用程序。所以我就直接跳到特色了。

1.  **将网页载入电子浏览器窗口。**

我们可以利用`createWindow()`函数将网页加载到新的`BrowserWindow` 实例中。我们可以用默认的宽度和高度初始化窗口。当 app 准备好时，我们可以调用`createWindow()` 函数，因为我们可以利用`app.whenReady().`一旦这个承诺被解决，它将调用创建窗口函数。

`app.whenReady().then(() => { createWindow()})`

我们可以使用`**setFullScreen**`将浏览器窗口设置为**全屏**。

```
const win = new BrowserWindow({ /* props */})
win.setFullScreen(true);
```

**2。IPC —进程间通信**

IPC 在电子应用程序开发中起着重要的作用，因为它提供了主进程和呈现器进程之间的网关。

我们可能会遇到这样的情况，我们必须根据来自电子主进程文件的响应将数据加载到网页中，或者我们需要根据用户与您的应用程序的交互来调用电子主进程中的任何子进程。这些情况可以通过使用 IPC 通道来处理。

**从渲染器与主进程通信(例如从您的。js 或者。苗条的文件)**

我们可以使用`**ipcRenderer.send**` 发送目标为`**ipcMain.on**`的消息

```
ipcRenderer.send('function_name', arg)   //from renderer process // inside main process
ipcMain.on('function_name', (event, arg) => {
console.log(arg)
})
```

您也可以使用`**webContents.send**`调用渲染器进程中的函数

```
// Inside main processconst win = new BrowserWindow({ /* props */}) win.webContents.send('function_name'); // Inside renderer process for accepting the functionipcRenderer.on('function_name', () => {
 /* functional logic */
})
```

**3。从电子主窗口创建子窗口**

可能会遇到这样的情况，我们必须集成拥有自己 UI 的第三方库。我们可以从主窗口创建一个新窗口，并将 UI 加载到新窗口(子窗口)中。
例如，如果我们正在集成支付 API 库，一旦用户验证完成，我们可以在新窗口中打开包含用户名和密码的支付表单。这样会给用户更好的 UI 体验。付款流程完成后，新窗口(子窗口)将关闭并返回主窗口。

```
const childWin = {};
childWin[WINDOW_ID] = new BrowserWindow({//Props
});
```

我们可以通过使用电子版提供的`ipcMain` 和`ipcRenderer` 来完成 renderer 文件和 main.js 文件之间的通信。

**4。包装电子应用**

我更喜欢用电子生成器来打包电子应用程序。电子生成器附带了许多其他功能，可以简化您的工作。

**我试着创建一个包含安装文件的文件夹，这样在安装电子应用程序时，这个文件夹也会被执行，可执行文件也会被安装在客户端系统上。**构建完成后，我面临着保存文件和访问它们的问题。我的想法是获取客户机上的文件夹路径，并使用 cmd 执行文件。我通过使用`extraResources` 属性解决了这个问题。感谢电子建造者。

通过使用`extraResources,` ,我可以保存一个包含可执行文件的文件夹，并通过 cmd 获得执行它们的路径。请按照以下步骤操作。

1.  在项目目录中创建一个与 package.json 相邻的文件夹，并将所有需要的文件保存在该文件夹中。
2.  在 package.json.
    下面添加`“build”: { “ extraResources ” : [ “ ./Folder_name/** ” ] }`
3.  使用`__dirname + '/../Folder_name'`获取文件夹的路径
4.  使用此路径通过 cmd 执行文件，cmd 可以通过节点子进程运行。

这就是本文的全部内容。如果你觉得这篇文章有帮助，请不要忘记检查我的其他文章！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***