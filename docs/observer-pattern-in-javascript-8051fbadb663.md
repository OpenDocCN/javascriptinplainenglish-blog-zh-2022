# JavaScript 中的观察者模式

> 原文：<https://javascript.plainenglish.io/observer-pattern-in-javascript-8051fbadb663?source=collection_archive---------5----------------------->

![T](img/97e826c971e9cf5664ff0bfa07877590.png)  T 他观察者模式被运用的情况比你可能想象的要多。你可能在不知道的情况下遇到了观察者模式，例如聊天应用、通知等。在本文中，我将向您展示什么是观察者模式以及它是如何工作的。

这是 JavaScript 设计模式系列文章的一部分。这里是我将要介绍的 JavaScript 中所有[设计模式的概述。](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

![](img/fdc046de60db9fd2d8a6ad27b9dab23b.png)

Photo by Daniel Lerman on Unsplash

观察者模式是一种设计模式，在这种模式中，一个对象(称为主题)维护一个依赖于它的对象(称为观察者)的列表，并自动通知它们任何状态变化，通常是通过调用它们的方法之一。这种模式允许对象之间相互通信，并对系统中的变化做出反应，而无需将它们紧密地耦合在一起。

在 JavaScript 中，可以使用 EventEmitter 类实现 observer 模式，该类允许对象订阅事件，并在事件发出时接收通知。当 subject 对象的状态改变时，它会发出事件，observer 对象会订阅这些事件，并根据需要对它们做出反应。

例如，假设您有一个用户帐户对象，它维护着用户的姓名、电子邮件地址和其他详细信息。如果您希望在用户名更改时得到通知，您可以订阅“nameChanged”事件，并提供一个回调函数，每当发出该事件时都会调用该函数。每当用户名改变时，用户帐户对象将发出该事件，并且您的回调函数将以新名称作为参数来执行。

下面是一个如何用 JavaScript 实现观察者模式的例子:

```
class Subject {
 constructor() {
 this.observers = [];
 }
subscribe(observer) {
 this.observers.push(observer);
 }
unsubscribe(observer) {
 this.observers = this.observers.filter(obs => obs !== observer);
 }
notify(data) {
 this.observers.forEach(observer => {
 observer.update(data);
 });
 }
}
class Observer {
 constructor(state) {
 this.state = state;
 }
update(data) {
 this.state = data;
 }
}
const subject = new Subject();
const observer1 = new Observer(1);
const observer2 = new Observer(2);
const observer3 = new Observer(3);
subject.subscribe(observer1);
subject.subscribe(observer2);
subject.subscribe(observer3);
subject.notify(4);
console.log(observer1.state); // 4
console.log(observer2.state); // 4
console.log(observer3.state); // 4
subject.unsubscribe(observer2);
subject.notify(5);
console.log(observer1.state); // 5
console.log(observer2.state); // 4
console.log(observer3.state); // 5
```

在这个例子中，Subject 类维护一个观察者列表，并提供订阅和取消订阅事件的方法。Observer 类有一个 state 属性，当它收到来自 subject 的通知时，可以更新该属性。

您可以使用 subscribe()方法向列表中添加新的观察者，使用 unsubscribe()方法删除它们。当对主题调用 notify()方法时，它将遍历它的观察器列表，并对每个观察器调用 update()方法，传入提供的任何数据。

观察者模式的优点包括:

*   它允许对象在没有紧密耦合的情况下相互通信，这可以使代码更加模块化，更易于维护。
*   这使得向系统添加新的观察者变得容易，因为他们可以简单地订阅他们感兴趣的事件，而不需要修改现有的代码。
*   它允许对象对系统中的变化作出反应，而不必知道这些变化是如何发生的细节或涉及到哪些其他对象。

观察者模式的缺点包括:

*   这会使代码变得更加复杂，因为可能有许多对象订阅和发出事件，这使得理解和调试代码变得困难。
*   如果有大量对象发出事件并对事件做出反应，会导致性能问题，因为这会导致系统中大量不必要的活动。
*   这使得确保系统正常工作变得困难，因为很难预测事件发出和处理的顺序。

观察者模式通常用于各种不同的场景，包括:

*   GUI 应用程序:在 GUI 应用程序中，观察者模式可用于允许用户界面的不同组件对事件(如按钮点击或数据更改)作出反应，而无需知道如何处理这些事件的细节。
*   联网:在联网应用程序中，观察者模式可用于允许不同的对象对网络连接的变化或从网络接收的数据做出反应，而无需知道网络通信是如何实现的细节。
*   游戏开发:在游戏中，观察者模式可用于允许不同的游戏对象对事件(如冲突或游戏状态的变化)做出反应，而不需要知道如何处理这些事件的细节。
*   异步编程:在异步程序中，观察者模式可用于允许代码的不同部分对长期运行任务的完成或新数据的可用性做出反应，而无需知道这些任务是如何实现的细节。

总的来说，观察者模式是一个有用的工具，用于解耦对象，并允许它们以灵活和动态的方式相互通信。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

请继续关注我，因为我将在接下来的文章中发布更多关于 JavaScript 设计模式的内容。这里是我将要介绍的 JavaScript 中所有[设计模式的概述。](https://pandaquests.medium.com/overview-of-design-patterns-in-javascript-27d14530397a)

你以前用过观察者模式吗？你遇到什么挑战了吗？你是怎么解决的？

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***