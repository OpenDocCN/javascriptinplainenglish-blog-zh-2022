# React-Redux 简单易用

> 原文：<https://javascript.plainenglish.io/react-redux-simple-way-to-use-fb57cf0983ee?source=collection_archive---------8----------------------->

## 用一个简单的例子说明使用 **Redux 的最简单方法。**

![](img/90729ba5393417eebdadaf82f7748283.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好，

今天我来告诉你使用 **Redux** 最简单的方法。我没有给出复杂的例子，而是准备了一个简单而恰当的例子。

希望对刚接触 **Redux** 的人，很久没有重复的人，以及在使用 **Redux** 的时候*相当迷茫*的人有一个说明性的例子。

该实例由两个按钮及其`onClick()`事件组成。

## 那么为什么是 Redux 呢？

你可以在许多文章中找到对此的解释，但我不会详细告诉你。你可以从这些文章中学到“什么是 Redux，什么是 payload，什么是 state……”。

我们将使用几种方法在页面之间传输数据。我们可以使用**道具**，但是随着子页面的增加，这种方法*会杀死我们*。我们可以使用**上下文**，但我不知道它们在非常大的项目中会有多有效。这里，Redux 来帮助我们了。

**第一步**

按照这些步骤创建 react 应用程序

**第二步**

安装 Redux 库

```
npm install @reduxjs/toolkit
npm install react-redux
npm install redux
npm install redux-persist
```

```
yarn add @redux/toolkit
yarn add react-redux
yarn add redux
yarn add redux-persist
```

**第三步**

创建一个**存储**目录`./store`

创建`index.ts`文件。您的索引文件可以是这样的:

```
const rootReducer = combineReducers({
  language: LanguageSlice,
});
```

`rootReducer`是捧我们的切片。如果你有不止一个，你可以这样写:

```
const rootReducer = combineReducers({
  language: LanguageSlice,
  users: UserSlice,
  books: BookSlice
  ...
});
```

**第四步**

在商店目录中创建语言目录:`store/language`

在语言目录下创建`index.ts`文件

```
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

export type LanguageSlice = { languageCode: string; };

export type LanguagePlayload = { languageCode: string; };

const initialState: LanguageSlice = { languageCode: 'tr', };

const LanguageSlice = createSlice({
  name: 'language',
  initialState,
  reducers: {
    setLanguage: (
      state: LanguageSlice,
      action: PayloadAction<LanguagePlayload>
    ) => {
      state.languageCode = action.payload.languageCode;
    },
  },
});

export const { setLanguage } = LanguageSlice.actions;
export default LanguageSlice.reducer;
```

我们的 LanguageSLice 由一个值组成，这个值就是`languageCode`。

有效载荷包含我们将发送的值。所以我们的意思是我要改变它。

初始状态是切片的默认值。你可以随意定义。

现在，我们将使用`createSlice()`方法创建切片。

我们为这个切片写一个特定的名称。

在 reducers: {}中，创建一个用于获取操作的函数。

```
setLanguage: (
      state: LanguageSlice,
      action: PayloadAction<LanguagePlayload>
    ) => {
      state.languageCode = action.payload.languageCode;
    },
```

`setLanguage`是功能。这个函数的状态将是 LanguageSlice，它包含有效负载动作。我们可以将这个函数与 arrow 函数一起使用。

在函数中，我们将从有效负载中获得的值设置为状态中的值。如果你有一个以上的州；

```
setLanguage: (
      state: LanguageSlice,
      action: PayloadAction<LanguagePlayload>
    ) => {
      state.languageCode = action.payload.languageCode;
      state.languageTitle = action.payload.languagetitle;
      state.languageIcon = action.payload.languageIcon
      ...
    },
```

最后，导出减速器。

**步骤 5——在组件中使用**

打开`Index.ts`文件，这样写；

```
 <Provider store={store}>
    <PersistGate persistor={persistedStore}>
      <App />
    </PersistGate>
  </Provider>
```

创建一个组件，或者使用您自己的组件

```
const dispatch = useDispatch();
const selector = useSelector((state: any) => state.language);
```

`dispatch`用于创建或更新你的减速器。

`selector`用于通过切片名称调用您的切片。

```
 const setBlogsLanguage = (code: string) => {
    dispatch(
      setLanguage({
        languageCode: code,
      })
    );
  };
```

`setLanguage`是一个函数，它是在减速器中创建的。在这个函数中，我将从`code`更新`languageCode`。我在`button`发送这个值

现在，时间就是用途`selector.`

```
<button
          className={`${
            selector.languageCode === 'tr' ? 'activeButtons' : 'buttons'
          }`}
          onClick={() => {
            setBlogsLanguage('tr');
            setActiveCode('tr');
          }}
        >
          Turkısh (TR)
</button>
<button
          className={`${
            selector.languageCode === 'en' ? 'activeButtons' : 'buttons'
          }`}
          onClick={() => {
            setBlogsLanguage('en');
            setActiveCode('en');
          }}
        >
          English (EN)
</button>
```

我将检查`selector.languageCode`‘tr’或‘en’

单击 TR 按钮或 EN，我将更新语言片。

我试着用最基本的方式解释了一下，希望有用。例如，我将链接留到工作版本。您可以从那里更详细地检查代码。

Simple React Redux Example

谢谢你，

`Bestte..`

再见。

[](https://bestte.medium.com/membership) [## 用我的推荐链接加入媒体

### 阅读 Beste(以及 Medium 上成千上万的其他作家)的每一个故事。你的会员费直接支持 Beste 和…

bestte.medium.com](https://bestte.medium.com/membership) [](/how-to-create-your-recursive-list-with-react-1001dc57b3c0) [## 如何用 React 创建你的递归列表？

### 如何通过制作递归列表来制作下拉列表？

javascript.plainenglish.io](/how-to-create-your-recursive-list-with-react-1001dc57b3c0) [](/how-to-create-marker-and-marker-cluster-with-leaflet-map-95e92216c391) [## 如何使用传单地图创建标记和标记簇

### 在活页地图架构中创建标记和图层，然后对标记进行聚类的方法。

javascript.plainenglish.io](/how-to-create-marker-and-marker-cluster-with-leaflet-map-95e92216c391) [](/graphql-services-and-mongodb-connection-b48b86289e93) [## GraphQL 服务和 MongoDB 连接

### 如何使用 GraphQL 服务写入 MongoDB？

javascript.plainenglish.io](/graphql-services-and-mongodb-connection-b48b86289e93) [](/how-to-avoid-runtime-errors-for-frontend-development-d24741df4a52) [## 如何避免前端开发的运行时错误

### 作为开发人员和测试人员，我们经常会遇到我们没有注意到的运行时错误。我们可以用…来摆脱它们

javascript.plainenglish.io](/how-to-avoid-runtime-errors-for-frontend-development-d24741df4a52) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***