# 如何在 React Native 中创建平面列表

> 原文：<https://javascript.plainenglish.io/flatlist-in-react-native-create-your-first-flatlist-step-by-step-with-example-4ee906be451c?source=collection_archive---------3----------------------->

## 如何在 React Native 中创建平面列表的分步指南。

![](img/8c5e36dcd750ad066510744a23590042.png)

嘿大家:)

今天我想用 React Native 提供的最重要的特性在 React Native 中创建一个 FlatList，所以废话不多说，让我们开始吧！

让我们创建一个名为`CustomList.tsx`的新组件，这个组件将创建并向 UI 显示我们的列表。在这个项目中，我将在下一条路径`./components/CustomList/CustomList.tsx`中找到`CustomList.tsx`文件。然后我将创建 Home.tsx 文件，并将它放在下一个路径:`./screens/Home/Home.tsx`。最后，我在`Home.tsx`屏幕中导入并使用组件`CustomList.tsx`。

这时的`CustomList.tsx`应该是这样的:

```
import { FlatList, FlatListProps} from 'react-native'
import React from 'react' const CustomList = () => {
  return (
    <FlatList />
  )
}export default CustomList
```

`Home.tsx`应该是这样的:

```
import { View } from 'react-native'
import React from 'react'
import CustomList from '../../components/CustomList/CustomList'const Home = () => {
  return (
  <View style={Style.flex}>
      <Text style={Style.title}>Persons List</Text>
      <CustomList />
    </View>
  )
}export default Home
```

太好了！现在，让我们创建我们的列表，我将创建一个人员数组，其属性为:姓名、年龄、地址、工作。然后，我将在`Home.tsx`文件中定位我们的 persons 数组。

`Home.tsx`应该是这样的:

```
import { View } from "react-native";
import React from "react";
import CustomList from "../../components/CustomList/CustomList";interface IPerson {
  name: string;
  age: number;
  address: string;
  job: string;
}const Home = () => {
  const persons: IPerson[] = [
    {
      name: "David John",
      age: 16,
      address: "Peter street",
      job: "React Native Developer",
    },
    {
      name: "Arik berdan",
      age: 17,
      address: "Parker street",
      job: "JavaScript Developer",
    },
    {
      name: "Sofi Zohir",
      age: 18,
      address: "Spiderman street",
      job: "React Native Developer",
    },
  ];
  return (
    <View style={Style.flex}>
      <Text style={Style.title}>Persons List</Text>
      <CustomList data={persons} />
    </View>
  );
};export default Home;const Style = StyleSheet.create({
  flex: {
    flex: 1,
  },
  title: {
    fontSize: 25,
    fontWeight: "bold",
    textAlign: "center",
    marginTop: 35,
    marginBottom: 10,
  },
});
```

# 所需的道具

## 数据

我们的 CustomList 组件需要接收列表以将其显示给 UI，因此这里我们需要所需的属性数据。我们需要向数据属性提供 persons 数组。记住，数据属性**的供给值应该总是数组**。

让我们发送人员数组:

```
import { StyleSheet, Text, View } from "react-native";
import React from "react";
import CustomList from "../../components/CustomList/CustomList";interface IPerson {
  name: string;
  age: number;
  address: string;
  job: string;
}const Home = () => {
  const persons: IPerson[] = [
    {
      name: "David John",
      age: 16,
      address: "Peter street",
      job: "React Native Developer",
    },
    {
      name: "Arik berdan",
      age: 17,
      address: "Parker street",
      job: "JavaScript Developer",
    },
    {
      name: "Sofi Zohir",
      age: 18,
      address: "Spiderman street",
      job: "React Native Developer",
    },
  ];
  return (
    <View style={Style.flex}>
      <Text style={Style.title}>Persons List</Text>
      <CustomList **data**={persons} />
    </View>
  );
};export default Home;const Style = StyleSheet.create({
  flex: {
    flex: 1,
  },
  title: {
    fontSize: 25,
    fontWeight: "bold",
    textAlign: "center",
    marginTop: 35,
    marginBottom: 10,
  },
});
```

现在我们需要接收 CustomList 组件中的数据:

```
import { FlatList, FlatListProps } from "react-native";
import React from "react";
import CustomCard from "../CustomCard/CustomCard";interface IPerson {
  name: string;
  age: number;
  address: string;
  job: string;
}interface IProps {
  **data**: IPerson[];
}const CustomList = ({ **data** }: IProps) => {
  return (
    <FlatList
      **data={data}**
    />
  );
};export default CustomList;
```

## `renderItem`

我们的 CustomList 组件现在在 data prop 上接收列表，现在我们需要运行数组中的每个元素，并将其显示到 UI 上。我们现在可以通过使用`renderItem({ item, index, separators })`来访问每个元素属性，并从**项**属性中获取姓名、年龄、地址和工作。

为 person 条目创建一个卡片是可以接受的，通过这样做，我们可以将条目参数(带有属性 name、age、address 和 job)传递给 person 卡片，并在该卡片上使用条目属性。

我将在 route: `/components/CustomCard/CustomCard.tsx`中创建一个 CustomCard 文件。

简单个人卡示例:

```
import { View, Text, StyleSheet } from "react-native";
import React from "react";interface IPerson {
  item: {
    name: string;
    age: number;
    address: string;
    job: string;
  };
}
const CustomCard = ({ item }: IPerson) => {
  return (
    <View style={Style.card}>
      <Text style={Style.row}>Name: {item.name}</Text>
      <Text style={Style.row}>Age: {item.age}</Text>
      <Text style={Style.row}>Address: {item.address}</Text>
      <Text style={Style.row}>Job: {item.job}</Text>
    </View>
  );
};export default CustomCard;const Style = StyleSheet.create({
  card: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    flexDirection: "column",
    margin: 10,
    padding: 10,
    borderRadius:1,
    borderWidth:1
  },
  row: {
    textAlign: "center",
    fontSize: 16,
  },
});
```

现在我将在自定义列表组件的`renderItem`中使用它:

```
const CustomList = ({ data }: IProps) => {
  return (
    <FlatList
      data={data}
      renderItem={({ item }) => <CustomCard item={item} />}
    />
  );
};
```

到这一步，您应该看到一个人的列表将出现在 UI 中。

免费下载完整项目:

[](https://github.com/nissimzarur/flatlist-persons) [## GitHub-nissimzarur/flat list-人员

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/nissimzarur/flatlist-persons) 

**感谢**到目前为止的阅读，如果你喜欢这样的内容，并且你想支持我作为一个程序员和作家来写更多这样的文章， [***请用我的链接注册成为 Medium 的会员(5 美元/月订阅)，你将可以无限制地访问 Medium 上的所有内容。***](https://medium.com/membership/@nissimzarur)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***