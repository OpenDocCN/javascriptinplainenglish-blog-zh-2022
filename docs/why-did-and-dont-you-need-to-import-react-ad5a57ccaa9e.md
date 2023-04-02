# 为什么需要和不需要导入 React？

> 原文：<https://javascript.plainenglish.io/why-did-and-dont-you-need-to-import-react-ad5a57ccaa9e?source=collection_archive---------6----------------------->

## 这对你来说意味着什么？

![](img/f3f5829f05e4351227dddbc59909718a.png)

从 React v17.0 开始，您不必再在 JSX 文件中导入 React。但是，为什么在创建 React 组件时，这种看似未使用的导入首先是必要的呢？为什么现在不再是了？

在 React 开发的很长一段时间里，有必要在使用 React 组件的 JavaScript 或 TypeScript 文件中导入`React`。直到 2020 年 8 月发布的 React v17.0，React 才引入了一个新的转换功能，使其开发人员不必再这样做了。

但是为什么我们首先要进口它呢？我们每次创建 React 组件时都必须添加这个看似未使用的导入，这是什么原因呢？为什么我们“突然”不再需要它了？

# 我们需要它的原因

如果你不熟悉 React 开发，它由大量所谓的 React 组件组成。React 开发背后的主要理念是创建可以在不同场景中重用和组合的小组件。要创建 React 组件，标准是使用 JSX，它是 JavaScript 的语法扩展。

此类组件和 JSX 的外观示例如下:

```
import React from "react";function Card({ content }) {
  return (
    <div>
      <CardBody size="medium">{content}</CardBody>
    </div>
  );
}
```

对于大多数 React 开发人员来说，这感觉非常熟悉。这是一个接受一个道具的简单的`Card`组件。该组件本身呈现一些 HTML、一个单独的`div`和另一个名为`CardBody`的随机 React 组件。对于后一个组件，我们传递两个属性:`Card`作为其`children`接收的`content`属性和其`size`属性的静态值。

这里没什么特别的。但是在目前的形式下，浏览器对此无能为力。如前所述，JSX 是建立在 JavaScript 之上的语法扩展。浏览器不理解 JSX，所以当它试图评估这段代码时，它只会抛出一个错误。

这跟必须导入`React`有什么关系？最终，您的 React 代码仍然需要由浏览器接收和呈现。但它将首先被转换成浏览器可以理解的形式，而不是当前的形式:常规 JavaScript。这将看起来如下:

```
import React from "react";function Card({ content }) {
  return React.createElement('div', null, React.createElement(CardBody, { size: 'medium' }, content));
}
```

所有的语法糖都被去除，并转换成各自的 JavaScript 等价物。基于此，我们可以看到，使用 JSX 创建一个 React 组件只不过是一个使用 3 个函数参数的函数调用:组件的类型、它在对象形式中的属性以及它的子元素。

但最需要注意的是函数本身。在引擎盖下，React 组件是`createElement`调用，该函数来自`React`。基于此，我们可以回到本文最初的问题，理解每当我们创建一个 React 组件时导入`React`的必要性。没有它，转换后的 JSX 代码将在浏览器中失败，因为 React 需要在范围内通过其`createElement`函数创建组件。

# 我们不再需要它的原因是

所以现在我们知道了之前为什么需要它，下一个有趣的问题就变成了为什么我们突然不再需要它了。React v17.0 中的什么改变让我们不必在每个使用 JSX 的文件中执行这种烦人且看似无用的`React`导入？

简而言之，React 将创建元素的功能移向了新的入口点。它没有依赖于包的主入口点中公开的`createElement`函数，而是被分割成仅供编译器使用的入口点，如 Babel 和 TypeScript。

因此，现在在转换 JSX 时，编译器能够并且将会自动从那些新的入口点导入适当的函数。这意味着开发人员不必手动添加`React`导入，因为编译器不再需要依赖主入口点。转换前后的示例代码如下所示:

```
function Card({ content }) {
  return (
    <div>
      <CardBody size="medium">{content}</CardBody>
    </div>
  );
}// Inserted by a compiler
import { jsx as _jsx } from 'react/jsx-runtime';function Card({ content }) {
  return _jsx("div", {
    children: _jsx(CardBody, { size: "medium", children: content })
  });
}
```

为了向后兼容，这个特性也被移植到了大多数旧的 React 版本中。如果您想了解更多关于如何升级到这种新的 JSX 变换，建议看一看[升级指南](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#how-to-upgrade-to-the-new-jsx-transform)。

如果你喜欢这篇文章，可以考虑看看[不凡反应](https://www.getrevue.co/profile/chakshunyu)时事通讯和我的[推特](https://twitter.com/keraito)中的其他条目，以便将来更新。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**