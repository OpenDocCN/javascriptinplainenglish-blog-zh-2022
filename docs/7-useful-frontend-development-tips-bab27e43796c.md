# 7 个有用的前端开发技巧

> 原文：<https://javascript.plainenglish.io/7-useful-frontend-development-tips-bab27e43796c?source=collection_archive---------9----------------------->

## 1.节流，2。切换全屏，3。UUid，4。时间操作，5。`Object.keys({})`，6。转换为布尔值，7。用对象传递参数

![](img/2638b92f0620f9e064710e657db82129.png)

**这里我们整理了 7 个前端小技巧，一看就熟悉，非常实用。让我们来看看。**

## **1。节流**

对于节流，大部分朋友应该一看就懂，这里就不赘述了。让我们直接看对应的代码:

```
export const throttle = (() => {let last = 0return (callback, wait = 800) => {let now = +new Date()if (now - last > wait) {callback()last = now}}})()
```

## **2。打开全屏&关闭全屏**

对于全屏的性能提升，我们来看看开启全屏和关闭全屏的不同方式。

```
export const launchFullscreen = (element) => {if (element.requestFullscreen) {element.requestFullscreen()} else if (element.mozRequestFullScreen) {element.mozRequestFullScreen()} else if (element.msRequestFullscreen) {element.msRequestFullscreen()} else if (element.webkitRequestFullscreen) {element.webkitRequestFullScreen()}}export const exitFullscreen = () => {if (document.exitFullscreen) {document.exitFullscreen()} else if (document.msExitFullscreen) {document.msExitFullscreen()} else if (document.mozCancelFullScreen) {document.mozCancelFullScreen()} else if (document.webkitExitFullscreen) {document.webkitExitFullscreen()}}
```

## **3。UUid**

一看到这个标题，很多同事肯定会问，UUid 一般不是后端生成的吗？是的，这是毫无疑问的，我们来看看:

```
export const uuid = () => {const temp_url = URL.createObjectURL(new Blob())const uuid = temp_url.toString()URL.revokeObjectURL(temp_url)return uuid.substring(uuid.lastIndexOf('/') + 1)}
```

## **4。时间操作**

对于时间操作，在我和大家的交流以及我自己的项目经验中，我觉得应该没有必要自己写很多代码，这里推荐使用 Day.js。
**至于 Day.js** ，这里简单介绍一下:它是一个轻量级的 JavaScript 时间和日期处理库，所以需要下载、解析和执行的 JavaScript 更少，把更多的时间留给代码。

## **5。对象为空**

对于物体判断，一般用什么方案？下面是一个使用`Object.keys({})`的小技巧。

```
Object.keys({}).length // 0
Object.keys({key: 1}).length // 1
```

## **6。转换为布尔值**

类型转换，“！!"，就这么简单。

```
!!fine // false!!"good"     // true!!null      // false!!No       // false
```

## 7.用对象传递参数

你们一般是怎么传递参数的？作为一个前端工程师，你必须能够想到你需要把参数打包成一个对象，然后传递，否则你将无法理解这种无穷无尽的有序的参数。

```
function getItem(price, quantity, name, description) {}getItem(15, undefined, 'green', 'color')function getItem(args) {const {price, quantity, name, description} = args}getItem({name: 'green',price: 10,quantity: 1,description: 'color'})
```

**感谢您的阅读，期待您的关注，让我们共同进步。**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***