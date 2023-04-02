# Meet React useEvent():最新最棒的 React 钩子

> 原文：<https://javascript.plainenglish.io/react-useevent-the-latest-and-greatest-react-hook-56ae71febbf3?source=collection_archive---------0----------------------->

## 被誉为“原 Hooks 版本中缺失的部分”，useEvent()将改变你编写 modern React 的方式。

![](img/08eaa89e8e96181a576978f7b5a66131.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

反应钩子很棒，我们不能同意吗？在很大程度上，它们允许您编写干净的、可扩展的、易于理解的具有明确定义行为的功能组件。与旧的基于类的生命周期方法和本地状态管理相比，你会想知道 React 是如何变得如此流行的。

React 团队当然将 hooks 视为未来，并准备在现有库的基础上加入 **useEvent()。**

## useEvent 解决什么问题？

在这一节，我们来看看回调函数中的**引用相等。这可能看起来令人困惑，但让我们通过一些代码示例来理解这意味着什么。**

![](img/4e5d2e807e82948efe130cc64c3fd152.png)

New hooks for use to play with!

假设我们有一个购物篮组件作为父组件，一个“购买”按钮作为子组件。我们希望“购买”按钮(子按钮)在被按下时在父按钮中执行一些代码。这可以在**回调函数的帮助下完成。**你可能见过数百个这样的例子，因为它们是一种极其常见的模式，但它可能是这样的:

```
export const Basket = () => {
  const [total, setTotal] = useState('');

  ... More component logic here ...    const onBuyClick = () => {
    showTotal(total);
  };

  return <BuyButton onClick={onBuyClick}/>;
}
```

这是一个非常有效的 React 回调实现——但是还可以改进。

每次重新呈现“Basket”组件时，它当前也会重新呈现“BuyButton”组件。这可能会导致下游的巨大性能损失(想象一下 BuyButton 有 10 层以上的组件，所有这些组件也将被重新呈现)。

*但是为什么会发生这种情况呢？这是因为* ***的参照完整性！***

看回调函数`onClickBuy` *。*当“Basket”被重新渲染时，它拆掉并重新创建这个方法。虽然这个方法的行为不会随着渲染而改变，但是它的引用标识会改变。

*本质上，React 并不认为上一次渲染的方法与当前渲染的方法相同。*

因为(默认情况下)组件在其属性改变时会重新呈现，所以“BuyButton”会重新呈现，因为`onClickBuy`方法的引用标识已经改变。

在每次渲染时更改引用标识并导致子级重新渲染是 useEvent()旨在解决的问题。

## useMemo() + useCallback()怎么样？

还记得 30 秒前我说过，默认情况下，当组件的属性改变时，组件会重新渲染吗？useMemo()和 useCallback()改变了这个默认行为。

我们可以在 useMemo()中包装我们的子组件——这意味着只要 props 等于它们在先前渲染中的值，子组件**就不会重新渲染**。

这是解决方案的一半，因为目前`onClickBuy`仍将通过 useMemo shallow props 比较检查。我们真正想做的是阻止`onClickBuy`在每次渲染时都有一个新的引用身份。我们可以通过将它包装在 useCallback()中来实现这一点，例如，

```
export const Basket = () => {
  const [total, setTotal] = useState('');

  const onBuyClick = useCallback(() => {
    showTotal(total);
  }, [total]);

  return <BuyButton onClick={onBuyClick}/>;
}
```

这需要一点努力，但是现在我们有了一个解决引用完整性问题的好办法。现在，只有当`onBuyClick`的引用标识改变时，子元素才会重新呈现，而`onBuyClick`只有当它的依赖数组改变时才会改变。这是目前解决重新渲染问题的最好方法。**但并不完美。**

`onBuyClick`只有当它的依赖关系改变时才会改变，但如果它们经常改变呢？如果每次用户在购物篮中添加或删除东西时,`total`状态值都发生变化，那该怎么办？这意味着`onBuyClick`的参照完整性仍然会有很大的变化，因此 BuyButton 最终仍然会重新呈现很多。

哦不！看起来我们已经做了很多工作，但最终还是出现了几乎相同的问题！嗯……是的。
但是不用担心，因为 useEvent 可以解决这个问题！

使用 useEvent()，即使函数中使用的属性或状态发生变化，我们也可以保持相同的引用身份。

一旦函数被创建，它会给你一个相同的身份。你可以把它想象成一个更强大的 useCallback()。这是一个游戏规则的改变，当谈到整理子组件重新渲染优化。

## useEvent 实现看起来像什么？

useEvent()与 useCallback()非常相似，所以实现非常相似，只是 useEvent()没有依赖数组(这意味着没有额外的 deps 数组 lint 错误)。

```
export const Basket = () => {
  const [total, setTotal] = useState('');

  const onBuyClick = useEvent(() => {
    showTotal(total);
  });

  return <BuyButton onClick={onBuyClick}/>;
}
```

## 太好了，我等不及要用了！

我很高兴你能看到 useEvent()的价值，但很抱歉打破你的幻想，目前 React 的当前版本中不提供 useEvent()。
好消息是，该功能还不足以构成一个主要版本，并且将作为次要版本发布，但还没有确认何时发布，所以请保持警惕！

要阅读更多关于 useEvent 的内容，请访问 React GitHub 上的[官方 RFC。](https://github.com/reactjs/rfcs/blob/useevent/text/0000-useevent.md)

如果你喜欢这篇文章或者觉得它有用，那么欢迎关注。或者，你可以在这里的[](https://jamesmbrightman.medium.com/membership)**培养基上支持我，或者给我买一杯* [*咖啡*](https://ko-fi.com/jamesbrightman) *！非常感谢所有的支持。**

**更多内容请看**[***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****