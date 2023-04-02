# (值得收集)你应该学习的 6 个有用的算法和代码快捷方式

> 原文：<https://javascript.plainenglish.io/6-useful-algorithms-code-shortcuts-you-should-learn-49f04ae61eb8?source=collection_archive---------15----------------------->

## 学习成为更好的开发者的算法和代码捷径。

![](img/924ff536425311a5869776d3bf6dd129.png)

以下是你可以使用的 6 种算法和技巧:

1.  **如何找到数组中缺失的数字**

先来看看下面这段代码，然后大家一起讨论一下:

```
Input: [1, 2, 4,5, 6,]Output: 3const find_missing = function(input) {let n = input.length + 1;let sum = 0;for (let i in input) {sum += input[i];}return Math.floor((n * (n + 1)) / 2) - sum;};
```

看完上面的算法代码，我们一起讨论几个问题:

(1)如果数组中少了两个数，还能这样用吗？如果不能用，怎么办？

***解释:*** 这个答案是否定的。上述方法只有从 1 开始，用等差数列求和，再减去和，才能得到正确答案。

(2)如果数组不是从 1 开始，这个方法可行吗，如果不可行，怎么解？

***解释:*** 不从 1 开始，就不行。看看下面的方法:

```
const find_missing = function(input: number[]) {const a1 = input[0];const an = input[input.length - 1];const initSum = (a1+an)*(input.length + 1) / 2;let sum = 0;for (let i in input) {sum += input[i];}return Math.floor((initSum)) - sum;};
```

(3)你有其他更好的方式或方法适合你吗？

***解释:*** 也有很多同学提到了以下方法:先去掉重复的，然后从小到大排序，再遍历，观察数字和索引是否能匹配，如果不匹配，数字-1 就是缺失的数字

**2。如何反转整数**

事不宜迟，让我们直接看下面的代码:

```
Input: num = 345Output: 543Input: num = -345Output: -543const reverse = function(num) {let result = 0;while (num !== 0) {result = result * 10 + num % 10;// Math.trunc()num = Math.trunc(num / 10);}if (result > 4**53|| result < -(4**53)) return 0;return result;};
```

看了上面的逆序整数的写法，我们一起来思考一下下面的写法。大家一起想想，这样的方式是不是更好？然后里面有负数，那么怎么处理呢？然后我们将看下面的方式:

```
let reverse=(num)=>{
return Number(String(~~num).split('').reverse().join(''))
}
```

![](img/cd162bfb08c00d21ab594a50940f45a4.png)

Photo by [Maxim Hopman](https://unsplash.com/@nampoh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**3。什么是字符串乘法？**

对于字符串乘法，我们来做一个简单的，如下:

```
Input: num1 = "1", num2 = "2"Output: "2"const multiply = function(num1, num2) {if (num1 == 0 || num2 == 0) return '0';const result = [];for (let a = num1.length - 1; a >= 0; a--) {for (let b = num2.length - 1; b >= 0; b--) {const p1 = a + b;const p2 = a + b + 1;const sum = (result[p2] ?? 0) + num1[a] * num2[b];result[p1] = (result[p1] ?? 0) + Math.floor(sum / 10);result[p2] = sum % 10;}}result[0] == 0 && result.shift();return result.join('');};
```

看了字符串相乘，很多朋友说运算结果会自动转换。你的测试结果是什么？欢迎在评论区留言讨论。

**4。让我们一起来看看克隆的数组**
以下缩写在我看来更简单:

```
let color = ['red', 'green','blue ','yellow '];let cloneFruits = [...color];  // <-- hereconsole.log( clonecolor );//=> ["red", "green", "blue", "yellow"]
```

当然，在这里，我们也可以使用 Array 中的 *slice()* 方法轻松克隆*数组*。这种方法比较常见，就不赘述了，不过大家可以想想平时是怎么写的。

**5。一起看一下 for 循环**
为了简化代码，我会用它们 for…of 语句来实现，因为这样代码会更简洁。下面我们一起讨论一下写作方法:

```
let color = ['red', 'green','blue ','yellow '];// Using for...of statementfor (let fruit of color) {console.log( color );}//=> red//=> green//=> blue//=> yellow
```

当我第一次开始编程时，我通常使用 for 循环来遍历数组，这样会有点复杂。你们用哪种方法？我们可以一起讨论。

![](img/6e1a33e16c41600818123d3badc5b653.png)

Photo by [Henry & Co.](https://unsplash.com/@hngstrm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**6。什么是数组析构？**
在处理数组的时候，很多时候，我们大多数人都会把数组“解包”成很多变量。其实这个方法太复杂了。在这里，让我们学习一下析构赋值，以及如何使用一行代码达到相同的结果:

```
let pears = ['greenpear','yellowpear'];let [greenPear, yellowPear] = pears;  // <-- hereconsole.log( greenPear );    //=> greenpearconsole.log( yellowPear );  //=> yellowpear
```

看完上面的代码，你也可以思考一下，在使用数组处理的“解包”方法时，哪个更符合你平时的使用。

**感谢您的阅读，期待您的关注，让我们一起进步。**

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*