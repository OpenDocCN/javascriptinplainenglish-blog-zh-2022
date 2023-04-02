# JavaScript 面试问题

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-one-must-know-2e85f940644a?source=collection_archive---------3----------------------->

## 第 2 章:JavaScript 面试必答问题

![](img/879bc3e4feee2ef41133d3bbfa3a7746.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是世界上最流行的编程语言，被广泛用于 web 开发。具有 JavaScript 背景的开发人员可以很容易地接触到 React 等前端库。

这使得 JavaScript 成为专业人士的必备语言。由于 JavaScript 的广泛使用，它为新生/专业人士提供了大量的工作机会。如果你正在准备 JavaScript 面试，下面是你必须知道的问题列表。

**1。map 和 forEach 的区别&什么是过滤函数？**

**ForEach**

`forEach()`方法接收一个函数作为参数，并对每个元素应用相同的代码。它不会返回任何内容，只是将条件应用于每个元素。它不会改变原始数组。

**地图**

`map()`方法接收一个函数作为参数，类似于 forEach，map 将对每个元素应用代码并返回一个全新的数组。它不会改变原始数组。

**过滤器**

`filter()`方法接收一个函数作为参数。它对数组中的每个元素运行函数。它将返回满足应用条件的新数组。它不会改变原始数组。

**差异**

*   `map()`和`forEach()`的区别是它的返回值。`map()`会根据应用的条件返回一个**新数组**，而`forEach()`不会返回任何东西。`forEach()`返回**未定义的**。
*   如果您有修改当前数组的需求，并且期望修改后的数组，那么您应该选择`map()`。如果只是想迭代数组，那么可以使用`forEach()`。
*   由于`forEach()`返回 undefined，所以不能附加`filter()`等其他函数。你可以用`map()`轻松应用`filter()`。

```
//forEachvar Language = ['React','Javascript','HTML','CSS'];
Language.forEach(function(language){ console.log(language); }); 
```

```
 //map var List = [10,12,15,30];
  var updatedList = List.map(function(list){ return list * 2 }); console.log("original List" ,List)  //Original array not Modified
  console.log("Updated List" , updatedList) //Returns new array 
```

```
//filtervar List = [10,12,15,30];
var updatedList = List.filter(function(list){ return list %  2 == 0  });

console.log("original List" ,List)  //Original array not Modified
console.log("Updated List" , updatedList) //Returns new array
```

**2。JavaScript 中的 Rest 参数是什么？**

Rest 参数是 ES6 的特色之一。Rest 可以与 ***【剩余全部】*** 相关联，以便于理解。Rest 收集所有剩余的元素，并将它们组合成一个数组。

让我们通过下面的例子了解更多。在 JavaScript 中，我们可以调用带有任意数量参数的函数，而不管函数声明中接受的参数数量。

**3。JavaScript 中什么是变量提升？**

**JavaScript 中的提升**允许我们在声明变量之前使用它们。这是因为在 JavaScript 中，所有的声明都被移到了作用域的顶部。

例如，如果您在任何函数中使用变量，在编译阶段，JavaScript 引擎会将它们移动到函数的顶部。

需要注意的一点是**只提升声明，不提升初始化**。

对于变量和常数，我们使用 var，let 和 const。var 关键字默认初始化为**未定义**。因此，我们可以先声明 var，然后再初始化它，但是 let 和 const 就不是这样了。如果 let 和 const 没有用任何值初始化，它们会抛出一个错误。如前所述，只有声明被提升，因此 let 和 const 不允许提升。

Variable hoisting Example

**4。JavaScript 中的块作用域和全局作用域是什么？**

*   **块作用域**适用于在{}包围的任何块内声明的变量。
*   **全局作用域**将应用于在任何块或函数之外声明的变量。

问这个问题的主要目的是检查 let、var 和 const 的**范围。**

*   如果在函数外声明，Var 是全局范围的，如果在函数内声明，它将是函数范围的。
*   **设**和**常量**是块范围的，即在{}内部。

**5。let，const，var 有什么区别？**

**ECMA 版:**
在 ES5 中引入 Var。在 ES6 中引入了 Let 和 const

**作用域:**
如果在函数外部声明，Var 就是全局作用域。如果在函数中声明，它将是函数范围的。Let 和 const 是块范围的，即在{}内部

**提升:**Var 变量被提升到其作用域的顶部。Let 和 const 变量可以被提升，但是我们不能访问它们，因为它们需要被初始化为某个值。在 JavaScript 中，只提升声明而不提升初始化，因此我们不能对 let 和 const 使用提升。

**修改和重新声明:**
Var 变量可以直接更新和重新声明。
Let 变量可以更新，但不能重新声明。常量不能更新和重新声明。

用 const 声明的变量不是**常量/固定**。它们可以变异。比如 const numnum++
我们不能直接更新但是可以变异。

```
 var userName = "TnS_User"
 userName = "TnS_User1"; console.log(userName)   * //TnS_User1*
 var userName = "TnS_User_redeclaration"
 console.log(userName)  *//TnS_User_redeclaration*
```

```
 let userName = "TnS_User"
  userName = "TnS_User1"; console.log(userName)   * //TnS_User1*
 let userName = "TnS_User_redeclaration"
 console.log(userName) *//Uncaught SyntaxError: Identifier 'userName' has already been declared" * 
```

```
const userName = "TnS_User"
userName = "TnS_User1";console.log(userName)    //Uncaught TypeError: Assignment to constant variable."const userName = "TnS_User_redeclaration"
console.log(userName) //Uncaught SyntaxError: Identifier 'userName' has already been declared"
```

**6。ES6 有什么特点？**

ES6 的主要特性如下:

*   承诺
*   箭头功能
*   let 关键字
*   const 关键字
*   多行字符串
*   休息和伸展(…)

**7。回调和承诺有什么区别？**

**回调:**

Callback 是作为参数传递给另一个函数的函数，当它符合所应用的条件时将被调用。回调函数主要用于异步调用的情况。当将函数作为参数传递时，请确保不要使用括号。

**承诺:**

承诺提供了一种更干净的方式来处理异步操作。正如诺言这个词所暗示的，它要么在未来被遵守和履行，要么被打破。JavaScript 中的 Promise 有三种状态——已解决、待定和已拒绝。

```
 //Callback
        function Tns(userName, callbackFun) {
          console.log('User Name -' + ' ' + userName);
          callbackFun();
        }
        function callbackFun() {
          console.log('I am TnS_User');
        }
        Tns('TnS_User', callbackFun);
```

```
 //Promise Syntax
        const TnsPromise = new Promise((resolve, reject) => {  
              // condition
          });
```

本文到此为止。如果你觉得这篇文章有帮助，那么请检查其他文章。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***