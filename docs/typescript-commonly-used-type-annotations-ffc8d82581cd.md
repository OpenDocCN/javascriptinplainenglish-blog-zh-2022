# TypeScript 中常用的类型批注

> 原文：<https://javascript.plainenglish.io/typescript-commonly-used-type-annotations-ffc8d82581cd?source=collection_archive---------11----------------------->

## 如何以更好的方式使用类型和类型脚本备忘单

![](img/84d4a1b5ef4f7fb175b23f6dc9156e1d.png)

Photo by [Kenny Eliason](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 原始类型

始终使用小写的字符串、数字或布尔值。不要使用字符串、数字和布尔值(以大写字母开头)。

1.  **弦**——嗯，你知道，弦就是弦。
2.  **number** —我们不需要担心 int、float 或 double equivalent。你可以给所有看起来像数字的东西赋予数字类型注释。
3.  **布尔型** —只有两个值是可能的——真或假。
4.  **null** — null 是一个 nothing 对象。
5.  **未定义** —其值未定义时，为未定义。

# 其余的

1.  **数组** —值的数组。数组标注有 2 种语法:
    a .像 number[]，string[]，等等。当需要同构数据结构时，这很有用。
    b .用泛型数组<编号>。当需要具有联合类型的数据结构时，这很有用。
2.  **函数类型表达式** —当我们在多个组件之间传递函数作为道具时，我们经常需要函数类型表达式。
    例如，一个状态设置函数经常被作为道具传递，我们可以为这个道具添加一个类型表达式，比如(prevState: string) = > void。就像许多其他语言一样，Typescript 中的 void 是在没有数据时使用的。在上面的表达式中，因为函数不返回任何东西，所以返回类型是 void。
3.  **对象类型** —任何带有属性的 JavaScript 值。要定义一个对象类型，我们只需列出它的属性和类型。例如:
    `const color: {name: string, hexCode: string} = {
    name: 'white',
    hexCode: '#fff'
    }` *可选属性:*
    对象类型也可以指定其部分或全部属性是可选的。去做这个，混蛋？在属性名之后。例如
    `const color: {name: string, hexCode: string, rgba?: string} = {
    name: 'white',
    hexCode: '#fff'
    }` **注意:当你从一个*可选属性*中读取时，确保你在使用它之前正在*检查未定义的*。**
4.  联合类型(union types)—TypeScript 允许我们以有趣的方式组合各种类型，并从中构建新的类型。例如
    `let id: string | number = 0` 在这里，用联合式的一个重要概念*就发挥作用了。我们改天再谈这件事。在那之前，你可以试着把它当作家庭作业来学习。祝你好运！*
5.  ***文字类型** —在 TypeScript 中，我们可以在类型位置引用特定的字符串、数字和布尔值。
    文字类型本身并不有趣。但是如果用在联合字体中，它们会非常有用。
    通常在 React 中，我们需要将道具或功能参数的值限制为特定值。例如 justifyContent:'右' | '左' | '居中'。*
6.  ***any** —如果你不想要类型检查错误，你可以使用 any。我会说尽可能避免使用任何类型的注释。这只是一个绕过 typescript 的技巧，因此，如果没有计划地使用它，可能会出现类型和逻辑错误。*

# *TypeScript 中的函数:*

*TypeScript 允许您指定函数的输入和输出值的类型。*

*所以函数有参数(输入)类型注释和返回(输出)类型注释。*

***参数类型注释**位于参数名称之后:*

```
*function getSquare(num: number) {
  console.log(number*number)
}*
```

*为什么参数类型注释很有用？
检查该函数的参数类型。
—这让我们意识到我们需要在函数代码中注意的可能类型。
—这也为我们提供了调用函数时预期参数及其类型的列表。*

**即使没有参数类型注释，TypeScript 仍然会检查您传递的参数数量是否正确。**

***返回类型注释**转到参数列表后:*

```
*function getSquare(num: number): number {
  return number*number
}*
```

*为什么返回类型注释有用？
i)用于记录目的
ii)避免意外变更*

## ***打字稿常用类型备忘单***

*TypeScript Common Types Cheatsheet*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**