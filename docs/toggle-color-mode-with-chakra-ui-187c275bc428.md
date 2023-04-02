# 用脉轮用户界面切换颜色模式

> 原文：<https://javascript.plainenglish.io/toggle-color-mode-with-chakra-ui-187c275bc428?source=collection_archive---------13----------------------->

## 了解如何切换查克拉用户界面的颜色模式。

![](img/01cc0a0c86eb0d49c8f6ce59b59270aa.png)

Photo by [Stainless Images](https://unsplash.com/@ramone?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近我刚刚完成了一个来自 [frontendmentor.io](https://www.frontendmentor.io/home) 的挑战，它是关于在主页上显示一些来自 API 的数据，并且只需要一个又一个页面就可以到达每个项目的细节，非常简单。但我的注意力被吸引到一个要求，它需要能够切换颜色模式，在黑暗，明亮的模式。我觉得受到了挑战。

毫无疑问，我直接下载启动项目。我还决定用`create-create-app`模板做挑战和查克拉 UI 作为它的 UI 库。我现在真的很喜欢 Chakra，因为它是基于组件的(更多内容见这里的)。

以下是我学到的快速切换颜色开关的方法。

# 1.把你的组件包在里面`ChakraProvider`

```
function App() {return (<ChakraProvider> <Header /> <Routes> <Route exact path='/' element={<Home />} /> <Route path='/country/:name' element={<Country />} /> </Routes> </ChakraProvider>);}
```

# 2.在根目录下创建 theme.js

*//theme.js*

```
//background color
export const darkBg = 'hsl(207, 26%, 17%)'
export const lightBg = 'hsl(0, 0%, 98%)'//element color
export const darkElement = 'hsl(209, 23%, 22%)'
export const lightElement = 'hsl(0, 0%, 100%)'//text color
export const lightModeText = 'hsl(200, 15%, 8%)'
export const darkModeText = 'hsl(0, 0%, 100%)'
```

我还导出所有恒定颜色的原因是，我想用它来与当前颜色状态进行比较，我们将在稍后讨论它。还是在`theme.js`文件中，我定义了一些颜色，以便以后更容易访问。然后我声明了一个函数来改变颜色，如下所示:

```
import { useColorModeValue } from '@chakra-ui/react'export const CentralTheme = () => {
  let elementColor = useColorModeValue(lightElement, darkElement)
  let bgColor = useColorModeValue(lightBg, darkBg)
  let textColor = useColorModeValue(lightModeText, darkModeText)
  return {
    elementColor, bgColor, textColor
  }
}
```

在那里，我使用 Chakra 提供的`useColorModeValue`钩子，并将它赋给一个变量，这样我就可以很容易地在另一个组件中访问它。像`elementColor`这样的变量将保存当前的颜色值。这是关键语法(更多来自[文档](https://chakra-ui.com/docs/features/color-mode#usecolormodevalue)):

```
// Here's the signature 
const value = useColorModeValue(lightModeValue, darkModeValue)
```

# 3.从另一个组件访问功能

例如，在我的 header 组件中，我使用了来自`theme.js`的`CentralTheme()`函数的颜色，因此它可以根据当前的颜色模式改变方向。

*//header.js*

```
import { Flex, Box, useColorMode } from "@chakra-ui/react";
import { CentralTheme, lightBg } from "../theme";const Header = () => {
  const { toggleColorMode } = useColorMode() return(
    <Flex bg={CentralTheme().bgColor} color={CentralTheme().textColor}>
      <Flex onClick={toggleColorMode} >
      {
        CentralTheme().bgColor === lightBg ?
          'Light Mode'
        :
          'Dark Mode'
      }
      </Flex>
    </Flex>
  )
}
```

在那里，我导入`useColorMode`并通过析构它得到`toggleColorMode`。这个`toggleColorMode`用来改变颜色模式，并放入 onClick 事件中。

我还通过调用`bg` 和`color` 道具内部的`CentralTheme()`函数来访问当前的背景和文字颜色，得到我想要的值。

我还将当前颜色与从`theme.js`导出的恒定颜色进行比较，以决定显示哪个文本。最后，每当您单击组件时，组件将改变其颜色。

其余部分是相同的，将其应用于另一个组件。这就是我今天从脉轮中学到的一切，祝你愉快！

*更内容于* [***浅显易懂的英语中***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社群不和***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。*