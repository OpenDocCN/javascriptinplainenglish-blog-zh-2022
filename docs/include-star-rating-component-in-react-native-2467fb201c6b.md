# 如何在 React Native 中包含星级组件

> 原文：<https://javascript.plainenglish.io/include-star-rating-component-in-react-native-2467fb201c6b?source=collection_archive---------13----------------------->

![](img/47d9962e0ecf6da5e1ca54fe87991fc8.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

1.  通过运行以下命令安装 react-native-star-rating:

```
npm install react-native-star-rating
```

2.通过运行以下命令安装 react-native-vector-icons:

```
npm install — save react-native-vector-icons
```

**3。先把 React-native-vector-icon 链接到 iOS:**

a.在你的项目下创建一个名为**字体**的 Xcode 新文件夹:

*= >右击项目名称- >新建组- >将其命名为字体*

b.转到项目文件夹，浏览到 node modules/react-native-vector-icons/Fonts。

c.拖移 Fonts 中的所有文件，并将它们粘贴到您刚刚在 Xcode 中创建的 Fonts 文件夹中。

d.你会看到一个屏幕；在那里，选择复制项目(如果需要),然后单击完成

e.浏览到 ios/project/Info.plist 中的 info.plist 文件，并在 VS 代码或任何其他编辑器中打开该文件，您可以在其中修改该文件。将以下几行添加到文件中:

```
<key>UIViewControllerBasedStatusBarAppearance</key><false/><key>UIAppFonts</key><array><string>AntDesign.ttf</string><string>Entypo.ttf</string><string>EvilIcons.ttf</string><string>Feather.ttf</string><string>FontAwesome.ttf</string><string>FontAwesome5_Brands.ttf</string><string>FontAwesome5_Regular.ttf</string><string>FontAwesome5_Solid.ttf</string><string>Foundation.ttf</string><string>Ionicons.ttf</string><string>MaterialCommunityIcons.ttf</string><string>MaterialIcons.ttf</string><string>Octicons.ttf</string><string>SimpleLineIcons.ttf</string><string>Zocial.ttf</string><string>Fontisto.ttf</string></array>4\. Now, in your React Native App , create a file that will have the star rating component and add the following code to get the stars :import React from ‘react’;import StarRating from ‘react-native-star-rating’;const FeedbackStarRating = () =>{return (<StarRatingdisabled={false}maxStars={5}/>);}export default FeedbackStarRating
```

您可能会得到以下错误:

```
Issue: Unable to resolve module lodash.isstring from /[…]/node_modules/react-native-vector-icons/lib/icon-button.js: Module lodash.isstring does not exist in the Haste module map
```

**解决方案:**停止正在运行的 app，运行以下命令:

```
npm start — — reset-cache
```

**安卓系统:**

只需将下面一行添加到 android/app/build.gradle 文件中:

```
apply from: “../../node_modules/react-native-vector-icons/fonts.gradle”
```

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***