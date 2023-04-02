# React 本机高阶组件与 Utils 函数:何时使用每种方法？

> 原文：<https://javascript.plainenglish.io/higher-order-components-vs-utils-functions-react-native-when-to-use-each-approach-8c2063ff3914?source=collection_archive---------13----------------------->

## 解释如何以及何时使用 React 本机高阶组件

![](img/cf0474a39f2b0edd338cd0fa0a75730a.png)

When To Use Each Approach?

经常有人问我什么时候使用 HOC ( [高阶组件](https://reactjs.org/docs/higher-order-components.html))以及什么时候使用通常在具有以下名称的文件中找到的常用函数:

*   Helpers.js
*   Commons.js
*   Utils.js 等等。

我决定把这个主题讲清楚，并解释如何以及何时以最正确的方式使用每种方法。所以就跟着走吧。

# 什么是反应高阶组件？

*高阶分量(HOC)是取一个分量并返回一个分量的函数。*

具体来说，**高阶分量是取一个分量并返回一个新分量的函数。**

# HOCs 解决什么问题？

让我们不要兜圈子，问一个主要问题，hoc 解决的问题是什么？我们为什么需要它？

**简单的**答案是干，你问什么是干？干是一个原则，意思是“不要重复自己”。
在我的职业生涯中，我已经在多种编程语言中使用了 DRY 原则，业内专家也一直建议我这样做。

比如 API 调用，复杂函数等等。

所以，是的，在某些情况下，您可以使用 Utils 函数来这样做，但是 hoc 是另一种可能来做同样的事情，甚至更多。通过使用 hoc，您可以共享公共功能，而无需重复相同的代码。

**高级**答案是不止这些。例如，使用 HOCs，我们可以在原始组件旁边添加另一个组件，并创建一个包含这两个组件的新组件。

我将在下一个问题中解释，如果我们希望在通过 API 请求获取数据的同时显示一个加载器，该怎么办？

从这个问题可以感受到 HOC 的强大。

# 通过例子学习

假设我们有以下组件。

```
function ListOfUsers = ()=> {
  const [users, setUsers] = useState([]);
  const [isLoading, setIsLoading] = useState(false);useEffect(()=>{
  (
    async ()=>{
      setIsLoading(true);
      const users = 
         await axios.get(GET_USERS_URL.then(results => results);
      setUsers(users);
      setIsLoading(false);
    }
  )();
  },[])render(
  <View>
    <Loader isLoading={isLoading}/>
    users.length ?
      users.map((user) => <UserCard user={user}/>) :
      <Text>No users</Text>
  </View>
  )
}
export default ListOfUsers;
```

现在，我们想要实现特定的方法。这里我们可以注意到两件事:

*   我们发出一个调用请求，从服务器获取所有用户。
*   我们正在使用`Loader`组件。

在这个例子中，我们可以将 API 请求和`Loader`组件从`ListOfUsers`组件中取出，并将它们移动到 HOC 中，这一步将使它们可以在下一次获取调用中重用。

# 特别创作

现在，让我们创建特设。用前缀“with”来调用 HOC 是可以接受的，就像我们的例子中的“withAxiosRequest”。

该文件可以创建在。/hoc/withAxiosRequest。

```
const withAxiosRequest = (OriginalComponent) => {
  return class extends React.Component {

    state = { isLoading: false};    createRequest = async (params: {url:string}) => {
      try {
        this.setState({ ...this.state, isLoading: true });        response = await axios.get(params.url).then((res) => res);        this.setState({...this.state, isLoading: false});
       return response;
      } catch (error) {
        this.setState({ ...this.state, isLoading: false });
        return false;
    }
  }  render() {
    return (
    <>
      <Loader isLoading={this.state.isLoading} />
      <OriginalComponent {...this.props}
       createRequest = {this.createRequest}
      />
    </>)
  }
 }
}export default withAxiosRequest;
```

自组织网络接收原始组件，并发回具有更多功能的新组件。

该功能是可重用的`createRequest`功能。现在，每当我们用`withAxiosRequest` HOC 封装一个组件时，我们可以使用`createRequest`函数。

被包装的组件现在包含了`Loader`组件，所以任何带有`createRequest`的获取调用都会自动激活`Loader`组件。

**注意:**这个例子只让您获取数据，您可以改进这个概念来支持 POST、DELETE、PUT 等等。

# 最后一步

最后一步是用`withAxiosRequest` HOC 包装我们的`ListOfUsers`组件。

```
function ListOfUsers = ({createRequest})=> {
  const [users, setUsers] = useState([]);useEffect(()=>{
  (
    async ()=>{
      const users = await createRequest({url:GET_USERS_URL});
      setUsers(users);
    }
  )();
  },[])render(
  <View>
    users.length ?
      users.map((user) => <UserCard user={user}/>) :
      <Text>No users</Text>
  </View>
  )
}
export default withAxiosRequest(ListOfUsers);
```

如您所见，我们可以在`ListOfUsers`组件中接收函数`createRequest`作为道具，因此我们不再需要`ListOfUsers`组件中的 axios 请求。

默认情况下，我们包装的组件现在包含了`Loader`组件，所以我们不再需要`ListOfUsers`组件中的`Loader`组件。

# 结论

在这个例子中，我们看到了 HOC 通过使用`createRequest`函数使我们的代码更短和可重用的能力，以及在我们选择包含的每个组件中包含`Loader`组件的能力。

高阶组件使您的代码更加抽象，一旦您掌握了它，您可能会过于频繁地使用这种模式。

**感谢您迄今为止的阅读，**如果您喜欢这样的内容，并且您想支持我作为一名程序员和作家撰写更多这样的文章， [***请使用我的链接注册 Medium 成为会员(每月订阅 5 美元)，您将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

请继续关注更多 React 本地示例和技巧。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*