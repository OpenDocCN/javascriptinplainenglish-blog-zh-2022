# 如何在 React Native 中构建跨平台移动 App

> 原文：<https://javascript.plainenglish.io/how-to-build-cross-platform-mobile-app-in-react-native-fb425c8a3592?source=collection_archive---------10----------------------->

![](img/7c3db2086b97abd333be48120e2f222d.png)

## **简介**

当谈到移动应用程序开发时，你选择的框架是什么？React Native 是脸书开发的一个开源框架，建立在 React 框架之上。它允许开发者使用 JavaScript 创建跨平台的 iOS 和 Android 应用程序。

它不同于其他使用 JavaScript 的跨平台框架，因为应用程序逻辑在 JavaScript 中运行，产生的应用程序 UI 是 100%原生的。这意味着您不必处理通常与管理基于 HTML5 的 UI 相关的许多妥协。

## **设置您的开发环境**

确保您的开发环境设置了安装了正确软件包的节点。如果你在 Mac 上工作，你可以使用苹果模拟器和安卓模拟器。如果你在 Windows 或 Linux 上工作，你只能使用 Android 模拟器进行测试。然而，你应该能够将你的物理设备连接到任一操作系统来测试你手机上的应用程序。

## **你需要的工具**

IDE 或代码编辑器，例如 Visual Studio 代码

终端/Bash 应用，例如 iTerm 2、Apple 终端等。

在浏览器中安装 Redux DevTools

## **您将需要的软件包**

创建 React 应用

世博会框架

Redux

纱线或 nmp

## **设置您的项目**

在桌面上创建一个文件夹，并将其命名为您的应用程序。

在代码编辑器中打开项目。

使用您的终端 cd 进入项目目录，并设置一个样板文件 [React 本地应用程序](https://educationecosystem.com/glenettn/2bOj9-how-to-create-volunteer-delivery-app)。使用此代码:

```
npx create-react-app my-app-web
```

设置好应用程序后，使用您的终端应用程序将 cd 放入其中，然后运行该应用程序。

```
cd my-app-webnpm run start
```

您应该会看到应用程序在您的浏览器中运行。现在，您可以安装一些包并清理 React 应用程序的样板文件。

## **设置 Redux 商店**

您已经安装并运行了 React 本地应用程序，现在可以开始在 Redux Store 上工作了。您将需要一个 store.js 文件以及用于操作和缩减器的文件夹。

在 src 文件夹中创建 store.js 文件，并输入下面的代码来设置 Redux 存储。

```
import { createStore, applyMiddleware } from 'redux';import { composeWithDevTools } from 'redux-devtools-extension';import thunk from 'redux-thunk';import rootReducer from './reducers';const initialState = {};const middleware = [thunk];const store = createStore(rootReducer, initialState, composeWithDevTools(applyMiddleware(...middleware)));export default store;
```

## **创建卡片缩减器**

现在创建一个名为 actions 的空文件夹和一个名为 reducers 的空文件夹，并将它们放在 src 文件夹中。

进入 reducers 文件夹，创建一个名为 index.js 的文件。

## **将应用程序连接到 Redux 商店**

最后，将 actions 和 reducers 连接到主 App.js 文件。首先创建一个 App.css 文件，并将其放在 src 文件夹的根目录下。

现在，您可以随心所欲地向应用程序添加样式。

如果你做的一切都是正确的，你应该看到移动应用程序的工作！你可能需要重新加载浏览器或重启模拟器或手机才能看到它工作。

## **结束语**

虽然用本地语言开发移动应用程序将使您拥有 iOS 或 Android 所能提供的所有武器，但是将具有更快开发速度的 React 本地技术带到桌面上会节省您的软件项目时间和金钱。在本文中，我们已经使用 React Native 构建了跨平台的移动应用程序。

## 进一步阅读

[](https://bit.cloud/blog/creating-a-cross-platform-design-system-for-react-and-react-native-with-bit-l7i3qgmw) [## 为 React 和 React Native with Bit 创建跨平台设计系统

### 对于 web 和移动开发，许多团队使用 React 和 React Native 来实现 UI/UX 的一致性。当开发人员…

比特云](https://bit.cloud/blog/creating-a-cross-platform-design-system-for-react-and-react-native-with-bit-l7i3qgmw) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****