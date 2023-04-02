# 如何安装精确版本的 NPM 软件包的最佳方式

> 原文：<https://javascript.plainenglish.io/how-to-install-npm-packages-with-an-exact-version-558599f0aa5b?source=collection_archive---------2----------------------->

## 为什么要在包中使用精确的包版本

![](img/09904868bf97b095abc2a42f6cc36b21.png)

# 1.安装 npm 软件包的精确版本

如果你来这里是因为 npm 默认的 semver range 运算符给你带来了麻烦，而你正在寻找一条出路，我不会延迟回答。但是，如果您也想知道*为什么*应该在 *package.json* 中保留精确的包版本，请继续阅读。

## 答:按照以下步骤安装精确版本

1.  在项目根文件夹中创建`**.npmrc**`文件。
2.  将`**save-exact=true**`添加到`**.npmrc**`文件中。
3.  利润！所有未来的 npm 软件包都将安装精确的版本。

## **备选:**

不建议，但是如果您想只安装具有精确版本的特定 npm 包，出于某种原因，您可以使用`install`命令的`save-exact`配置参数指定它，即`**npm install --save-exact react**`。也可与*纱:* `**yarn add --exact react**`纱配合使用。

# 2.语义版本控制(semver)

为了更好地理解`package.json`中的包版本和`npm install`的默认行为，理解用于 npm 包的版本控制系统是很重要的——称为*语义版本控制(sever)*。最好的解释，尤其是对于本文，可以在 [*中找到——为什么在我的包中有一个插入符号(^)。*](https://bytearcher.com/articles/semver-explained-why-theres-a-caret-in-my-package-json/)

# 3.为什么要安装一个精确的版本

总之，您对安装的软件包版本有了更多的确定性、可预测性和控制。

想象一个潜在的场景:你使用了 npm 的默认 semver range 操作符(`"**^**”`，这样你就有了 *package.json 中的`"react": "**^**16.1.0"`。*然后，又有了 *react 的新版本:* `v16.**2**.0`。所以当你运行`npm install`时，你实际上会得到`v16.**2**.0`，这通常是好的。然而，在这种情况下，新的 *react* 版本包含一个会让你的应用崩溃的 bug。因为 *package.json* 说的是`"react": "**^**16.1.0"`而不是`"react": "16.2.0"`，所以不容易识别出包更新是导致 app 崩溃的原因。另一方面，如果您使用确切的版本，您可以在单独更新 *react* 包时发现错误。

## **如果你喜欢这篇文章，请关注我，了解更多关于 React、JavaScript、TypeScript 等开发的技巧:】**

![](img/c5c5223511b66daedf7d7a68e5ab6095.png)

## 成为会员

*如果你喜欢阅读这样的故事，并想支持我成为一名作家，* [*考虑报名成为一名中等会员*](https://jakub-kozak.medium.com/membership) *。一个月 5 美元，你可以无限制地阅读媒体上的故事。如果你* [*用我的链接*](https://jakub-kozak.medium.com/membership) *注册，我会赚一小笔佣金*🙌

[](https://jakub-kozak.medium.com/membership) [## 通过我的推荐链接加入 Medium 雅各布·科萨克

### 阅读雅各布·科萨克(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

jakub-kozak.medium.com](https://jakub-kozak.medium.com/membership) 

## 工作机会——来加入我吧

我在 Tjekvik 的团队正在寻找更多的开发者！你有使用 React 和 Ruby on Rails 的经验吗？那就不要犹豫，马上申请吧:[https://www.tjekvik.com/careers](https://www.tjekvik.com/careers)。你可以在欧洲的任何地方工作！🌍

[](https://jakub-kozak.medium.com/stop-using-for-conditional-rendering-in-react-a0f7b96200f8) [## 停止在 React 中使用“&&”进行条件渲染

### 通过在 React 组件中不使用` && '来避免错误

jakub-kozak.medium.com](https://jakub-kozak.medium.com/stop-using-for-conditional-rendering-in-react-a0f7b96200f8) [](/react-hooks-when-to-use-uselayouteffect-instead-of-useeffect-3271a96d881a) [## React 挂钩—何时使用 useLayoutEffect 而不是 useEffect

### useEffect 和 useLayoutEffect 的区别——用一个真实的例子来解释。

javascript.plainenglish.io](/react-hooks-when-to-use-uselayouteffect-instead-of-useeffect-3271a96d881a) [](https://medium.com/swlh/how-to-build-a-chrome-extension-with-react-typescript-and-webpack-92e806ce2e16) [## 如何使用 React、TypeScript 和 Webpack 构建 Chrome 扩展

### 从创建样板文件到发布 Chrome 网络商店的完整扩展

medium.com](https://medium.com/swlh/how-to-build-a-chrome-extension-with-react-typescript-and-webpack-92e806ce2e16) [](https://medium.com/swlh/best-moment-js-alternatives-5dfa6861a1eb) [## 最佳时刻。JS 替代方案

### 比较大小、性能、类型脚本支持等

medium.com](https://medium.com/swlh/best-moment-js-alternatives-5dfa6861a1eb) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*