# 我写了这 10+行 JavaScript 代码；团队领导称赞代码非常优雅

> 原文：<https://javascript.plainenglish.io/i-wrote-these-10-single-lines-of-javascript-code-the-team-lead-praised-the-code-for-being-elegant-6a9c471a9613?source=collection_archive---------1----------------------->

![](img/7401c7c9e83d6f61cf820385118db678.png)

JavaScript 非常大的特点是简单易用，非常灵活，代码实现方式多种多样；有时候一行代码就能解决，尽量不要用两行。

本文编译了非常有用的一行代码。这些需求在开发中非常普遍。使用一行代码可以帮助你提高工作效率。

# 阵列重复数据消除

有许多方法可以从数组中删除所有重复的值。这里我们将讨论最简单的方法，只需一行代码即可完成:

```
const uniqueArr = (arr) => [...new Set(arr)];console.log(uniqueArr(["Front-end","js","html","js","css","html"]));
// ['Front-end', 'js', 'html', 'css']
```

uniqueArr 方法将数据转换为一个集合，然后将其解构为一个数组并返回。

# 从 url 获取参数并将它们转换为对象

网页路径的形式往往是:[www.google.com.hk](http://www.google.com.hk/)？search=js & xxx=kkk。我们经常需要带参数，可以用第三方 qs 包实现。如果你只是想删除参数，这句话的代码将它可以实现没有引入 qs。

```
const getParameters = URL => JSON.parse(`{"${decodeURI(URL.split("?")[1]).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"')}"}`
  )getParameters("[https://www.google.com.hk/search?q=js+md&newwindow=1](https://www.google.com.hk/search?q=js+md&newwindow=1)");
// {q: 'js+md', newwindow: '1'}
```

# 检查对象是否为空

检查对象是否为空实际上没那么简单。即使对象为空，它每次检查对象是否等于{}时都会返回 false。

幸运的是，下面这一行代码正是我们想要的。

```
const isEmpty = obj => Reflect.ownKeys(obj).length === 0 && obj.constructor === Object;
isEmpty({}) // true
isEmpty({a:"not empty"}) //false
```

# 反转绳子

使用 split 结合 reverse 和 join 方法可以很容易地实现反转字符串。

```
const reverse = str => str.split('').reverse().join('');
reverse('this is reverse');
// esrever si siht
```

# 生成随机十六进制

生成随机数我相信你可以做到触手可及，然后随机生成十六进制，比如生成十六进制颜色值。

```
const randomHexColor = () => `#${Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, "0")}`
console.log(randomHexColor());
// #a2ce5b
```

# 检查当前选项卡是否在后台

浏览器使用标签式浏览，任何网页都可能在后台，此时用户并没有在浏览，知道如何快速检测，你的网页是隐藏的还是用户可见的？

```
const isTabActive = () => !document.hidden;isTabActive()
// true|false
```

# 检测元素是否在焦点上

activeElement 属性返回文档中当前获得焦点的元素。

```
const elementIsInFocus = (el) => (el === document.activeElement);elementIsInFocus(anyElement)
// Returns true if the element is in focus, otherwise returns false
```

# 检查设备类型

使用 navigator.userAgent 确定它是移动设备还是计算机设备:

```
const judgeDeviceType =
      () => /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|OperaMini/i.test(navigator.userAgent) ? 'Mobile' : 'PC';judgeDeviceType()  // PC | Mobile
```

# 将文本复制到剪贴板

Clipboard API 它所有的操作都是异步的，返回 Promise 对象，不会造成页面冻结。此外，它可以将任意内容(如图片)放入剪贴板。

```
const copyText = async (text) => await navigator.clipboard.writeText(text)
copyText('One Line of Code Front End World')
```

# 获取选定的文本

使用内置的 getSelection 获取用户选择的文本:

```
const getSelectedText = () => window.getSelection().toString();getSelectedText();
//Return selected content
```

# 检查某一天是否是工作日

当我们编写自己的日历组件来确定一个日期是否是工作日时，我们经常使用它；周一至周五是工作日:

```
const isWeekday = (date) => date.getDay() % 6 !== 0;isWeekday(new Date(2022, 03, 11))
// true
```

# 转换华氏/摄氏温度

处理温度有时会令人眩晕。这两个函数帮助您将华氏温度转换为摄氏温度，将摄氏温度转换为华氏温度。

*   将华氏温度转换为摄氏温度

```
const fahrenheitToCelsius = (fahrenheit) => (fahrenheit - 32) * 5/9;fahrenheitToCelsius(50);
// 10
```

*   将摄氏温度转换为华氏温度

```
const celsiusToFahrenheit = (celsius) => celsius * 9/5 + 32;celsiusToFahrenheit(100)
// 212
```

# 两个日期之间的天数

在日常开发中，我们经常会遇到需要显示剩余天数的情况。通常，我们需要计算两个日期之间的天数差:

```
const dayDiff = (date1, date2) => Math.ceil(Math.abs(date1.getTime() - date2.getTime()) / 86400000);dayDiff(new Date("2021-10-21"), new Date("2022-02-12"))
// Result: 114
```

# 将 RGB 转换为十六进制

```
const rgbToHex = (r, g, b) =>   "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1);rgbToHex(255, 255, 255); 
//  #ffffff
```

# 计算数组的平均值

平均值的计算方法有很多种，计算的逻辑都是一样的，只是实现方法不同。实现了一行简单的代码:

```
const average = (arr) => arr.reduce((a, b) => a + b) / arr.length;
average([1,9,18,36]) //16
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****