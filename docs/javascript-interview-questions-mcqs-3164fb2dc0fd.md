# JavaScript 面试问题

> 原文：<https://javascript.plainenglish.io/javascript-interview-questions-mcqs-3164fb2dc0fd?source=collection_archive---------4----------------------->

## 多项选择题列表，帮助你准备技术 JavaScript 能力倾向测试。

![](img/1c7eed0eaf46419263c8b4482f88c1a9.png)

Photo by [Artem Sapegin](https://unsplash.com/@sapegin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**JavaScript** 是世界上最流行的编程语言，被广泛用于 web 开发。具有 JavaScript 背景的开发人员可以很容易地接触到 React 等前端库。

这使得 JavaScript 成为专业人士的必备语言。由于 JavaScript 的广泛使用，它为新生/专业人士提供了大量的工作机会。如果你正在准备 JavaScript 面试，下面是你必须知道的问题列表。

下面列出了在不同平台上最常被问到的 JavaScript 问题，这些问题用于进行第一轮筛选。

1.  **JavaScript 是一种单线程语言。**

A.真
B .假

**2。JavaScript 使用？**

A.字面作用域
B .词法作用域
C .函数作用域
D .顺序作用域

**3。以下代码的输出会是什么？**

```
console.log("50" + 50 - 50)
```

A.5000
b . 50
c . 500
d . 505050

**4。下面的输出会是什么？**

```
 function TnS_outer(){
          var a = 10 ;
          function TnS_inner(){
            var b= 10 ;
            return a + b ;
          }
         return TnS_inner();
        }
        console.log(TnS_outer());
```

A.10
B. 20
C .未定义
D .错误

**5。以下哪个陈述是正确的？**

A.splice()改变原始数组，slice()不变。
B. slice()改变原数组，splice()不变。
C. slice()和 splice()都改变原数组。
D. slice()和 splice()都不改变原数组。

6。下面两个代码的输出会是什么？

```
 function TnS_add(a,b)
        {
          return a + b;
        }
        function TnS_spreadadd(...nums){
          var count = 0 ;
          for(let num of nums)
          {
          count += num ;
          }
          return count ;
        }

        console.log(TnS_add(10,20,40) , TnS_spreadadd(10,20,40))
```

A.错误
B. 30，70
C .未定义，70
D. 30，30

**7。执行的顺序是什么？**

```
 console.log("A")
        setTimeout(function(){ console.log("B") }, 0);
        console.log("C")
        setTimeout(function(){ console.log("D") }, 1000);
```

A.
B B C D
C B D A C
D D B A C

为了方便起见，我在这里给出了前 7 个选择题的答案:

![](img/870139923d106c0b044cb2bfb34f0d42.png)

Photo by [Usman Yousaf](https://unsplash.com/@usmanyousaf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

1.  **A**
    **True**
    JavaScript 是单线程语言。JavaScript 只有一个调用栈和一个内存堆。它按照代码定义的顺序执行代码，这意味着 JavaScript 本质上是同步的。当我们从服务器获取数据或使用 ajax 调用时，这种同步特性可能会导致问题。

2. **B**
**词法范围界定。**

3.**A**
**5000**
`console.log("50" + 50 - 50)` ->先“50”+50 =“5050”，然后“5050”-50 将结果变成 5000。这里,+运算符会看到左边的操作数是一个字符串，右边的是一个数字，因此它会将 num 转换为字符串，并在第一个后面追加。负(-)运算符会将字符串视为数字，并进行减法运算。

4.这里出现了词法范围的概念。在 JavaScript 中，嵌套函数可以访问在其外部作用域中声明的变量。`TnS_outer()`在内部函数中创建一个局部变量“a”和函数`TnS_inner().`,我们得到另一个局部变量“b ”,内部函数可以访问它的外部函数变量。因此，我们得到两个变量相加的结果。

5.**一个**
`**splice()**` **改变原阵，** `**slice()**` **则不然。**
通过使用`**splice()**`，我们可以在一个现有的数组中添加或删除项目。它将返回已执行加减运算的新数组。如果没有元素被移除，`splice()`将返回一个**空数组**。

`slice(start ,end)`将**不修改**原数组。它将使用函数调用中提供的起始和结束位置返回一个从当前数组中切片/选择的新数组。它将挑选元素，直到结束，但将排除结束索引。

6.在第一次调用中，我们调用了一个只接受两个参数的函数。这是可能的，因为在 JavaScript 中没有函数参数限制。这里的`Tns_add()`只需要两个参数，它将只选取前两个参数，并将它们相加得到 30。

为了处理这种情况，我们有一个扩展操作符，如`TnS_spreadadd(...nums).`所示。这将把数组元素扩展到个体中，通过使用一个循环，我们可以按照我们的要求对数组元素执行操作。

7.**B**
**A C B D**
这里首先输出的将是 **A** 。之后是延迟 0 秒的`setTimeout()`函数，但不会立即被调用。它之所以会这样，是因为`setTimeout()`是一个**异步**函数。它将创建一个回调，并将被放在一个队列中。一旦另一个代码完成执行，队列上的这些回调将被执行。因此，下一个输出将是 **C** ，之后将是 **B** ，因为计时器值比**d**高

我们现在继续回答其余的问题。

![](img/f041fd258c051b3f096ddf422db5f402.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**8。控制台上会输出什么？**

```
 for(var i=0 ;i<5;i++)
        {
          setTimeout(function(){ console.log(i) }, i);
        }
```

A.0 1 2 3 4
b . 0 0 0 0
c . 5 5 5 5 5
d . 0 5 5 5

9.输出会是什么？

```
 for(let i=0 ;i<5;i++)
        {
          setTimeout(function(){ console.log(i) }, i);
        }
```

A.0 1 2 3 4
b . 0 0 0 0
c . 5 5 5 5 5
d . 0 5 5 5 5

10.`TnS_Traingle`的输出会是什么？

```
 function TnS_Traingle()
        {
          var height = 10 ;
          let base = 20 ;

          var height = 20;
          let base = 30;

          return 0.5*base*height ;
        }
```

A.100
B .语法错误:已经声明了标识符“height”c . 300
d .语法错误:已经声明了标识符“base”

11.`TnS_Rectangle`的返回值会是什么？

```
 function TnS_Rectangle()
        {
          var height = 10 ;
          let base = 20 ;

          if(height  > 5)
          {
            let base = 10 ;
          }

          return base*height ;
        }
```

A.200
B. 100
C .无限循环
D .语法错误:已经声明了标识符“base”

以下是问题 8 至 11 的答案。

![](img/dc7c27cf26343dbe24e724001bfe6630.png)

Photo by [bruce mars](https://unsplash.com/@brucemars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

8.**C
5 5 5 5 5 5**
输出将是 5 乘以 5，因为我们知道 var 具有全局/功能范围，因此每次调用`setTimeout()`回调时，它将拥有 var i 的相同副本。这可以用 let 关键字来处理。

9. **A
0 1 2 3 4**
这里，由于 let 有 block 作用域，它总是有一个不同的值 I，因此将打印 0 1 2 3 4，直到循环结束。

10. **D
语法错误:已经声明了标识符“base”**
上述代码将导致语法错误，因为我们正在重新声明 let 关键字。我们**不能重新声明 let 关键字**，我们只能更新它。var 不会出现此错误，因为 **var 可以重新声明并重新初始化**。

11.**一
200
一**如前所述，**让有一个阻塞范围**。因此，第二个`let base`变量将被视为不同。返回基数*高度时，`base`的值将为 20，因为它将引用第一个`base`变量。

这是我遇到的一些 JavaScript 选择题的列表。我试图根据我的理解和知识来解释。就这样，我们到了这篇文章的结尾。如果你觉得这篇文章有帮助，请不要忘记检查其他文章！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***