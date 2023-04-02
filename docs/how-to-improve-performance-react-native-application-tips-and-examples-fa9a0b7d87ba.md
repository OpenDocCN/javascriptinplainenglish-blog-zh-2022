# 如何提高 React 本机应用程序的性能

> 原文：<https://javascript.plainenglish.io/how-to-improve-performance-react-native-application-tips-and-examples-fa9a0b7d87ba?source=collection_archive---------7----------------------->

## 提高 React 本机应用程序性能的提示和示例。

![](img/9339bb8d7561c5914d3cd58eebc118ae.png)

# 缓存图像

在 React Native 中，我们将“图像”作为核心组件。我们可以使用这个组件来显示图像，但是它有一些问题，比如:

*   忽明忽暗。
*   缓存未命中。
*   从缓存进行低性能加载。
*   总体表现不佳。

所有这些都会损害用户体验。对于这些情况，我们可以从“react-native-fast-image”中得到帮助。这个库可以跨平台使用，它像魔术一样工作。

**注意:**您必须使用 React Native 0.60.0 或更高版本才能使用 react-native-fast-image 的最新版本。

## 例子

步骤 1:安装库。

```
yarn add react-native-fast-image
cd ios && pod install
```

步骤 2:导入并使用库。

```
import FastImage from 'react-native-fast-image'const YourImage = () => (
    <FastImage
        style={{ width: 200, height: 200 }}
        source={{
            uri: 'https://unsplash.it/400/400?image=1',
            headers: { Authorization: 'someAuthToken' },
            priority: FastImage.priority.normal,
        }}
        resizeMode={FastImage.resizeMode.contain}
    />
)
```

更多例子可以在 [*这里*](https://github.com/DylanVann/react-native-fast-image) 找到。

# 记忆值

当屏幕频繁渲染时，使用`useMemo`可以优化您的 react 原生应用程序。

`useMemo`将记忆变量值，并且仅当其中一个依赖关系发生变化时才重新计算该值。因此，这种优化有助于避免每次渲染时进行昂贵的计算。`useMemo`接受 2 个参数:

*   memoized 函数将返回值。
*   一组依赖关系。

## 例子

```
const computeExpensiveValue = (a, b)=>{
  let total = 0;
  for(index=0; index<10000000; index++){
    total += index+a+b;
  }
  return total;
}const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

正如我们在上面的例子中看到的，我们将使用变量“a”和“b”计算索引 10000000 次。请注意，没有`useMemo`优化的帮助，我们将为每个渲染计算相同的值，这可能会降低您的 React 本机应用程序的速度。使用`useMemo`将确保我们不会为每个屏幕渲染一遍又一遍地计算相同的值，并且只有当影响最终结果的依赖关系之一被改变时。

# 记忆式回调

和`useMemo`一样，`useCallback`可以在屏幕频繁渲染的情况下优化你的 react 原生 app。`useCallback`将返回回调的记忆版本。`useCallback`接受 2 个参数:

*   要记忆的功能。
*   一组依赖关系。

## 例子

```
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b]
);
```

正如我们在上面的例子中看到的，我们传递了一个接受两个参数“a”和“b”的内联函数`doSomething`。这些参数意味着我们必须包含这些参数作为依赖项数组。通过在`useCallback`中使用，我们确保如果“a”和“b”没有改变，我们不会为每个渲染创建相同的函数。

`useCallback`将返回回调的记忆化版本，该版本仅在其中一个依赖关系发生变化时才会发生变化。

# 避免箭头功能

箭头函数是无效重渲染的常见问题。避免在呈现屏幕的函数中使用箭头函数作为回调函数。

为什么？

因为每当父元素重新呈现一个新的引用时，函数就会被重新创建。使用箭头函数方法将导致每次渲染都生成该特定函数的新实例，因此，React Native 将无法重用旧引用。

## 避免这种情况—例如

```
class AvoidCase extends React.Component {
  // ...
  addTodo() {
    // ...
  }
  render() {
    return (
      <View>
        <TouchableHighlight onPress={() => this.addTodo()} />
      </View>
    );
  }
}
```

## 正确案例—示例

```
class CorrectCase extends React.Component {
  // ...
  addTodo = () => {
    // ...
  }
  render() {
    return (
      <View>
        <TouchableHighlight onPress={this.addTodo} />
      </View>
    );
  }
```

**感谢**到目前为止的阅读，如果你喜欢这样的内容，并且你想支持我作为一个程序员和作家写更多像这样的文章， [***请用我的链接注册成为 Medium 的会员(5 美元/月订阅)，你将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

请继续关注更多 React 本机优化示例和技巧。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***