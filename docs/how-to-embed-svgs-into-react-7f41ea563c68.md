# 如何将 SVG 嵌入 React

> 原文：<https://javascript.plainenglish.io/how-to-embed-svgs-into-react-7f41ea563c68?source=collection_archive---------9----------------------->

![](img/61bb6a1130314cb1e1a96ebf1713f7cc.png)

Photo by [Adam Winger](https://unsplash.com/@awcreativeut?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望将 SVG 嵌入到 React 应用程序中。

在本文中，我们将研究如何将 SVG 嵌入 React 应用程序。

# 用 JSX 直接加他们

我们可以将 SVG 和 JSX 一起直接嵌入到 React 应用程序中。

例如，我们可以写:

```
import React from "react";const SvgWithXlink = (props) => {
  return (
    <svg
      width="100%"
      height="100%"

      xmlnsXlink="http://www.w3.org/1999/xlink"
    >
      <style>{`.classA { fill:${props.fill} }`}</style>
      <defs>
        <g id="Port">
          <circle style={{ fill: "inherit" }} r="10" />
        </g>
      </defs> <text y="15">black</text>
      <use x="70" y="10" xlinkHref="#Port" />
      <text y="35">{props.fill}</text>
      <use x="70" y="30" xlinkHref="#Port" className="classA" />
      <text y="55">blue</text>
      <use x="70" y="50" xlinkHref="#Port" style={{ fill: "blue" }} />
    </svg>
  );
};export default function App() {
  return (
    <div className="App">
      <SvgWithXlink fill="green" />
    </div>
  );
}
```

将 SVG 嵌入到`SvgWithXLink`组件中。

我们只是将嵌入 SVG 所需的元素放入组件中。

我们可以像处理任何其他 HTML 元素或组件一样，将属性传递到元素中。

我们有`circle`来添加圆。

而`xLinkHref`属性让我们可以通过`g`元素的`id`进行循环。

`x`和`y`是元素所在位置的坐标。

在`App`中，我们添加`SvgWithXLink`并把`fill`道具设置为`'green'`。

现在我们看到三个圆圈。

# 结论

我们可以将 SVG 和 JSX 一起直接嵌入到 React 应用程序中。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*