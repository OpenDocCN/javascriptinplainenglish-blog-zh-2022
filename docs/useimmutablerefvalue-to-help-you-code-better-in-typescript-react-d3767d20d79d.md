# 使用 ImmutableRefValue 帮助您在 TypeScript + React 中更好地编码

> 原文：<https://javascript.plainenglish.io/useimmutablerefvalue-to-help-you-code-better-in-typescript-react-d3767d20d79d?source=collection_archive---------8----------------------->

## 另一个抽象层次`useRef`

![](img/cc7bef6e2ab8aca2324683b84dc2e8e5.png)

Photo by [marina](https://unsplash.com/@marinajune?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 React 中，你可能经常使用`useRef`，它允许你引用渲染不需要的值。这很重要，例如，在一个组件中创建一个唯一的`VideoPlayer`。

```
function Component() {
  const playerRef = useRef(new VideoPlayer());
  // ...
```

但是请记住，`useRef`保存初始的`ref`值一次，并在下次渲染时忽略它。

对于上面的例子，组件初始化时调用`new VideoPlayer()`的结果会被存储在`ref`中，这没问题，但是注意下次渲染时`new VideoPlayer()`还是会被再次调用，只是其调用的结果不再被`useRef`接收。这意味着这是无效的浪费，如果您正在创建昂贵的对象，这很可能会影响您的应用程序的性能。

值得一提的是，`useState`钩子也有这种情况，但是它可以接收一个*初始化器*函数，并且在下一次渲染中不再调用它，就像这样:`const [player] = useState(() = > new VideoPlayer());`，但是这里`player`不是渲染所需要的值，所以还是用`useRef`比较好。

所以为了处理这种情况，我们可能需要在每个组件渲染中做出判断:

```
function Component() {
  const playerRef = useRef(null);
  if (playerRef.current === null) {
    playerRef.current = new VideoPlayer();
  }
  // ...
```

看起来不错，这个组件将只调用`new VideoPlayer()`一次，并生成一个惟一的实例存储在`playerRef`中。但是如果您正在使用 TypeScript，那么在访问`playerRef`时您将需要一个非空检查:

```
function Component() {
  const playerRef = useRef<VideoPlayer | null>(null);
  if (playerRef.current === null) {
    playerRef.current = new VideoPlayer();
  }

  const onClick = () => {
    // Error: Object is possibly 'null'.
    playerRef.current.play();
  };
}
```

您当然可以简单地通过使用可选的链接操作符`?.`来解决这个问题，就像这样:`playerRef.current?.play();`。如果是一个或者两个也没问题，但是如果`player`有很多可访问的属性和方法，这就需要你把它添加到你使用的每一个地方，这是多余的。

所以我们可以创建一个简单的函数来规避这个问题:

```
const getPlayer = () => {
  if (!playerRef.current) {
    playerRef.current = new VideoPlayer();
  }

  return playerRef.current;
};

getPlayer().play();
```

它工作得很好，但是如果您的 React 应用程序中有很多地方需要这样处理，那么最好抽象成一个自定义钩子:

使用它可以在类似的逻辑中获得唯一的不可变参考值:

```
function Component() {
  const player = useImmutableRefValue(() => new VideoPlayer());

  const onClick = () => {
    player.play();
  };
}
```

玩得开心！感谢阅读，下次再见，干杯🍻

*不是中等会员？* [*支持我在这里成为一个*](https://medium.com/@hellostephanie2022/membership) *。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***