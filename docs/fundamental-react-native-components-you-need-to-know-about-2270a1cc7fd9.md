# 您需要了解的基本反应原生组件

> 原文：<https://javascript.plainenglish.io/fundamental-react-native-components-you-need-to-know-about-2270a1cc7fd9?source=collection_archive---------4----------------------->

## 您所需要了解的基本 React 原生组件以及如何创建自定义组件。

![](img/baf3ae11dcbddc8db8d68f7eb057bef8.png)

[React Native](https://reactnative.dev/) 使您能够从单一代码库创建本地应用程序。使用 React Native 创建的应用程序是本机应用程序，而不是 web 应用程序。

在过去几年中，React Native 在受欢迎程度方面一直排名第一。根据[统计](https://www.statista.com/statistics/869224/worldwide-software-developer-working-hours/)，全球大约 40%的开发者使用 React Native。

![](img/e49401760a6cc946eeda7b7e3d2be86b.png)

由于其单一的代码库、Javascript 的使用以及对性能的关注，它已经成为最受欢迎的框架之一。

它有许多有利条件。最大的问题是框架的混合性质。[如今混合应用程序风靡一时](https://venturebeat.com/business/why-74-of-the-top-50-retail-apps-are-hybrid-apps-not-native-apps/)，像 Twitter & Instagram 这样的顶级应用程序将它们的优势带到了聚光灯下。

现在可以使用一个代码库来为 Android 和 iOS 构建一个应用程序，而不是像以前那样需要维护两个分别用 Java 和 Swift 编写的代码库。这意味着更快的上市和更新时间。

除此之外，它还是免费开源的，并且有一个[大型开发者社区](https://github.com/facebook/react-native/stargazers)，在全球拥有数千名成员。

React 的本机特性是热重装，这意味着只对发生变化的代码打补丁，从而节省了大量时间。此外，代码库遵循与 React 项目相似的模式和概念，因此 web 开发人员可以轻松地使用该框架来构建移动应用程序。

像 D.R.Y(不要重复自己)这样经过时间考验的实践可以很容易地实现。据估计，Android 和 iOS 之间大约 90%的代码可能会被重用。

为了实现无缝开发，React Native 提供了大量组件，这些组件本质上只是本机组件的包装器，使您能够轻松地插入本机代码。

# 深入了解 React 本机组件

React Native 具有各种内置组件，可以帮助您将 UI 分解为可重用的部分。这些元素是在函数或类中指定的。只需从 React Native 导入这些组件，并在文件中自由使用它们。

React 本地组件的主要应用是使开发人员能够使用一组预定义的组件快速设计用户界面。

在幕后，这些组件只是使用 JavaScript 生成的，然而，iOS 和 Android 不支持 JS，因此它使用特定于平台的 API 和模块在运行时转换为原生组件。

因为框架提供了过多的组件，所以有几个组件是最重要的。

# 基本组件

## 1.视角

将它视为一个容器、一个 div 或一个节。视图组件显示幻灯片、文本、图像、用户输入以及您能想到的几乎任何东西。

它在运行时被转换成 Android 和 iOS 组件。

```
import React from "react";
import { View, Text } from "react-native";
const App = () => {
  return (
    <View style={{ margin: 10 }}>
      <Text style={{ marginBottom: 10 }}>
        Hello Readers, I'm inside View Component
      </Text>
      <Text style={{ marginBottom: 10 }}>You can also define image</Text>
    </View>
  );
};export default App;
```

这里我们有视图组件，在其中我们定义了一个名为 Text 的组件。

## 2.文本

它是一个在应用程序中显示文本的组件。它支持嵌套、触摸事件以及标准样式选项，如自定义字体、字体大小等。

请注意，不能将文本直接放在视图组件中，这一点很重要。换句话说，文本必须始终包装在文本组件中。

```
import React from "react";
import { View, Text } from "react-native";
const App = () => {
  return (
    <View style={{ margin: 10 }}>
      <Text style={{ marginBottom: 10 }}>Hello, I am Text Component</Text>
      <Text style={{ marginBottom: 10 }}>I am also a Text Component</Text>
    </View>
  );
};
export default App;
```

## 3.图像

下一个 React 本地组件是图像。它可以让你添加图像到你的应用程序。

此外，您可以包括网络图像、临时图像、静态图像等等。

```
import React from "react";
import { View, Text, Image } from "react-native";
const App = () => {
  return (
    <View>
      <Text>The Image Component is next to me.</Text>
      <Image
        source={{
          uri: "[https://reactnative.dev/docs/assets/p_cat2.png](https://reactnative.dev/docs/assets/p_cat2.png)",
        }}
        style={{ width: 200, height: 200 }}
      />
      <Image
        style={styles.logo}
        source={{
          uri: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg==',
        }}
      /></View>
  );
};
export default App;
```

还有访问图像大小或预取图像的方法。

例如，我们可以使用以下公式获得图像的大小:

```
Image.getSize(uri, success, [failure]);
```

## 4.文本输入

该组件使用户能够添加输入。

您可以通过传递 props 来保存来自用户的输入响应，更新某些部分和文本，或者在用户提交输入后查看应用程序，从而为它添加更多功能。

其他事件，如 onChange、onSubmitEditing、onScroll 等。，可用于修改 TextInput 组件。

```
import React from "react";
import { View, Text, TextInput } from "react-native";const App = () => {
  return (
    <View style={{ margin: 10 }}>
      <Text>The user can type something.</Text>
      <TextInput
        style={{
          height: 30,
          borderColor: "black",
          borderWidth: 1,
        }}
        defaultValue="I am a Text Input"
      />
    </View>
  );
};export default App;
```

## 5.滚动视图

您可以使用 ScrollView 组件水平或垂直滚动特定区域。换句话说，如果您有很多子组件，可能无法一次显示在屏幕上，那么您可以使用 ScrollView，因此您可能希望在滚动后显示其中一些子组件。

要使用它，只需将该部分包装在 ScrollView 组件中。

在这里，ScrollView 同时呈现其所有子组件，这可能会导致较差的呈现和性能。

```
import React from "react";
import { View, Text, Image, ScrollView, TextInput } from "react-native";const App = () => {
  return (
    <ScrollView>
      <Text style={{ fontSize: 100 }}>
        I am a text component inside ScrollView component
      </Text>
      <Text style={{ fontSize: 100 }}>Some more text</Text>
    </ScrollView>
  );
};export default App;
```

# 用户界面

## 1.纽扣

下一个组件叫做“Button ”,顾名思义，它可以帮助您创建用户可以与之交互的按钮。这些只是用于控制屏幕和执行操作的触敏元件。

你甚至可以借助 [TouchableOpacity](https://reactnative.dev/docs/touchableopacity) 或 [TouchableWithoutFeedback](https://reactnative.dev/docs/touchablewithoutfeedback) 定制或构建一些新的按钮。还有 [TouchableHighlight](https://reactnative.dev/docs/touchablehighlight) ，它通过克隆它的孩子并对其应用响应道具来工作。

```
import React from "react";
import { Button, View, Alert } from "react-native";const App = () => (
  <View>
    <Button title="Click Me" onPress={() => Alert.alert("I am pressed")} />
  </View>
);export default App;
```

## 2.转换

开关组件基本上是一个开/关按钮或一个布尔值。用户可以根据自己的偏好进行更改。

它是一个受控组件，需要您使用“onValueChange()”回调函数手动更新。

如示例所示，我们导入了 Switch 组件并传递了两个道具:一个用于更改状态，另一个用于显示状态。

```
import React, { useState } from "react";
import { View, Switch, StyleSheet } from "react-native";
const App = () => {
  const [isTrue, setIsTrue] = useState(true);
  const toggleSwitch = () => setIsTrue((previousState) => !previousState);
  return (
    <View style={styles.container}>
      <Switch onValueChange={toggleSwitch} value={isTrue} />
    </View>
  );
};const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
});
export default App;
```

# 列表视图

## 1.平面列表

该组件以列表格式显示数据。在 FlatList 组件中，您需要知道两个关键的属性，即“数据”和“呈现项”。

在 data prop 中，我们需要传递我们想要呈现的数据。renderItem prop 将逐个渲染数据。

如果你没有传递一个钥匙作为道具，你可能会看到一个警告。

```
import React from "react";
import {
  SafeAreaView,
  View,
  FlatList,
  StyleSheet,
  Text,
  StatusBar,
} from "react-native";
const DATA = [
  {
    id: "1",
    title: "Hello",
  },
  {
    id: "2",
    title: "Bye",
  },
  {
    id: "3",
    title: "See You",
  },
];
const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);
const App = () => {
  const renderItem = ({ item }) => <Item title={item.title} />;
  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={(item) => item.id}
      />
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight || 0,
  },
  item: {
    backgroundColor: "blue",
    padding: 20,
    marginVertical: 8,
    marginHorizontal: 16,
  },
  title: {
    fontSize: 18,
  },
});
export default App;
```

## 2.章节列表

React Native SectionList 组件是一个列表视图组件，它将数据列表划分为多个不完整的逻辑部分。

它支持各种各样的现代功能，如滚动加载、列表页脚以及拉刷新功能。

```
import React from "react";
import {
  StyleSheet,
  Text,
  View,
  SafeAreaView,
  SectionList,
  StatusBar,
} from "react-native";
const DATA = [
  {
    title: "Starter",
    data: ["Bacon Rings", "Tuna Empanadillas", "Paneer Crispy"],
  },
  {
    title: "Main Course",
    data: [
      "Shrimp Quinoa Fried Rice",
      "Salmon Mac And Cheese",
      "Creamy Garlic Paprika Shrimp",
    ],
  },
];
const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);
const App = () => (
  <SafeAreaView style={styles.container}>
    <SectionList
      sections={DATA}
      keyExtractor={(item, index) => item + index}
      renderItem={({ item }) => <Item title={item} />}
      renderSectionHeader={({ section: { title } }) => (
        <Text style={styles.header}>{title}</Text>
      )}
    />
  </SafeAreaView>
);
const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
    marginHorizontal: 16,
  },
  item: {
    backgroundColor: "#f9c2ff",
    padding: 20,
    marginVertical: 8,
  },
  header: {
    fontSize: 32,
    backgroundColor: "#fff",
  },
  title: {
    fontSize: 18,
  },
});
export default App;
```

# 创建自定义 React 本机组件

当从单一代码库开发 iOS 或 Android 应用程序时，React Native 的表现令人钦佩，这两个平台使用相同的组件。内置组件对于大多数界面和功能来说都很棒，但在某些地方可能会有所欠缺。

由于 iOS 和 Android 的操作方式不同，您可能希望设计一些基于特定操作系统的独特的自定义组件。

下面是一个自定义组件的示例。

```
import React from 'react';
import { View, Text } from 'react-native';const CustomTextComponent = () => {
  return (
    <View> 
      <Text>Hello, I am a Custom Component</Text>
    </View> 
  );
}export default CustomTextComponent;
```

就这样，您已经创建了一个定制组件。现在，您可以将它导入到文件中并重复使用。

使用 [Locofy.ai](https://locofy.ai) 插件，通过让插件生成 React 本地组件，遵循最佳实践和行业标准，你可以在几个小时内将你在 [Figma](https://www.figma.com/) 和 [Adobe XD](https://www.adobe.com/in/products/xd.html) 中的设计转化为生产就绪的前端代码。

您可以简单地[标记设计中的元素](https://guide.locofy.ai/tagging-elements-on-your-react-native-project)，然后[使用](https://guide.locofy.ai/exporting-react-native-code) [Locofy Builder](https://guide.locofy.ai/locofy-builder-basics) 以 JavaScript 或 TypeScript 的形式导出代码，这是设计和高质量代码之间的自然过渡。

Locofy Builder 将允许您定制您的项目并生成 React 本地组件。您甚至可以指定希望组件接受的属性，从而使代码具有高度的可扩展性。更重要的是，您可以只导出组件，而不是整个代码库，从而允许您快速地将它们插入到现有的项目中。

[使用 Locofy.ai 插件从设计到原生应用，将产品交付速度提高 5 倍！](https://locofy.ai)

希望你喜欢。

就这样——谢谢。

[*如果你喜欢看这样的故事，并想帮助我成为一名作家，可以考虑成为一名中等会员*](https://nitinfab.medium.com/membership) *。它每月花费 5 美元，给你* [*无限制访问媒体内容*](https://nitinfab.medium.com/membership) *。如果你通过我的链接注册，我会得到一点佣金。*

*原发布于*[*https://blog . locofy . ai*](https://blog.locofy.ai/react-native-components)*。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。**