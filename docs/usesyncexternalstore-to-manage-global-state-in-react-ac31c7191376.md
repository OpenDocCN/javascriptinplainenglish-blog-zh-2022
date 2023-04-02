# 使用 SyncExternalStore 管理 React 中的全局状态

> 原文：<https://javascript.plainenglish.io/usesyncexternalstore-to-manage-global-state-in-react-ac31c7191376?source=collection_archive---------7----------------------->

![](img/174fa017adcb1826bd20d9002936a003.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都知道 React 希望我们如何管理状态，主要是通过*钩子*。我写了一本关于它的书[以正确的方式设计 React 钩子](https://www.amazon.com/Designing-React-Hooks-Right-Way-dp-1803235950/dp/1803235950/ref=mt_other?_encoding=UTF8&me=&qid=1640158953)，在那里你可以找到很多使用钩子来保存组件渲染数据的例子。坦率地说， *React* 都是关于使用局部状态驱动组件渲染的。

尽管我很喜欢本地状态管理，但在某些情况下，尤其是在与捆绑了外部数据存储的第三方集成时，我们希望第三方在外部数据发生变化时通知 *React* 。

让我们来看看最近推出的 [React 18](https://thisweekinreact.com/articles/useSyncExternalStore-the-underrated-react-api) 钩子`useSyncExternalStore`是如何做到这一点的。假设我们有客房服务，每当有新客人出现，我们都要为他登记一个房间。如果有任何房间活动，他会得到通知。以下是图书馆代码:

```
let occupied = []
const list = []

function checkIn(room) { 
  occupied = [...occupied, room]
  notify()
}

function checkOut(room) { 
  occupied = occupied.filter(r => r !== room)
  notify()
}

function notify() {
  list.forEach(cb => {
    cb()
  })
}

export function subscribe(callback) {
  list.push(callback)
  ...
}

export function getOccupied() {
  return occupied
}
```

客房服务是建立在一个`occupied`数组之上的，这个数组记录了已入住房间的列表。最重要的是，它使用了一个订阅`list`，所以我们可以使用`subscribe`来添加一个`callback`功能，以防任何`checkIn`和`checkOut`活动发生，所有的听众都可以立即得到通知。

*注意:* `*subscribe*` *和* `*getOccupied*` *都是从库的接口导出的，所以它们是公共的消费者方法。*

## 什么是 useSyncExternalStore？

现在在 *React* 内部，我们想要使用这个库，比如`checkIn`和`checkOut`，此外我们想要它，以便每当房间可用性发生变化时，组件可以反映这种变化。

下面是`useSyncExternalStore`钩子的定义:

```
function useSyncExternalStore<Snapshot>(
  subscribe: (onStoreChange: () => void) => () => void,
  getSnapshot: () => Snapshot
): Snapshot;
```

钩子将两个函数`subscribe`和`getSnapshot`作为输入，返回`Snapshot`状态。这有点复杂。让我们将客房服务插入其中，看看它实际上是如何工作的:

```
const App = () => {
  const occupied = useSyncExternalStore(subscribe, getOccupied)
  ...
}
```

第一个参数是一个`subscribe`函数，它的唯一目的是允许我们的钩子通过回调来监听房间服务的变化。你可能想知道为什么我们看不到`callback`出现在界面的任何地方。这是因为这个回调变量是在初始化时在`useSyncExternalStore`钩子内创建的，并且将在订阅过程中被发送给`subscribe`。我们的工作是确保客房服务确实实现了这个接受`callback`作为输入的`subscribe`函数。完成所有这些设置后，从现在开始，客房服务应该与 *React* 组件连接。

第二个参数是一个`getSnapshot`函数，在我们的例子中，它返回`occupied`状态。如果从函数返回的状态发生变化，`App`组件将像*反应*一样尝试重新渲染。我们这些来自 *Redux* 的人可以把这个函数和`selector`函数联系起来。这里的想法是相似的。

钩子函数以第二个函数`getOccupied`给出的格式返回状态`occupied`。您可以将这个状态与`App`中 UI 的其余部分连接起来。

就是这样。你可能会想，这个钩子什么时候能派上用场？我猜想任何支持订阅模型的库在这里都是很好的候选，比如`window.addEventListener`。

## 与`useState`的区别

让我们快速比较一下这个吓人的`useSyncExternalStore`和常见的`useState`:

*   `useState`定义一个本地状态
*   `useSyncExternalStore`基于全局状态导出局部状态

相似之处在于两个钩子都定义了本地状态，而关键的不同之处在于，由于`useSyncExternalStore`所基于的服务是一个**全局**服务，很可能该服务甚至在我们进入`App`组件之前就已经被初始化了。在此之后，服务可以被任何其他组件调用，甚至可以在任何时候在 *React* 之外调用，因此理论上可以有很多东西与 *React* 代码一起进行。只有当服务生成一个**新的** `Snapshot`(可能在 *React* 之外)时，钩子才会得到一个新状态的通知，从而进入常规的 *React* 渲染周期。

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*