# 如何使用 Formik 以最佳方式处理 React 原生表单

> 原文：<https://javascript.plainenglish.io/react-native-forms-formik-the-best-way-step-by-step-3bde7d02ba4f?source=collection_archive---------4----------------------->

## 使用 Formik 处理 React 原生表单的分步指南。

![](img/fc147865f2505a4bc81ce75385254375.png)

表单不容易处理，尤其是当表单中有很多字段时。我们知道，表单中的每个字段都需要被跟踪，我们可以通过为每个字段设置`useState` hook 来实现。

## 例如:

```
const [username, setUsername] = useState<string>('');
//code line..
//code line..
const [address, setAddress] = useState<string>('');
```

**另一种处理表单域的方式**是使用`useReducer`来使它变得更简单。

## 例如:

```
const initialState = {
  username: "",
  address: "",
};function reducer(state, action) {
  switch (action.type) {
    case "setUsername":
      return { ...state, username: action.payload };
    case "setAddress":
      return { ...state, address: action.payload };
    default:
      throw new Error();
  }
}export const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);
  //...
};
```

上面的例子是处理表单字段状态的两种方法，正如你所看到的，如果有 2-5 个字段，这并不坏，但是如果表单中包含 10 个甚至 20 个字段呢？代码会越来越多，而且会很乱。

这里福米克可以帮忙！

# **步骤 1 —安装 Formik**

在我们开始之前，让我们通过下一个命令`npm i formik`先安装 **Formik** 。现在我们可以将 Formik 导入表单屏幕。它应该看起来像下面的例子:

```
import { Formik } from 'formik';export const MyForm = props => (
  <Formik>
    {()=>(
      //code line..
      //code line..
    )}
  </Formik>
);
```

正如你所看到的，在 **Formik** 标签中有一个 JavaScript 函数，这个函数将处理我们的表单元素，就像我们稍后看到的那样。

# 第 2 步— Formik 方法和道具

Formik 渲染方法和道具，例如:

*   **initialValues:** 您**必须用初始值初始化所有字段**，否则 React 将抛出一个错误，指出您已将输入从非受控更改为受控。
*   **onSubmit:** 您的表单提交处理程序。所有表单字段值将被传递给`onSubmit`函数。

```
<Formik
    initialValues={{ username: '', address: '' }}
    onSubmit={(values) => console.log(values)}
  >
    {() => (
      //code line..
      //code line..
    )}
  </Formik>
```

# 步骤 3—使用 Formik 创建表单

在 Formik 标记中，我们设置了一个 JavaScript 函数。这个函数的意义是返回表单元素，让我们创建一个简单的表单。

```
<Formik
  initialValues={{ email: '', username: '' }}
  onSubmit={values => console.log(values)}
>
  {() => (
    <View>
      <TextInput /> //This field for username.
      <TextInput /> //This field for address.
      <Button onPress={} title="Submit" /> //Button for Submit
    </View>
  )}
</Formik>
```

在上面的例子中，你可以看到`<View></View>`包含了我们的表单字段，一个是用户名的**字段，一个是地址**的**字段，此外，我们还有“提交”按钮来打印这些字段中的值。**

主要的两个问题是，我们如何连接和存储要在某个状态下保存的字段值，以及提交按钮如何打印出在该特定状态下保存的值。

# 步骤 4—用 Formik 连接表单

现在我们有了一个简单的表单，我们需要回答上面的两个问题，为此我们需要首先将表单连接到 Formik。我们的简单表单和 Formik 之间的连接是通过使用由`<Formik></Formik>`标签内的 **JavaScript 函数**接收的 **props** 来完成的。

这些道具内部包含一些属性，我们将在接下来的属性中使用这些属性: **handleChange** ， **handleSubmit** ， **values** 以尽可能保持简单。

**handleChange:** 该处理程序将通过将字段设置为 **onChangeText** 属性来处理字段中的更改，其值名类似于:`handleChange(‘username’)`。

**handleSubmit:** 这个处理程序会将所有的字段值传递给提交函数，这个函数在 Formik 标签处已经定义为`**onSubmit**` 。

**值:**这是一个对象，它包含了之前在 Formik 标签中定义的所有`**initialValues**` ，但是每次字段中的值被 **handleChange** 改变时，它都会被更新。

最终结果应该是这样的:

```
export const MyReactNativeForm = props => (
  <Formik
    initialValues={{ username: '', address = '' }}
    onSubmit={values => console.log(values)}
  >
    {({ handleChange, handleSubmit, values }) => (
      <View>
        <TextInput
          onChangeText={handleChange('username')}
          value={values.username}
        />
        <TextInput
          onChangeText={handleChange('address')}
          value={values.address}
        />
        <Button onPress={handleSubmit} title="Submit" />
      </View>
    )}
  </Formik>
);
```

现在我们已经将表单连接到 Formik，而不需要自己处理表单中每个字段的状态，我们可以根据需要继续添加越来越多的字段，并让 Formik 进行状态管理。

很棒吧？

**感谢您到目前为止的阅读，如果您喜欢这样的内容，并且您想支持我作为一名程序员和作家撰写更多这样的文章， [***请使用我的链接注册 Medium 成为会员(每月订阅 5 美元)，您将可以无限制地访问 Medium 上的所有内容。*T31**](https://medium.com/membership/@nissimzarur)**

*   如果你想了解 [***回调***](https://nissimzarur.medium.com/what-is-callbacks-how-it-works-in-javascript-step-by-step-real-life-example-425bc277893) 以及它在 JavaScript 中是如何工作的？ [***此处***](https://nissimzarur.medium.com/what-is-callbacks-how-it-works-in-javascript-step-by-step-real-life-example-425bc277893) 。
*   如果你想了解 [***范围***](https://towardsdev.com/4-types-of-javascript-scopes-all-you-need-to-know-about-207598da120e) 和每个范围之间的区别，你可以在这里 阅读它们。
*   如果你想学习关于 [***闭包***](https://nissimzarur.medium.com/what-is-closures-how-it-works-in-javascript-step-by-step-real-life-example-eb4a97c7120d) 以及它在 JavaScript 中如何工作的真实例子，你可以在这里阅读[](https://nissimzarur.medium.com/what-is-closures-how-it-works-in-javascript-step-by-step-real-life-example-eb4a97c7120d)*。*
*   *如果你想了解一下 [***箭头函数&常规函数***](https://nissimzarur.medium.com/javascript-arrow-function-vs-regular-function-whats-the-difference-fast-understanding-cda1a162a355) 的区别你可以在这里阅读一下[](https://nissimzarur.medium.com/javascript-arrow-function-vs-regular-function-whats-the-difference-fast-understanding-cda1a162a355)*。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***