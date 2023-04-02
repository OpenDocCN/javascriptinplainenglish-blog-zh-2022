# 反应状态

> 原文：<https://javascript.plainenglish.io/state-in-reactjs-a8392a7bbcb3?source=collection_archive---------9----------------------->

![W](img/d891666cc9ebd9231a574f9c9cb6a45e.png)  W 欢迎来到 React state 的奇妙世界！起初，这可能看起来令人生畏，但不要担心，我们会握住您的手，引导您通过组件通信的神奇土地。相信我们，这其实很容易理解。所以，拿起一杯咖啡(或一杯葡萄酒，这里没有判断)，让我们开始掌握 React 的艺术状态！

![](img/bd1ce46ffb349ce5ccacc65b2764e267.png)

Photo by [Randy Tarampi](https://unsplash.com/@randytarampi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ReactJS 中的状态是组件在内部存储和管理信息的一种方式。它就像一个组件的“内存”，允许它记住并跟踪某些值或数据。

例如，假设您有一个表示购物车的组件。该组件的状态可能包括关于已经添加到购物车中的商品的信息、这些商品的总成本以及购物车当前是打开还是关闭。

下面是一些演示如何在 React 组件中使用状态的代码:

```
class ShoppingCart extends React.Component {
 constructor(props) {
 super(props);
 this.state = {
 items: [],
 totalCost: 0,
 isOpen: false
 };
 }
addItem(item) {
 this.setState(prevState => {
 return {
 items: […prevState.items, item],
 totalCost: prevState.totalCost + item.price
 }
 });
 }
toggleCart() {
 this.setState(prevState => {
 return { isOpen: !prevState.isOpen }
 });
 }
render() {
 return (
 <div>
 <button onClick={this.toggleCart}>
 {this.state.isOpen ? 'Close' : 'Open'} Cart
 </button>
 {this.state.isOpen &&
 <div>
 {this.state.items.map(item => (
 <p key={item.id}>{item.name} - ${item.price}</p>
 ))}
 <p>Total: ${this.state.totalCost}</p>
 </div>
 }
 </div>
 );
 }
}
```

在本例中，ShoppingCart 组件有三种状态:items、totalCost 和 isOpen。每当调用 addItem 方法时，就会更新 items 和 totalCost 值，并且当调用 toggleCart 方法时，会切换 isOpen 值。该组件还有一个按钮，允许用户打开或关闭购物车，只有当 isOpen 值为 true 时，才会显示购物车。

*   在 ReactJS 中使用状态的主要优点是，它允许组件在内部存储和管理信息，而不是依赖于 props (props 是从其父组件传递给组件的数据)。这使得构建可重用和自包含的组件变得更加容易，因为它们可以管理自己的数据和行为，而不依赖于其父组件的数据和行为。
*   状态的另一个优点是它允许组件响应用户动作和事件，比如点击、表单提交和悬停事件。这使得构建能够根据用户输入改变和更新的交互式动态用户界面成为可能。
*   此外，通过允许组件仅在必要时重新呈现，而不是每次父组件更新时都重新呈现，状态可以提高 React 应用程序的性能。这有助于减少不必要的重新渲染次数，并提高应用程序的整体性能。
*   最后，state 可以使 React 应用程序的调试和故障排除变得更加容易，因为它允许您跟踪各个组件的数据和行为，而不是试图一次调试整个应用程序。

总的来说，状态是构建 React 应用程序的重要组成部分，它提供了许多好处，使构建可重用、交互式和高性能的组件变得更加容易。

*   在 ReactJS 中使用状态的一个潜在缺点是，它会使组件更加复杂，因为它要求组件在内部管理自己的数据和行为。这使得理解和维护组件变得更加困难，特别是当它有很多状态或者状态以复杂的方式使用时。
*   另一个潜在的缺点是，state 会使测试 React 组件变得更加困难，因为除了它的属性和呈现的输出之外，它还要求您考虑组件的内部状态。这使得为使用状态的组件编写和维护测试用例更加耗时。
*   此外，状态会使推理组件的行为变得更加困难，因为它会受到各种内部和外部因素的影响。这使得预测组件在不同情况下的行为变得更加困难，从而使调试和解决出现的问题变得更加困难。
*   最后，状态会使构建可伸缩和可维护的 React 应用程序变得更加困难，因为它会导致组件之间的紧密耦合，并使它们之间共享数据和行为变得更加困难。随着时间的推移，这使得更改和更新应用程序变得更加困难，因为这可能需要您更新依赖于共享状态的多个组件。

ReactJS 中的状态是构建 React 应用程序的一个重要部分，但是它也会带来一些您应该知道的挑战和复杂性。为了构建可维护和可伸缩的应用程序，明智地使用状态并且只在必要时使用是很重要的。

ReactJS 中的状态有许多用例，因为它允许组件在内部存储和管理信息。下面是一些如何在 React 应用程序中使用状态的示例:

*   存储表单输入:状态可用于存储表单字段和输入元素的值，允许组件跟踪用户输入并响应更改。
*   管理应用程序状态:状态可用于存储和管理全局应用程序状态，例如当前登录的用户、当前页面或选定的主题。
*   显示数据:状态可用于存储和显示从外部 API 或数据库获取的数据，允许组件向用户显示动态和最新的信息。
*   处理用户交互:状态可用于跟踪和响应用户交互，如点击、悬停事件和表单提交。
*   提高性能:状态可用于控制组件何时重新呈现，从而避免不必要的重新呈现并提高应用程序的性能。
*   调试和故障排除:通过允许您跟踪各个组件的数据和行为，State 可以使 React 应用程序的调试和故障排除变得更加容易。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

这就是我们对 ReactJS 国家世界的一个总结！我们希望本教程对您有所帮助，并且您现在对状态如何在 React 中工作有了更好的理解。

如果你喜欢这篇文章，请在评论中告诉我们，并考虑关注我们，以获得更多关于 ReactJS 和其他 web 开发主题的精彩内容。敬请关注——这只是我们关于 ReactJS 的[系列的开始，所以请务必关注更多的文章。](https://pandaquests.medium.com/core-concepts-in-reactjs-for-beginners-a0bffaba49ce)

感谢阅读！再见

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*