# 反应中最常见的错误

> 原文：<https://javascript.plainenglish.io/the-most-common-mistake-in-react-144603145248?source=collection_archive---------3----------------------->

![](img/d224a6e901faaa470df717cce835dce5.png)

Photo by [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 React 应用程序中需要解决的最常见的问题之一是获取外部数据。一般来说，这是你要学习如何解决的第一个问题，但是大多数实现都犯了一个简单的错误，**更新一个卸载组件的状态**。

我们将从一个非常简单的例子开始，一个博客组件获取与文章相关的数据，在获取过程中显示加载消息，在出现错误时显示错误，在另一种情况下显示文章列表。

```
const Blog = () => {
  const [posts, setPosts] = useState([]);
  const [status, setStatus] = useState('idle');
  const [error, setStatus] = useState(null); useEffect(() => {
    const fetchData = async () => {
      setStatus('loading');
      try{
        setStatus('loading');
        const posts = await getAllPosts();
        setPosts(posts);
        setStatus('finished');
       } catch(e) {
         setStatus('error');
         setError(e);
       }
    } fetchData();
  }, []); if(status == 'error') return <p>Error while loading data</p>;
  if(status == 'loading') return <p>Loading...<p>;
  return <PostGrid posts={posts} />
};
```

这是可以的，在大多数情况下有效，但是存在一个问题…

`getAllPosts`函数是一个正在等待的异步函数，这个函数可能需要几秒钟才能返回，当它返回时，代码试图调用`setPosts`函数，但是当组件在此之前被卸载时会发生什么呢？。您会收到警告，因为您无法设置已卸载组件的状态。

```
const posts = await getAllPosts();
setPosts(posts);  **# Warning: Can't perform a React state update on an unmounted component.**
setStatus('finished');
```

**如何修复问题？**

关键是只有当组件被挂载时才设置状态，在这种情况下，你需要确保组件在`getAllPosts`被调用后被挂载。为此，我们将使用一个抽象机制的钩子来检查当前组件是否已安装。

```
const useIsMounted = () => {
  const isMounted = **React.useRef(false)**;     // **(1)** React.useEffect(() => {
    **isMounted.current = true;                // (2)**
    return **() => isMounted.current = false;**  // **(3)**
  }, **[]**);                                    // **(4)**
  return isMounted.current;
}
```

我们使用一个`useRef`钩子(1)，以确保当值`isMounted`改变时，使用它的组件中不会触发重新呈现器。之后，我们使用`useEffect`第一次渲染组件时，它将 ref 的值设置为`true` (2)，换句话说，当前组件现在被挂载。之后，`useEffect`钩子定义了一个清理函数(3)和一个空数组(4)作为依赖项，这意味着一旦组件被卸载，清理函数才会被触发。

现在，您可以将它与您的原始组件一起使用

```
const Blog = () => {
  const [posts, setPosts] = useState([]);
  const [status, setStatus] = useState('idle');
  const [error, setStatus] = useState(null);
 **const isMounted = useIsMounted();**useEffect(() => {
    const fetchData = async () => {
      setStatus('loading');
      try{
        const posts = await getAllPosts();
 **if(isMounted) {
          setPosts(posts);                    // 1
          setStatus('finished');
        }** } catch(e) {
          **if(isMounted) {
            setStatus('error');               // 2
            setError(e);
          }** }
    } fetchData();
  }, []); if(status == 'error') return <p>Error while loading data</p>;
  if(status == 'finished') return <PostList posts={posts} />
  return <p>Loading...<p>;
};
```

一个重要的注意事项是，您需要确保组件不仅在异步函数成功完成(1)时挂载，而且在它失败(2)时挂载，换句话说，在 catch 块中挂载。

## **结论**

试图更新一个卸载组件的状态是 react 应用中一个非常常见的问题，这个问题通常出现在你获取一些外部数据的时候，但是当你使用任何异步事件来触发完成后状态的一些变化的时候，同样的问题也会出现。

# 感谢阅读！

这就是这篇帖子的全部内容，希望内容已经合你意，下期见。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*