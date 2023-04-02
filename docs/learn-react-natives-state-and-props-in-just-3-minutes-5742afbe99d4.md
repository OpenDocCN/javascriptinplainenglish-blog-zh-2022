# 在 5 分钟内学会反应当地人的状态和道具

> 原文：<https://javascript.plainenglish.io/learn-react-natives-state-and-props-in-just-3-minutes-5742afbe99d4?source=collection_archive---------20----------------------->

## React Native 状态和道具初学者指南:学习何时使用它们。

![](img/26678728c199d4d688401cb656e57715.png)

Photo by [Lautaro Andreani](https://unsplash.com/es/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React Native 是一个 JavaScript 框架，用于构建高质量的本地应用程序，可以在 iOS 和 Android 上运行。

在 React Native 中，我们使用可组合的模块化组件来构建应用程序。为了使这些组件可操作，我们必须使用`state`和`props`。

如果你是开始学习 React/React Native 的人，你将需要了解基本的机制:状态和道具。

所以，让我们开始吧！

# **道具**

Props 是属性的简称，与 CSS 中的 ***属性*** 相同。你可以把道具想象成 ***一个可以倒果汁、水或者其他任何东西的杯子*** 。

![](img/1e5195ab8d0a7c7a59c6286e8dcc7b1c.png)

Photo by [NordWood Themes](https://unsplash.com/@nordwood?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

道具的主要特征:

1.  这些是**不可改变的**，这意味着**不可改变的**。(就像我们不能改变杯子的大小一样)。
2.  它们通过**进入组件**。

# **状态**

我们使用状态来处理组件内部的状态。它作为 CSS 中属性 的 ***值。用上面的例子来说，状态就是你倒进杯子里的东西。***

![](img/3fe84d64eb6be957841146a90e7581cd.png)

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

国家的主要特征:

1.  它们是**可变的**，意思是**可变的**。(你可以往杯子里倒咖啡或水或其他任何东西。)
2.  它们在组件中被处理**。**

好吧！我希望你能比以前更好地理解属性和道具。所以，让我们写一个简单的程序。

首先，我们将使用自己的代码替换默认的 App.js，该代码包含一个文本和文本输入框。

```
import * as React from 'react';import { Text, View, StyleSheet, TextInput } from 'react-native';export default class App extends React.Component {render() {let { container, textInputStyle, paragraph} = styles;return (<View style={container}><Text style={paragraph}>Stats and Props Testing</Text><TextInput style = {textInputStyle} placeholder = 'to test props!'/></View>);
}
}
const styles = StyleSheet.create({container: {flex: 1,justifyContent: 'center',paddingTop: Constants.statusBarHeight,backgroundColor: '#ecf0f1',padding: 8,},
textInputStyle: {width: 200,height: 50,backgroundColor: '#eaeaea',textAlign: 'center',alignSelf: 'center',marginTop: 10,borderRadius: 5,},paragraph: {margin: 24,fontSize: 18,fontWeight: 'bold',textAlign: 'center',},});
```

然后，我们将在组件文件夹中创建一个名为`component1.js` 的新组件。

```
import React from 'react';import { StyleSheet, Text, View } from 'react-native';export default class Component1 extends React.Component {render() {return (<View style={styles.container}><Text> {this.props.inputText}</Text></View>);
}
}const styles = StyleSheet.create({container: {backgroundColor: '#fff',alignItems: 'center',justifyContent: 'center',},});
```

在这个组件中，我们创建了 inputText props，然后我们将把它传递给`App.js`组件。

```
import Component1 from './components/component1';
```

然后在正文下面插入这个`Component1` 。

```
<Text style={paragraph}>Stats and Props Testing</Text><Component1 inputText={text}/>
```

这里我们将开始使用`state`。所以，我们将开始在我们的 App.js 中创建`Constructor`。

```
constructor(props){super(props);this.state= {text: 'State Testing'}
```

然后我们将在 render 语句中声明一个新变量。

```
let { text } = this.state;
```

然后，我们必须使用 onChangeText 属性在文本组件中显示输入的单词。

```
<TextInput style = {textInputStyle} placeholder = 'to test props!' value= {text} onChangeText= {this.handleChangeText} />
```

我们将在`handleChangeText`函数中处理状态的所有变化。

```
handleChangeText = (text) => {this.setState({text: text})}
```

以下是 App.js 文件的完整代码:

```
import * as React from 'react';import { Text, View, StyleSheet, TextInput } from 'react-native';import Component1 from './components/component1';export default class App extends React.Component {constructor(props){super(props);this.state= {text: 'State Testing'}}handleChangeText = (text) => {this.setState({text: text})}render() {let { container, textInputStyle, paragraph} = styles;let { text } = this.state;return (<View style={container}><Text style={paragraph}>Stats and Props Testing</Text><Component1 inputText={text}/><TextInput style = {textInputStyle} placeholder = 'to test props!' value= {text} onChangeText= {this.handleChangeText} /></View>);}}const styles = StyleSheet.create({container: {flex: 1,justifyContent: 'center',paddingTop: Constants.statusBarHeight,backgroundColor: '#ecf0f1',padding: 8,},textInputStyle: {width: 200,height: 50,backgroundColor: '#eaeaea',textAlign: 'center',alignSelf: 'center',marginTop: 10,borderRadius: 5,},paragraph: {margin: 24,fontSize: 18,fontWeight: 'bold',textAlign: 'center',},});
```

如果您运行这个项目，您将看到您键入的所有单词都显示在上面的文本位置。

本文到此为止。希望你现在多了解一下状态和道具。

我将在接下来的文章中写更多关于 React Native 的内容，这样你就可以关注我阅读更多内容。

感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*