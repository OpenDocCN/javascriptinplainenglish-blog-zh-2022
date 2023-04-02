# 高级 React Native:use effect 清理功能如何工作

> 原文：<https://javascript.plainenglish.io/how-useeffect-cleanup-function-works-advanced-react-native-7b38c8b0efa1?source=collection_archive---------3----------------------->

## 用一个真实的例子解释 useEffect 清理函数是如何工作的。

这个主题对于 React Native 或 React 开发人员来说非常重要，但最近我看到相当多的 React 开发人员没有使用`useEffect` hook 中称为 cleanup function 的奇妙功能，所以我决定写一篇关于这个的帖子，并向我的朋友们展示一个真实的例子。

![](img/048eafe2eeadae969b6ef139fdbd4d26.png)

## 介绍

本文面向对`useEffect`钩子函数有基本了解的开发人员。

React 允许我们在组件挂载时或者在组件更新时通过使用带有依赖关系数组的`useEffect`钩子来创建动作。

它需要两个参数。第一个参数是一个函数。第二个参数是依赖项数组。如果任何依赖关系改变，那么效果将再次运行。

```
//Run after component mounted/first rendered.
useEffect(()=>{},[])//Run after dep1 or dep2 change/updated.
useEffect(()=>{},[dep1, dep2])
```

`useEffect`函数还有一个职责，这是在组件被卸载后运行的清理函数。

```
//Run after component is unmounted/removed
useEffect(()=>{
  return ()=>{}
},[])
```

## 为什么要使用清理功能

这是我们在使用它之前需要问自己的主要问题，因为我们需要知道它的确切目的。

`useEffect`为我们提供的这个清理功能是为了让我们清理或删除当组件被卸载或不再显示时不相关的任何进程或动作。

卸载组件后运行的操作示例。

```
//When the component will unmounted,
//The console will print "Component unmounted"useEffect(()=> {
  **return** ()=> {
    console.log("Component unmounted");
  }
},[])
```

**真实世界的例子**

我将用一个真实的例子来说明清理功能的重要性，它可以防止内存泄漏和性能下降。

假设我们有一个应用程序，我们想向其中添加一个新组件，该组件用 3 个点显示加载文本，一个接一个地构建这些点，直到我们收到来自服务器的响应。

例如:

**加载**1 秒后->**加载。**" 1 秒后- > " **加载..**" 1 秒后- > " **加载...**"等等，直到我们收到 API 请求的响应。

## 加载组件

这个组件将包含带有清理功能的`useEffect`钩子，让我们来构建这个组件。

```
const Loading = ()=> {
  const [dots, setDots] = useState<string>(".");
  const dotsLoading = () => {
    setDots((state)=>(state.length === 3 ? '' : `${state}.`));
  };useEffect(() => {
    //1000 ms = 1 sec
    const 1Sec = 1000;
    const **intervalId** = setInterval(dotsLoading, 1Sec);
    return () => **clearInterval(intervalId)**;
  }, []);return (
    <View style={Styles.modal}>
      <Text>Loading{dots}</Text>
    </View>
  )
}
```

这个`Loading`组件现在可以包含在任何发出 API 请求的屏幕组件中，并在它从/向服务器获取/发送数据时显示这个`Loading`组件。

## 屏幕组件

这个`Screen`组件将包含一个 API 请求，用于在我们等待从服务器接收数据时显示加载组件。

让我们来构建组件。

```
import Loading from "./components/Loading;
import { fetchData } from "./API;const Screen = ()=> {
  const [isLoading, setIsLoading] = useState<boolean>(false); useEffect(()=>{
    **setIsLoading**(true);
    (
      async ()=>{
        const result = await fetchData();
        **setIsLoading**(false);
      }
    )();
  },[])return (
    <View>
      {**isLoading** && <Loading />}
    </View>
  )
}
```

如你所见，我们有`Screen`组件，它在挂载时用`useEffect`中的`fetchData`函数创建一个 API 请求。

一开始，我们使`Loading`组件可见，现在`Loading`组件显示，直到我们从服务器接收数据，此外，**异步**函数是**以等待**对`fetchData`函数的响应。

当`isLoading`参数为假时，运行`Loading`组件内的清除功能，清除间隔并停止循环。通过这样做，即使我们不再使用`Loading`组件(当我们收到来自 API 请求的数据时),我们也能保护我们的应用程序不运行`dotsLoading`函数。

## 最后

`useEffect`的清理功能非常强大，如果我们很好地理解了它，我们就可以将我们的应用程序从糟糕的性能和内存泄漏中拯救出来。

感谢您到目前为止的阅读，如果您喜欢这样的内容，并且您想支持我作为一名程序员和作家来撰写更多这样的文章， [***请使用我的链接注册 Medium 成为会员(每月订阅 5 美元)，您将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。**