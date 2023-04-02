# 如何在 JavaScript 中将十进制转换成十六进制

> 原文：<https://javascript.plainenglish.io/javascript-convert-decimal-to-hex-eba0fc507917?source=collection_archive---------5----------------------->

![](img/bad32e20a007b13a3f22057e71dc1a4a.png)

在本文中，我们将学习如何在 JavaScript 中轻松地将十进制数转换成十六进制数。我们将看看一些我们需要这样做的真实场景。

# `Number` `toString()`法

要在 JavaScript 中将十进制转换为十六进制，调用十进制的`toString()`方法，将`16`作为`radix`参数传递，即`num.toString(16)`。方法将返回十六进制形式的数字的字符串表示。

例如:

```
const num = 60;
const hex = num.toString(16);
console.log(hex); // 3c

// Use parentheses when calling toString() directly
const hex2 = (60).toString(16);
console.log(hex2); // 3c
```

方法的作用是:返回一个数字的字符串表示。如果用第一个参数指定了一个基数，则该数字用该基数表示。我们通过`16`来使用基数 16，也就是十六进制的基数。

十六进制基数使用 16 个符号来表示数字:

*   `0`至`9`代表数值`0`至`9`
*   `a`至`f` ( `A`至`F`)代表`10`至`16`的数值。字母不区分大小写，因此`3C2b`与`3c2B`的值完全相同。

# 在数字文字上调用`toString()`

如果您直接在数字文字上调用`toString()`，请确保用括号(`( )`)将它括起来，或者在`toString()`前使用两个点(`..`):

```
// Use parentheses
const hex2 = (60).toString(16);
console.log(hex2); // 3c

// Use double dots
const hex3 = 50..toString(16);
console.log(hex3); // 32
```

如果只使用一个不带括号的点，JavaScript 解析器会将其视为数字文字的一部分，即小数点，而不是成员访问运算符。

```
console.log(40.); // 40
console.log(20.); // 20
```

所以会有一个错误，因为在成员名之前没有成员访问操作符。

```
// SyntaxError
console.log(40.toString(16));

// SyntaxError
console.log(20.toString(16));
```

所以你把数字用圆括号括起来，这样它们之外的所有东西都和数字分开了。

```
console.log((40).toString(16)); // 28

console.log((20).toString(16)); // 14
```

或者添加第二个点，它将被视为成员访问操作符。

```
console.log(40..toString(16)); // 28

console.log(20..toString(16)); // 14
```

# 用例:将 RGB(A)转换为十六进制

将十进制值转换为十六进制值的一个常见用途是将 [RGB](https://en.wikipedia.org/wiki/RGB_color_model) 颜色代码转换为其对等的[十六进制](https://en.wikipedia.org/wiki/Web_colors)。我们可以这样做:

```
function decToHex(dec) {
  return dec.toString(16);
}

function padToTwo(str) {
  return str.padStart(2);
}

function rgbToHex(r, g, b) {
  const hexR = padToTwo(decToHex(r));
  const hexG = padToTwo(decToHex(g));
  const hexB = padToTwo(decToHex(b));

  return `#${hexR}${hexG}${hexB}`;
}

console.log(rgbToHex(255, 128, 237)); // #ff80ed

console.log(rgbToHex(195, 151, 151)); // #c39797

console.log(rgbToHex(16, 16, 16)); // #0f0f0f
```

我们创建了一个可重用的`rgbToHex()`函数来将 RGB 代码转换成它的十六进制等价物。

我们使用`padToTwo()`函数将一个十六进制代码填充为两位数，例如`f -> 0f`。

在将`R`、`G`和`B`十进制值转换为十六进制表示后，我们将它们连接在一个以`#`字符为前缀的字符串中，形成十六进制颜色代码。

我们可以修改这个函数来接受 RGBA 值，其中`A`是一个百分比值(在 0 和 1 之间),用于指定颜色不透明度。`A`将是十六进制颜色代码的前两个字符，其值介于`00` (0 或 0%)和`ff` (255 或 100%)之间

```
function decToHex(dec) {
  return dec.toString(16);
}

function padToTwo(str) {
  return str.padStart(2);
}

function rgbToHex(r, g, b, a) {
  const hexR = padToTwo(decToHex(r));
  const hexG = padToTwo(decToHex(g));
  const hexB = padToTwo(decToHex(b));

  // Set "a" to 1 if not specified
  const aAbsolute = Math.round((a ?? 1) * 255);

  const hexA = padToTwo(decToHex(aAbsolute));

  return `#${hexA}${hexR}${hexG}${hexB}`;
}

console.log(rgbToHex(255, 128, 237)); // #ffff80ed

console.log(rgbToHex(195, 151, 151, 0.5)); // #80c39797

console.log(rgbToHex(16, 16, 16, 0.69)); // #b0101010
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/d03b16)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***