# 带有 React & TypeScript 的自定义下拉元素

> 原文：<https://javascript.plainenglish.io/custom-dropdown-element-with-react-typescript-17eef6ae84d4?source=collection_archive---------2----------------------->

## 如何使用 TypeScript 创建简单的 React dropdown 组件的指南。

![](img/18512858aba469545707670ecf487a83.png)

我们将创建一个简单的 React dropdown 组件，这只是一个简单的例子，任何人都可以使它更高级，并添加更多的功能来定制它。

dropdown 组件背后的逻辑很简单，您有一个打开和关闭 dropdown 显示的项目的状态，每当您将此状态从 false 更改为 true 时，我们将打开 dropdown 的项目，每当您选择其中一个项目时，它将关闭。有一个 useEffect 用于在用户单击页面上的任何位置时关闭下拉列表，onValueChange 函数处理状态更新，并用从下拉列表中选择的项目替换占位符。

快速提示:样式是用 Tailwind CSS 完成的，但是你可以根据你的设计和需要定制它。

那都是我送的。希望它能帮助你创建你自己的自定义组件和更多的功能。

如果你想在 LinkedIn 上联系，请点击下面的链接:

[AKIN KARAYUN | LinkedIn](https://www.linkedin.com/in/akin-karayun-ab3239bb/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****