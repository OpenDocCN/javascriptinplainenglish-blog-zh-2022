# 错误类型错误:未定义的不是对象(计算' _ this . props . navigation . navigation ')

> 原文：<https://javascript.plainenglish.io/error-typeerror-undefined-is-not-an-object-evaluating-this-props-navigation-navigate-f7198c3b2a31?source=collection_archive---------2----------------------->

## 解决方案…

![](img/1f5597a665af1e06dd74600b0567e64a.png)

Photo by [DAVIDCOHEN](https://unsplash.com/@sincerelydavidcohen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在项目中努力工作时，是否遇到过这样的错误****错误类型错误:未定义不是一个对象(评估' _ this . props . navigation . navigation ')***？别担心，你可能想试试这个…

## 解决办法

在这个简短的例子中，作为一个指导方针，在 **Home.js** **屏幕上会有 **2 个屏幕** ( *“搜索栏”* & *“主页”*)和 1 个按钮(【搜索按钮】/【搜索按钮. js】),这将引导您回到****search bar . js 屏幕。******

***** *注意从“@react-navigation/native”和“const navigation = useNavigation()”导入{ useNavigation }；****

## **Home.js**

```
import React from ‘react’;
import {View} from ‘react-native’;
import SearchButton from ‘../components/SearchButton’;const Home = () => {    
   return (
      <View> 
      <SearchButton />
      </View>
  );
};export default Home;
```

## **SearchButton.js**

```
import React from ‘react’;
import {Button} from ‘react-native’;
import {useNavigation} from ‘@react-navigation/native’;function SearchButton() {
     const navigation = useNavigation();
     return (
             <Button onPress = {() => navigation.navigate(‘SearchBar’)} title=”SearchBar”/>

     );
}export default SearchButton;
```

## **“useNavigation()”的其他用法;>**

**创建 ***搜索栏*** 并通过【可触摸不透明度】使下拉 ***列表可点击*** 。使用【使用导航()】将 ***导航至*** 平台列表 ***后，点击平台列表即可进入您偏好的另一个画面*** 。**

***更内容见于*[](http://plainenglish.io/)**。注册我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区纠纷***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。****

***[](https://forelsketaura.medium.com/subscribe) [## 每当奥罗拉发布时，收到一封电子邮件。

### 每当奥罗拉发布时，收到一封电子邮件。通过注册，如果您还没有中型帐户，您将创建一个中型帐户…

forelsketaura.medium.com](https://forelsketaura.medium.com/subscribe)***