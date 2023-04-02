# 常见的反应原生问题及其解决方法

> 原文：<https://javascript.plainenglish.io/common-react-native-problems-and-solutions-22a1076e4589?source=collection_archive---------15----------------------->

## 1.在文本组件中插入换行符，请按 2。按下键盘上的“下一步”按钮后，选择下一个文本输入，3。禁用按钮元素，请按 4。清除 React 本机缓存，5。在图像元素上制作模糊效果，6。使用 ScrollView 垂直居中显示项目。

> “你如何看待一个问题比问题本身更重要——所以总是积极思考。”~诺曼·文森特·皮尔

![](img/fac109e6d5802b9604e1786a04f399ac.png)

今天我们将讨论一些常见的问题以及解决这些问题的方法。

## 如何在 React Native 中的文本组件中插入换行符？

对于 React Native 中的开发人员来说，断开文本是一件痛苦的事情，但是有一个简单的方法可以做到这一点，只需将您想要输出的文本放在花括号内，然后`，在这之后，您唯一要做的就是在您想要断开的地方添加'/n'。简单哈？

## 按下键盘上的“下一步”按钮后，如何选择下一个文本输入？

当我们想要关注文本输入的下一个元素时，我们需要创建引用并将这些引用分配给元素，对于文本输入元素，当用户完成编辑并按下键盘上的“下一步”按钮时，会调用一个属性，在下面您会发现一个要点，它显示了如何使用该属性以及如何关注下一个文本输入。

## **如何禁用 React Native 中的按钮元素？**

在 React Native 中有一个简单的方法来禁用按钮，因为具有 onPress 功能的元素允许我们通过获取下面的属性来做到这一点，你可以看到，我们使用了 cableOpacity 元素，通过禁用属性，你可以传递变量来禁用或启用按钮。

## **如何清除 React 原生缓存？**

您可以通过在终端中运行命令来清除缓存。

对于反应原生

```
react-native start --reset-cache
```

对于国家预防机制

```
npm start -- --reset-cache
```

为了世博会

```
expo start -c
```

## **如何用 React Native 制作图像元素上的模糊效果？**

BlurRadius prop 将允许您在图像上添加模糊效果。

## **如何在 React Native 中用 ScrollView 垂直居中项目？**

垂直居中是开发人员几乎每天都要处理的问题之一，如果您使用的是 ScrollView 或 FlatList，只需为 contentContainerStyle 添加如下样式，项目就会居中。

那都是我送的。希望这篇文章能帮助你解决一些日常遇到的问题。

如果你想在 LinkedIn 上联系，请点击下面的链接。

[AKIN KARAYUN | LinkedIn](https://www.linkedin.com/in/akin-karayun-ab3239bb/)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***