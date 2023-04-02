# JavaScript 动画的运动成帧器

> 原文：<https://javascript.plainenglish.io/motion-framer-for-javascript-animation-e939aedf9a37?source=collection_archive---------8----------------------->

## 除了使用 CSS，您还可以使用 JavaScript 来触发和更新带有动画规范的动画。

![](img/25f29926815bfb975921262a004d97e8.png)

Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们使用 css 来制作动画，比如淡入淡出和滑动效果。然而，css 动画有一些限制:它不能给我们一个真正的动画师的颗粒级控制，类似于我们处理 css 其余部分的方式。我们不直接操作动画的开始和结束，因此当这些事件发生时，我们无法得到通知。

除了 css，我们可以看看另一种方法，Javascript 方式。

## 运动第一

任何动画背后都有一个数学形式的运动基本概念:

```
Motion speed = Travel distance / Travel time
```

跑步就是在一定的时间内跑一定的距离。如果我们用一个离散的单位来看时间，比如`30ms`，我们创造了一个计算机化的运动。在 Javascript 中，`30ms`不能是一个固定的常数，因为还有其他竞争消耗计算机的能力，比如浏览器服务等。所以我们求助于让动画足够“流畅”。

如果我们将距离抽象成任何元素量，如`width`、`color`等，它就变成了一个实用程序包，如[、**、【popmotion】、**、](https://github.com/Popmotion/popmotion)、**、**，其中**、**提供了一个函数`animate`将一个值从一个值传递到另一个值:

```
animate({
  from: 0,
  to: 100,
  onUpdate: latest => console.log(latest), 
  onPlay: () => {}, 
  onComplete: () => {} 
})
```

由于该库是为 DOM 元素定制的，为了便于使用，该值支持字符串类型:

```
animate({ from: "0px", to: "100px" })
```

把易用性放在一边，**这才是真正的动画师。**动画值实时变化。而且我们暴露了所有更新事件的接口，比如`onUpdate`、`onPlay`和`onComplete`。如果你想微调它，这是你进入动画的入口。

# 仅 Javascript

如果你还没有注意到的话，现在一切都与 javascript 有关。即使没有任何前端库，也可以将动画应用于任何 DOM 元素。但是为了快速进入主题，请原谅我使用 [**成帧器-运动**](https://github.com/framer/motion/tree/main/packages/framer-motion) ，一个派生的 React 版本来展示这种方法的一些特性。

```
const MyComponent = ({ opacity }) => {
  return <motion.div animate={{ opacity }}>Hello</motion.div>
)
```

该库允许您将任何 DOM 元素(如`div`)代理到一个新的 motion 元素`motion.div`，从而接受一个 prop `animate`。在上面的 my 组件中，它的不透明度可以根据从它的父组件传递来的内容进行动画处理。

听起来很简单，但你应该马上想到几个问题:

## 我如何触发动画

如何在 React 中触发状态变化？

```
const MyComponent = () => {
  const [opacity, setOpacity] = useState(0)
  useEffect(() => {
    setOpacity(1)
  }, [])
  ...
```

我们可以把它作为一种状态，而不是从道具中传递`opacity`,因此你可以在组件循环开始时触发动画。

## 我如何改变动画

这与上一个问题基本相同，基于任何事件，您都可以改变状态，从而使动画变形:

```
const MyComponent = () => {
  const [opacity, setOpacity] = useState(0)
  const onClick = () => {
    setOpacity(1)
  }
  ...
```

在任何时间点，无论是通过用户交互还是任何计划好的序列，只要状态`opacity`通过`setOpacity`被更新，你就可以期待一个屏幕渲染来适应新的动画需求。

## 我如何编码动画

这是一个非常宽泛和开放的问题。我想我的直觉是，你仍然像以前一样用同样的方式编码，使用组件，并在你适应的过程中重构组件:

```
const fadeTransition = (duration = 0.5, delay = 0.2) => ({
  animate: {
    opacity: 1,
    transition: {
      ease: 'easeInOut',
      duration,
      delay,
    },
  }, 
  ...
});
```

如果我们遵循一般的重构原则，一个有趣的片段会脱颖而出，它看起来有点像动画的规范。为了应用这个规范，我们可以用一个通用组件连接它，比如`Fade`:

```
const Fade = ({
  children,
  duration = 0.5,
  delay = 0.2,
  ...props
}: FadeProps) => {
  const variants = useMemo(() => {
    return **fadeTransition**(duration, delay);
  }, [delay, duration]);return (
    <motion.div
      variants={variants}
      **animate**="animate"
      {...props}
    >
      {children}
    </motion.div>
  );
};
```

现在，每当我们需要一种淡入淡出效果时，我们只需将它环绕起来即可:

```
<Fade delay={0.2}>
  ...
</Fade>
```

你可以看到，代码并不多，我们可能会用更少的代码向你展示，但我想用这种方式向你展示，以强调以下几点:

*   动画是组件的一部分，如果你愿意，你可以认为动画是另一个组件。
*   可以通过配置或规范来配置动画，这对于我们自己的目的来说是非常灵活的。
*   这种方法的一个副作用，*如果我们改变动画的细节，团队可以很容易地一起检查代码并做出改变。*

## 摘要

除了使用 css，您还可以使用 Javascript 来触发和更新带有动画规范的动画。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***