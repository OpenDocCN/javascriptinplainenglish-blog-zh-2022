# JavaScript 开发人员必须学习的 10 个工具(避免重复发明轮子)

> 原文：<https://javascript.plainenglish.io/10-must-learn-tools-for-javascript-devs-to-avoid-reinventing-the-wheel-5ffae566bbfb?source=collection_archive---------1----------------------->

![](img/9e037722a5d801654d0014dcf4ef76f6.png)

## 回到顶端

```
const bindTop = () => {
       // Method 1: This works, but it doesn't work very well
       window.scrollTo(0, 0)
       document.documentElement.scrollTop = 0;

      // Method 2: Scrolling through the timer will be visually smoother, without much lag effect
      const timeTop = setInterval(() => {
        // to control his sliding distance
        document.documentElement.scrollTop = scrollTopH.value -= 50
        // Remember to clear the timer(*) when swiping to the top
        if (scrollTopH.value <= 0) {
          clearInterval(timeTop)
        }
      }, 10)
    }
```

## 复制文本

```
const copyText = (text) => {
        // clipboardData Copy what you need on the page to the clipboard
        const clipboardData = window.clipboardData
        if (clipboardData) {
          clipboardData.clearData()
          clipboardData.setData('Text', text)
          return true
        } else if (document.execCommand) {  // Note that document.execCommand is deprecated but some browsers still support it. Remember to check the compatibility when using it
          // Get the content to be copied by creating a dom element 
          const el = document.createElement('textarea')
          el.value = text
          el.setAttribute('readonly', '')
          el.style.position = 'absolute'
          el.style.left = '-9999px'
          document.body.appendChild(el)
          el.select()
          // Copy the current content to the clipboard
          document.execCommand('copy')
          // delete el node
          document.body.removeChild(el)
          return true
        }
        return false
      }
      copyText('hello!') // ctrl + v = copyText  | true
```

## 去抖/节流

基本介绍

*   去抖:在指定时间内频繁触发事件，以最后一次触发为准
*   节流:事件在指定时间内频繁触发，但仅触发一次

有许多应用场景，例如:

去抖:输入搜索，当用户继续输入内容时，使用防抖减少请求次数，节省请求资源

节流:现场一般是按钮点击。一秒钟内点击 10 次将启动 10 个请求。节流后，1 秒内点击多次，只会触发一次。

让我们实施

```
// debounce
    // fn is the function that needs debounce, delay is the timer time
    function debounce(fn,delay){
        let timer =  null  // for saving the timer
        return function () { 
            // If the timer exists, clear the timer and restart the timer
            if(timer){
                clearTimeout(timeout);
            }
            //Set a timer and execute the actual function to be executed after a specified time
            timeout = setTimeout(() => {
               fn.apply(this);
            }, delay);
        }
    }

    // throttle
    function throttle(fn) {
      let timer = null; // First set a variable, when the timer is not executed, the default is null
      return function () {
        if (timer) return; // When the timer is not executed, the timer is always false, and there is no need to execute it later
        timer = setTimeout(() => {
          fn.apply(this, arguments);
           // Finally, set the flag to true after setTimeout is executed (key)
           // Indicates that the next cycle can be executed
          timer = null;
        }, 1000);
      };
    }
```

## 过滤特殊字符

```
function filterCharacter(str){
        // First set a mode
        let pattern = new RegExp("[`~!@#$^&*()=：”“'。，、？|{}':;'%,\\[\\].<>/?~！@#$……&*（）&;—|{ }【】‘；]")
        let resultStr1 = "";
        for (let j= 0; j< str.length; j++) {
            // Mainly through replace, pattern rules to replace characters with empty and finally spliced in resultStr1
            resultStr1 = resultStr1 + str.substr(j, 1).replace(pattern, '');
        }
        // When the loop ends, return the final result resultStr1
        return resultStr1;
    }

    // Example
    filterCharacter('gyaskjdhy12316789#$%^&!@#1=123,./[') // Result: gyaskjdhy123167891123
```

## 常用的常规判断

```
// Check 2-9 characters, false if not matched, true if matched
    const validateName = (name) => {
      const reg = /^[\u4e00-\u9fa5]{2,9}$/;
      return reg.test(name);
    };// Verify phone number
    const validatePhoneNum = (mobile) => {
      const reg = /^1[3,4,5,6,7,8,9]\d{9}$/;
      return reg.test(mobile);
    };// Check passwords consisting of 6 to 18 uppercase and lowercase alphanumeric underscores
    const validatePassword = (password) => {
      const reg = /^[a-zA-Z0-9_]{6,18}$/;
      return reg.test(password);
    };
```

## 初始化数组

```
// The fill() method is a new method in es6 that fills the array with the specified element, which is actually initializing the array with the default content
    const arrList = Array(6).fill()
    console.log(arrList)  // What is printed here is['','','','','','']
```

## 将 RGB 转换为十六进制

```
function getColorFun(r,g,b) {
       return '#' + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)
    }

    getColorFun(178,232,55) // The output here is #b2e837
```

## 检查它是否是一个函数

```
// Detecting whether it is a function In fact, it is good to write isFunction directly after writing, so as to avoid repeated writing judgments
    const isFunction = (obj) => {
        return typeof obj === "function" && typeof obj.nodeType !== "number" && typeof obj.item !== "function";
    };
```

## 检查它是否是安全数组

```
// Check if it is a safe array, if not, return an empty array here with the isArray method
  const safeArray = (array) => {
    return Array.isArray(array) ? array : []
  }
```

## 检查对象是否是安全对象

```
//First of all, we need to determine whether the current object is a valid object
    const isVaildObject = (obj) => {
        return typeof obj === 'object' && !Array.isArray(obj) && Object.keys(obj).length
    }
    // The above function is used directly here. If it is valid, it will return itself, and if it is invalid, it will return an empty object.
    const safeObject = obj => isVaildObject(obj) ? obj : {}
```

最后，如果以上文章有什么不清楚的地方，请指出来，希望能在一定程度上帮助到大家，也期待您的关注，谢谢支持~

[](/understand-es6-in-20-minutes-8ab8f958e379) [## 在 20 分钟内了解 ES6

### 不要让任何人告诉你:“你不知道 ES6 怎么敢说你知道 JS！”

javascript.plainenglish.io](/understand-es6-in-20-minutes-8ab8f958e379) [](/12-common-javascript-functions-you-need-to-know-3d3a3ab712fc) [## 你需要知道的 12 个常见 JavaScript 函数

### 本文收集了日常开发中非常常用的 12 个函数。其中一些可能很复杂…

javascript.plainenglish.io](/12-common-javascript-functions-you-need-to-know-3d3a3ab712fc) [](/how-to-better-use-conditional-judgment-in-javascript-5aa1d2981e08) [## 如何在 JavaScript 中更好地使用条件判断

### 本文花很短的时间介绍如何用 JavaScript 编写更简单的条件判断，帮助您…

javascript.plainenglish.io](/how-to-better-use-conditional-judgment-in-javascript-5aa1d2981e08) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****