# 如何在 JavaScript 中更好地使用条件判断

> 原文：<https://javascript.plainenglish.io/how-to-better-use-conditional-judgment-in-javascript-5aa1d2981e08?source=collection_archive---------6----------------------->

![](img/40a1f3b72aefa3da7811e333d8a7424b.png)

本文用很短的时间介绍如何用 JavaScript 编写更简单的条件判断，帮助您编写更简洁、可读性更强的代码。

假设我们有一个将颜色值转换为十六进制编码的函数。

```
function convertToHex(color) {
  if (typeof color === 'string') {
    if (color === 'slate') {
      return '#64748b'
    } else if (color === 'gray') {
      return '#6b7280'
    } else if (color === 'red') {
      return '#ef4444'
    } else if (color === 'orange') {
      return '#f97316'
    } else if (color === 'yellow') {
      return '#eab308'
    } else if (color === 'green') {
      return '#22c55e'
    } else {
      return '#ffffff'
    }
  } else {
    return '#ffffff'
  }
}
```

这个函数的目标很简单，就是传入颜色字符串，然后返回相应的十六进制。如果传入的不是字符串，或者没有传递任何内容，则返回白色十六进制。

接下来，我们开始优化这段代码。

## 避免直接使用字符串作为条件

直接使用字符串作为条件的问题是，当我们拼错时会很尴尬。

```
convertToHex("salte")
```

为了避免这种错误，我们可以使用常数。

```
const Colors = {
 SLATE: 'slate',
  GRAY: 'gray',
  // ...
}function convertToHex(color) {
  if (typeof color === 'string') {
    if (color === Colors.SLATE) {
      return '#64748b'
    } else if (color === Color.GRAY) {
      return '#6b7280'
    }
    // ...
  } else {
    return '#ffffff'
  }
}convertToHex(Colors.SLATE)
```

如果使用 typescript，那么可以直接使用 enum。

## 使用对象

其实从上面的代码中不难发现，我们可以直接将十六进制的值存储在对象的值中。

```
const Colors = {
 SLATE: '#64748b',
  GRAY: '#6b7280',
  // ...
}function convertToHex(color) {
  if (color in Colors) {
    return Colors[color]
  } else {
    return '#ffffff'
  }
}convertToHex(Colors.SLATE)
```

这样代码会更简洁，可读性更强。

## 不符合预期，提前返回

另一个最佳实践是，我们可以将意外返回写在函数的顶部，以避免忘记返回。

```
const Colors = {
 SLATE: '#64748b',
  GRAY: '#6b7280',
  // ...
}function convertToHex(color) {
  if (!color in Colors) {
    return '#ffffff'
  }
  return Colors[color]
}convertToHex(Colors.SLATE)
```

这样你甚至不需要另外一个。使用这个技巧，我们可以消除代码中的许多其他内容。

## 对对象使用贴图

使用 Map 更加专门化，因为它可以存储任何类型的键，并且它从 Map.prototype 继承而来，具有更方便的方法和属性。

而 Object 更方便访问属性，我们可以继续使用 Object 来实现枚举的作用。

```
const ColorsEnum = {
 SLATE: 'slate',
  GRAY: 'gray',
  // ...
}const Colors = new Map()
Colors.set(ColorsEnum.SLATE, '#64748b')
Colors.set(ColorsEnum.GRAY, '#6b7280')
// ...
Colors.set('DEFAULT', '#ffffff')function convertToHex(color) {
  if (!Colors.has(color)) {
    return Colors.get('DEFAULT')
  }
  return Colors.get(color)
}convertToHex(Colors.SLATE)
```

## 地图也可以存储功能

假设我们存储了很多颜色，多达上千个，还需要支持后端配置，通过一定的操作过程就可以得到结果。

然后我们可以使用映射来存储函数。

```
return Colors.get(color)()
```

## 尽量避免三元表达式和开关

三元表达式虽然简洁，但可读性却大打折扣。如果是多级条件，阅读起来会很困难。

switch 和 if 并没有明显的优势，但是有时候很容易返回，导致代码不能按预期执行。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***