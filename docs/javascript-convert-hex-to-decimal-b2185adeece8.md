# 如何在 JavaScript 中将十六进制转换成十进制

> 原文：<https://javascript.plainenglish.io/javascript-convert-hex-to-decimal-b2185adeece8?source=collection_archive---------3----------------------->

## 了解如何在 JavaScript 中轻松地将十六进制数转换为十进制数，并查看这样做的真实用例。

![](img/f247418822bcec4767043bb6fa3472dc.png)

在本文中，我们将学习如何在 JavaScript 中将十六进制数转换成十进制数。我们将看看一些我们需要这样做的真实场景。

# parseInt()函数

要将十六进制转换为十进制，调用`parseInt()`函数，将十六进制和`16`分别作为第一个和第二个参数传递，即`parseInt(hex, 16)`。例如:

```
function hexToDec(hex) {
  return parseInt(hex, 16);
}console.log(hexToDec('f')); // 15
console.log(hexToDec('abc')); // 2748
console.log(hexToDec(345)); // 837
```

函数解析一个字符串并返回一个指定基数的整数。它有两个参数:

1.  `string` -要解析的字符串。
2.  `radix` -一个介于 2 和 36 之间的整数，表示字符串的基数/基数。

忽略传递给它的字符串中的任何前导空格。

```
console.log(parseInt('   a', 16)); // 10
console.log(parseInt('   cd', 16)); // 205
```

如果传递的字符串不是指定基数的有效数字，`parseInt()`不会抛出错误，而是返回`NaN`。

```
console.log(parseInt('js', 16)); // NaN// 'a' does not exist in base 10
console.log(parseInt('a', 10)); // NaN// 5 does not exist in base 2
console.log(parseInt(5, 2)); // NaN
```

如果基数不在 2 和 36 之间，`parseInt()`也将返回`NaN`。

```
console.log(parseInt(54, 1));
console.log(parseInt('aa', 37));
console.log(parseInt(10, 50));
```

如果基数是无效数字或未设置，并且字符串以`0x`或`0X`开头，则基数假定为 16。但是如果字符串以任何其他值开始，基数被假定为 10。

```
// base 10 assumed
console.log(parseInt('45')); // 45
console.log(parseInt('36', 'invalid')); // 36// 'f' and 'b' do NOT exist in assumed base 10
console.log(parseInt('ff')); // NaN
console.log(parseInt('bb', 'invalid')); // NaN// 'f' and 'b' do exist in assumed base 16
console.log(parseInt('0xff')); // 255
console.log(parseInt('0Xbb', 'invalid')); // 187
```

# 用例:将十六进制代码转换为 RGB(A)

将十六进制值转换为十进制值的一个常见用途是将[彩色十六进制码](https://en.wikipedia.org/wiki/Web_colors)转换为其等效的 RGB 格式。我们可以这样做:

```
function hexToDec(hex) {
  return parseInt(hex, 16);
}function hexToRGB(hexColor) {
  const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hexColor);
  return {
    r: hexToDec(result[1]),
    g: hexToDec(result[2]),
    b: hexToDec(result[3]),
  };
}// { r: 255, g: 128, b: 237 }
console.log(hexToRGB('#ff80ed'));// { r: 195, g: 151, b: 151 }
console.log(hexToRGB('#c39797'));// { r: 255, g: 255, b: 255 }
console.log(hexToRGB('#ffffff'));
```

我们创建了一个可重用的`hexToRGB()`函数来轻松重用这个逻辑。

我们使用正则表达式来匹配和分隔代表红色(R)、绿色(G)和蓝色(B)的两个字母的代码。我们调用`exec()`方法在指定的十六进制颜色代码中查找这个正则表达式的匹配项。

```
/**
[
  '#ff80ed',
  'ff',
  '80',
  'ed',
  index: 0,
  input: '#ff80ed',
  groups: undefined
]
 */
console.log(/^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec('#ff80ed'));
```

在分离它们之后，我们使用我们的`hexToDec()`方法将它们中的每一个转换成它的十进制等价物。

我们返回一个具有`r`、`g`和`b`属性的对象，分别包含红色、绿色和蓝色的值。

根据我们的用例，我们可以返回一个`rgb()`字符串，而不是一个对象。这对于彩色动画很有用，因为有些动画库使用 RGB 值，但不使用十六进制颜色代码。

```
function hexToDec(hex) {
  return parseInt(hex, 16);
}function hexToRGB(hexColor) {
  const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hexColor);
  const r = hexToDec(result[1]);
  const g = hexToDec(result[2]);
  const b = hexToDec(result[3]); return `rgb(${r}, ${g}, ${b})`;
}// rgb(255, 128, 237)
console.log(hexToRGB('#ff80ed'));// rgb(195, 151, 151)
console.log(hexToRGB('#c39797'));// rgb(255, 255, 255)
console.log(hexToRGB('#ffffff'));
```

我们可以修改函数来检测十六进制代码中的 alpha 值，并将颜色代码转换为 RGBA 格式。如果没有指定，我们将使用 alpha 值`1`。

```
function hexToDec(hex) {
  return parseInt(hex, 16);
}function hexToRGBA(hexColor) {
  const regex = /^#?([a-f\d]{2})?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i;
  const result = regex.exec(hexColor); const alphaHex = result[1];
  const a = alphaHex ? hexToDec(alphaHex) / 255 : 1;
  const r = hexToDec(result[2]);
  const g = hexToDec(result[3]);
  const b = hexToDec(result[4]); return { r, g, b, a };
}// { r: 255, g: 128, b: 237, a: 1 }
console.log(hexToRGBA('#ff80ed'));// { r: 195, g: 151, b: 151, a: 1 }
console.log(hexToRGBA('#c39797'));// { r: 255, g: 128, b: 237, a: 0.8666666666666667 }
console.log(hexToRGBA('#ddff80ed'));// { r: 195, g: 151, b: 151, a: 0.6901960784313725 }
console.log(hexToRGBA('#b0c39797'));
```

我们也可以返回一个`rgba()`字符串而不是一个对象:

```
function hexToDec(hex) {
  return parseInt(hex, 16);
}function hexToRGBA(hexColor) {
  const regex = /^#?([a-f\d]{2})?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i;
  const result = regex.exec(hexColor); const alphaHex = result[1];
  const a = alphaHex ? hexToDec(alphaHex) / 255 : 1;
  const r = hexToDec(result[2]);
  const g = hexToDec(result[3]);
  const b = hexToDec(result[4]); return `rgba(${r}, ${g}, ${b}, ${a.toFixed(3)})`;
}// rgba(255, 128, 237, 1.000)
console.log(hexToRGBA('#ff80ed'));// rgba(195, 151, 151, 1.000)
console.log(hexToRGBA('#c39797'));// rgba(255, 128, 237, 0.867)
console.log(hexToRGBA('#ddff80ed'));// rgba(195, 151, 151, 0.690)
console.log(hexToRGBA('#b0c39797'));
```

【更新于:【codingbeautydev.com】

# **JavaScript 做的每一件疯狂的事情**

**一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。**

**![](img/143ee152ba78025ea8643ba5b9726a20.png)**

**[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。**