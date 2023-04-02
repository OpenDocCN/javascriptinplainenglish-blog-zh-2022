# 如何在 React Native 中路由(堆栈导航和使用按钮在屏幕之间移动)

> 原文：<https://javascript.plainenglish.io/how-to-route-in-react-native-stack-navigation-and-moving-between-screens-using-buttons-772d5750fbb3?source=collection_archive---------8----------------------->

## 在 React Native 中掌握路线的简单指南

![](img/26ded4b4305b4bd935254e5719a35607.png)

Photo by [Marek Piwnicki](https://unsplash.com/@marekpiwnicki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你是一个绝对的初学者，并希望同时开发一个 web 和 iOS/Android 应用程序，你可能想跳到 [***这篇文章***](/how-to-get-started-in-react-native-web-react-native-the-easiest-way-4d95c78d4470) 来轻松设置 React Native 和 React Native for Web。同时，在本文中，我们将只关注 React Native ***，而不关注与 React Native for Web 的*** 集成。

## 打开终端并运行这些命令—

```
cd desktop 
mkdir article
cd article 
npx react-native init stacknav
```

**这些命令的含义:**

`cd desktop` & `mkdir article`:在桌面上创建一个名为**文章**的文件夹。

`cd article` & `npx react-native init stacknav`:在桌面文件夹**文章**里面创建一个名为 **stacknav** 的文件夹，在 **stacknav** 里面安装 React Native。

如果你去你的桌面，你会找到文件夹**文章**，在**文章**里面，你会看到 **stacknav** 。在 **stacknav** 里面，你会发现 React Native 以及安装的相关文件。

## 打开 VSCode —

打开 VSCode， ***拖拽*** 文件夹中的**文章**进去。打开 VSCode 的终端**和*分割*和**它。在终端 左侧的 ***运行该命令——***

```
cd stacknav
npx react-native start 
```

在 VSCode 终端 的 ***右侧，运行该命令—***

```
cd stacknav
npx react-native run-ios
```

→在 VSCode 终端的左侧，您现在应该看到这些—

```
Welcome to Metro!
 Fast — Scalable — IntegratedTo reload the app press “r”
To open developer menu press “d”BUNDLE ./index.jsLOG Running “stacknav” with {“rootTag”:1,”initialProps”:{}}
```

→在 VSCode 终端的右侧，您应该能够看到这些—

```
info Launching "org.reactjs.native.example.stacknav"
success Successfully launched the app on the simulator
```

## 安装本地 Stack Navigator 库和项目的其他依赖项→

在右边的终端中运行这些命令，

```
yarn add @react-navigation/native-stack
yarn add @react-navigation/native
yarn add react-native-screens react-native-safe-area-context
npx pod-install ios
```

## App.js —

打开 App.js 文件。在 App.js 中，去掉 ***所有*** 代码，加上 ***这些—***

```
import React from 'react';
import {NavigationContainer} from '@react-navigation/native';
import {View, Button, StyleSheet, Dimensions} from 'react-native';
import {createNativeStackNavigator} from '@react-navigation/native-stack';const height = Dimensions.get('window').height;
const Stack = createNativeStackNavigator();function MainScreen({navigation}) {
    return (
      <View style = {{backgroundColor: 'white', flex: 1}}>
      <View style = {styles.button}>
      <Button title = "Go To Favourites"
       onPress={() => navigation.navigate('Favourite')}>
      </Button>
      </View>
      </View>
  );
}function FavouriteScreen({navigation}) {
    return (
      <View style = {{
       margin: height/2.1,
       width: 185,
       alignSelf: 'center'}}>
      <Button title = 'Back To Main Page'
       onPress={() => navigation.navigate('Main')}>
      </Button>
      </View>
  );
}function App() {
    return (
      <NavigationContainer>
      <Stack.Navigator screenOptions = {{headerShown: false}}>
      <Stack.Screen name = "Main"
       component = {MainScreen}
       options = {{title: 'Main'}}/>
      <Stack.Screen name = "Favourite"
       component = {FavouriteScreen}
       options = {{title: 'Favourite'}}/>
      </Stack.Navigator>
      </NavigationContainer>
  );
};export default App;const styles = StyleSheet.create({
      button: {
      borderRadius: 25,
      width: 185,
      backgroundColor: 'orange',
      alignSelf: 'center',
      margin: height/2.1,
  }
})
```

如果您看到此错误→

> 错误固定冲突:在 UIManager 中找不到 requinativecomponent:“rnscreenstackheaderconfig”。

## 解决方案—

*   寻找 **node_modules** 文件夹
*   删除整个 **node_modules** 文件夹
*   在 MacBook 上，按下→ control c
    (停止 metro)
*   检查您是否在主项目目录中。如果您一直在关注本文，您的终端应该显示“ **stacknav** ”。进入正确的项目目录后，运行以下命令→

```
yarn install
```

你会看到**节点 _ 模块**文件夹已经返回。在分割 VSCode 终端中，运行以下命令—

在左侧终端上，运行以下命令—

```
npx react-native start
```

在右侧终端上，运行以下命令—

```
npx react-native run-ios
```

现在，您应该可以在第一个屏幕上看到一个橙色按钮(“转到收藏夹”)，这将引导您进入第二个屏幕，该屏幕有一个无色按钮(“返回主页面”)。要创建更多的屏幕，在导航容器下添加更多的“堆栈屏幕”，然后为它们创建一个新功能。

要定制按钮、背景或文本的样式，请在“样式”下编辑。查看其余文章，查找遇到的任何错误的故障排除。更多关于 React Native 和 React Native for Web 的教程将会定期发布。请经常回来查看更多简单的指南和提示！

[](/how-to-get-started-in-react-native-web-react-native-the-easiest-way-4d95c78d4470) [## 如何开始使用 React Native Web & React Native(最简单的方法)

### 在一个源代码中创建本地应用和 web 应用的方法(综合指南)

javascript.plainenglish.io](/how-to-get-started-in-react-native-web-react-native-the-easiest-way-4d95c78d4470) ![](img/714139899d5992740e4178fec2467cc2.png)

Photo by [Michael Milverton](https://unsplash.com/@milverton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*