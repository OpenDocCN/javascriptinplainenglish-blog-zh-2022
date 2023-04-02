# 33 非常有用的 JavaScript 单行代码集

> 原文：<https://javascript.plainenglish.io/33-very-useful-javascript-one-line-code-collection-3acb042a246f?source=collection_archive---------4----------------------->

## 一组有用的 JavaScript 单行代码，让开发人员的工作更轻松。

![](img/6b35d2454dbfdb43d341d143a6a247b6.png)

Photo by [didin emelu](https://unsplash.com/@didin_emelu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近在社区看到一些关于一行代码的文章。我觉得很感兴趣，所以整理了一个帖子和大家分享。希望对你有帮助。
这些方法使用了若干 API 来简化操作，但是有些方法并不是很优雅，所以本文主要是教 API 技巧！

## 一.日期处理

1.  **判断日期是否正确。**
    该方法用于检查给定日期是否有效。

```
const isDateValid = (...val) => !Number.isNaN(new Date(...val).valueOf());isDateValid("December 27, 2022 13:14:00");  // true
```

**2。计算两个日期之间的间隔。**
此方法用于计算两个日期之间的间隔。

```
const dayDif = (date1, date2) => Math.ceil(Math.abs(date1.getTime() - date2.getTime()) / 86400000)

dayDif(new Date("2022-08-27"), new Date("2022-12-25"))  // 120
```

离圣诞节还有 120 天

**3。确定日期属于一年中的哪一天。**
该方法用于检测给定日期在一年中的哪一天。

```
const dayOfYear = (date) => Math.floor((date - new Date(date.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);dayOfYear(new Date());   // 239
```

2022 年已经过去了 239 天

**4。格式化时间**
这个方法可以用来将时间转换成 hh: mm: ss 格式。

```
const timeFromDate = date => date.toTimeString().slice(0, 8);

timeFromDate(new Date(2021, 11, 2, 12, 30, 0));  // 12:30:00
timeFromDate(new Date());  // now time 09:00:00
```

## 二。字处理

1.  **字符串的首字母大写**
    该方法用于将字符串的首字母大写。

```
const capitalize = str => str.charAt(0).toUpperCase() + str.slice(1)capitalize("hello world")  // Hello world
```

**2。翻转字符串**
这个方法用来翻转一个字符串并返回翻转后的字符串。

```
const reverse = str => str.split('').reverse().join('');reverse('hello world');   // 'dlrow olleh'
```

**3。**随机字符串
这个方法用来生成一个随机字符串。

```
const randomString = () => Math.random().toString(36).slice(2);randomString();
```

4.字符串截断
这个方法将一个字符串截断到指定的长度。

```
const truncateString = (string, length) => string.length < length ? string : `${string.slice(0, length - 3)}...`;truncateString('Hi, I should be truncated because I am too loooong!', 36)   // 'Hi, I should be truncated because...'
```

**5。从一个字符串中移除 HTML**
这个方法用来从一个字符串中移除 HTML 元素。

```
const stripHtml = html => (new DOMParser().parseFromString(html, 'text/html')).body.textContent || '';
```

## 三。阵列处理

1.  **从数组中删除重复项**
    这个方法用于从数组中删除重复项。

```
const removeDuplicates = (arr) => [... .new Set(arr)];console.log(removeDuplicates([1, 2, 2, 3, 3, 4, 4, 5, 5, 6]));
```

**2。确定数组是否为空。**
该方法用于判断一个数组是否为空数组。它返回一个布尔值。

```
const isNotEmpty = arr => Array.isArray(arr) && arr.length > 0;isNotEmpty([1, 2, 3]);  // true
```

3.合并两个数组
你可以用以下两种方法来合并两个数组:

```
const merge = (a, b) => a.concat(b);const merge = (a, b) => [. . a, . . b];
```

## 四。数字运算

1.  **判断一个数是奇数还是偶数**这个方法用来判断一个数是奇数还是偶数。

```
const isEven = num => num % 2 === 0;isEven(996);
```

**2。得到一组数字的平均值**

```
const average = (.. .args) => args.reduce((a, b) => a + b) / args.length;average(1, 2, 3, 4, 5); // 3
```

**3。从两个整数中确定随机整数。**
这个方法用来得到两个整数之间的一个随机整数。

```
const random = (min, max) => Math.floor(Math.random() * (max — min + 1) + min);random(1, 50);
```

**4。**四舍五入到指定的位数
该方法用于将一个数字四舍五入到指定的位数。

```
const round = (n, d) => Number(Math.round(n + “e” + d) + “e-” + d)round(1.005, 2) //1.01
round(1.555, 2) //1.56
```

## 动词 （verb 的缩写）颜色处理

1.  **RGB 转十六进制转换机制**
    该方法将一个 RGB 颜色值转换成十六进制值。

```
const rgbToHex = (r, g, b) => "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1);rgbToHex(255, 255, 255);  // '#ffffff'
```

**2。随机选择一种十六进制颜色。**
这个方法用来获得一个随机的十六进制颜色值。

```
const randomHex = () => `#${Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, "0")}`;randomHex();
```

## 不及物动词浏览器操作

1.  **将内容复制到剪贴板**
    该方法使用 navigator.clipboard.writeText 将文本复制到剪贴板。

```
const copyToClipboard = (text) => navigator.clipboard.writeText(text);copyToClipboard("Hello World");
```

**2。移除所有 cookie**该方法通过使用 document.cookie 来访问 cookie 并清除网页上存储的所有 cookie

```
const clearCookies = document.cookie.split(';').forEach(cookie => document.cookie = cookie.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date(0).toUTCString()};path=/`));
```

**3。检索选择的文本**
这个方法通过内置的 getSelection 属性获取用户选择的文本。

```
const getSelectedText = () => window.getSelection().toString();getSelectedText();
```

**4。确定它是否处于黑暗模式。**
该方法用于检测当前环境是否处于黑暗模式。它是一个布尔值。

```
const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matchesconsole.log(isDarkMode)
```

**5。导航到页面顶部。**
此方法用于回到页面顶部。

```
const goToTop = () => window.scrollTo(0, 0);goToTop();
```

**6。确定当前选项卡是否处于活动状态。**
该方法用于检查当前页签是否处于活动状态。

```
const isTabInView = () => !document.hidden;
```

**7。确定当前设备是否是 Apple 设备。** 该方法用于检查当前设备是否为苹果设备。

```
const isAppleDevice = () => /Mac|iPod|iPhone|iPad/.test(navigator.platform);isAppleDevice();
```

**8。是否滚动到页面底部？**
该方法用于判断页面是否在底部。

```
const scrolledToBottom = () => document.documentElement.clientHeight + window.scrollY >= document.documentElement.scrollHeight;
```

9。重定向到一个 URL这个方法用来重定向到一个新的 URL。

```
const redirect = url => location.href = urlredirect("[https://www.google.com/](https://www.google.com/)")
```

10。打开浏览器打印框。
该方法用于打开浏览器的打印框。

```
const showPrintDialog = () => window.print()
```

## 七。其他操作

1.  **随机布尔值**
    该方法返回一个随机布尔值。使用 Math.random()，您可以从 0–1 中获得一个随机数，并将其与 0.5 进行比较，以有一半的概率获得 true 或 false 值。

```
const randomBoolean = () => Math.random() >= 0.5;randomBoolean();
```

**2。切换变量**
两个变量的值可以交换，无需使用第三个变量，使用如下形式。

```
[foo, bar] = [bar, foo];
```

**3。获取变量的类型。**
该方法用于获取变量的类型。

```
const trueTypeOf = (obj) => Object.prototype.toString.call(obj).slice(8, -1).toLowerCase();
trueTypeOf(‘’); // string
trueTypeOf(0); // number
trueTypeOf(); // undefined
trueTypeOf(null); // null
trueTypeOf({}); // object
trueTypeOf([]); // array
trueTypeOf(0); // number
trueTypeOf(() => {}); // function
```

**4。华氏到摄氏温度转换**
该方法用于摄氏和华氏之间的转换。

```
const celsiusToFahrenheit = (celsius) => celsius * 9/5 + 32;
const fahrenheitToCelsius = (fahrenheit) => (fahrenheit — 32) * 5/9;
celsiusToFahrenheit(15); // 59
celsiusToFahrenheit(0); // 32
celsiusToFahrenheit(-20); // -4
fahrenheitToCelsius(59); // 15
fahrenheitToCelsius(32); // 0
```

**5。检测对象是否为空**
该方法用于检测一个 JavaScript 对象是否为空。

```
const isEmpty = obj => Reflect.ownKeys(obj).length === 0 && obj.constructor === Object;
```

***欢迎关注我上***[***Twitter***](https://twitter.com/yanghui0324)*[***LinkedIn***](https://www.linkedin.com/in/hui-yang-075076245/)***，以及***[***GitHub******！***](https://github.com/guchen-yh)*

*写作一直是我的激情所在，它给了我帮助和激励他人的快乐。如果您有任何问题，请随时联系我们！*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW)*