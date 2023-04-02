# JavaScript 隐藏的力量:不用 BigInt 就能添加大数字

> 原文：<https://javascript.plainenglish.io/javascripts-hidden-power-adding-big-numbers-without-bigint-3a35c16fe710?source=collection_archive---------20----------------------->

## 毁灭 2022

## 查看处理大整数的替代方法

![](img/4fdeb3422c575c7b7e7dc68df82c96e4.png)

我们已经到达了这场灾难的终点 2022 年。为了完美地结束事情，CodeWars 为我提出了一个 4 级 kyu 问题。像任何困难的问题一样，它表现得很简单，就像 2 加 2。这都是关于和的，但是是非常大，非常巨大，非常巨大的数字的和。这也是 JavaScript 在处理如此大的数字时的局限性。最后，这是关于回忆我们小时候是如何做算术的。

# 问题是:把大数字相加

链接到[形](https://www.codewars.com/kata/525f4206b73515bffb000b21)

![](img/f1948c9166c98b4ac461ac16ee9da5cd.png)

我们需要对大数字求和，我们需要你的帮助。

编写一个返回两个数之和的函数。输入数字是字符串，函数必须返回一个字符串。

**举例**

```
add("123", "321"); -> "444"
add("11", "99");   -> "110"
```

**注意事项**

*   输入的数字很大。
*   输入是一个只有数字的字符串
*   这些数字是积极的
*   你不能使用内置的大整数库(BigInt)
*   你不能使用其他库

# 人工智能解决方案

![](img/4b4019196e96f9bee117cec75b1880d1.png)

我承认我在黑暗中跌跌撞撞。问题是我不能使用 BigInt，这是最合理也是最有效的解决方案。在网上搜索了一下没有找到解决方案后，我试着向 ChatGPT 寻求一些想法。它给了我这个解决方案:

```
function add(a, b) {
  // Initialize result
  let result = "";

  // Initialize digit sum
  let sum = 0;

  // Initialize carry
  let carry = 0;

  // Add digits from right to left
  for (
    let i = a.length - 1, j = b.length - 1;
    i >= 0 || j >= 0 || carry > 0;
    i--, j--
  ) {
    // Get digits from both numbers
    let x = 0;
    let y = 0;
    if (i >= 0) {
      x = a[i] - "0";
    }
    if (j >= 0) {
      y = b[j] - "0";
    }

    // Add digits and carry
    sum = x + y + carry;

    // Update carry
    carry = Math.floor(sum / 10);

    // Update result
    result = (sum % 10) + result;
  }

  // Return result
  return result;
}
```

这段代码定义了一个函数 add，它接受两个大整数作为字符串，并将它们的和作为字符串返回。该函数使用以下步骤对两个大整数执行加法运算:

1.  它将变量 result 初始化为一个空字符串，该字符串将用于存储加法的结果。
2.  它将变量 sum 初始化为 0，用于存储当前相加的数字的总和。
3.  它将变量 carry 初始化为 0，这将用于存储前一次加法运算的结转值。
4.  然后，它从右向左遍历两个大整数的数字。
5.  对于每次迭代，它从两个大整数中获取当前位数。如果当前索引超出了大整数的长度，则将该数字设置为 0。
6.  然后，它将数字和结转值相加，通过将总和除以 10 并取结果的下限来更新结转值。
7.  然后，它通过将总和除以 10 后的余数加到字符串的左侧来更新结果变量。
8.  循环继续，直到处理完所有数字或结转值变为 0。
9.  最后，该函数返回结果变量，该变量包含两个大整数之和作为一个字符串。

# 我的解决方案

![](img/37f9aedfe18c44ff0fa81751d177df68.png)

提议的解决方案很好，我会很满意的。但是我不喜欢。我不喜欢它，因为用这种方式找到解决方案有点像作弊。最重要的是，它剥夺了发现和研究的乐趣。

所以，我可以尝试提出自己的解决方案。这是:

```
const sum = (x, y = 0, z = 0) => Number(x) + Number(y) + Number(z);
const dec = (x) => (Number(x) >= 10 ? 1 : 0);
const unit = (x) => (Number(x) >= 10 ? Number(x) - 10 : Number(x));

const add = (a, b) => {
  const max = a.length >= b.length ? a : b;
  const min = a.length >= b.length ? b : a;

  const revA = [...max].reverse();
  const revB = [...min].reverse();

  let decimal = 0;
  const revResult = revA.map((x, i, arr) => {
    const result = sum(x, revB[i], decimal);
    decimal = dec(result);
    return unit(result);
  });

  return `${decimal > 0 ? decimal : ""}` + revResult.reverse().join("");
};
```

这段代码定义了一个函数`add`,它接受代表正整数的两个字符串`a`和`b`,并返回代表这两个数字之和的字符串。

该函数首先确定两个输入字符串的最大长度，并将较长的字符串赋给变量`max`，将较短的字符串赋给变量`min`。然后，它使用 spread 运算符(`...`)创建字符串的反向版本，并将它们分别赋给变量`revA`和`revB`。

接下来，该函数定义一个变量`decimal`，并将其初始化为`0`。然后，它使用`revA`上的`map`方法迭代数组中的每个元素，并对其应用`sum`函数，传入来自`revB`的相应元素和 decimal 的当前值。`sum`函数返回其三个参数的和，这些参数都使用 Number 函数转换成数字。

然后将`sum`函数的结果传递给`dec`函数，如果结果大于或等于`10`则返回`1`，否则返回`0`。然后将该值赋给十进制变量。sum 函数的结果也被传递给 unit 函数，如果大于或等于`10`，则返回结果减去`10`，否则返回结果本身。

最后，该函数将`decimal`的值(如果它大于`0`)与`revResult`数组的反转版本连接起来，这是通过对其调用 reverse 方法获得的。然后结果作为字符串返回。

例如，如果输入字符串是`"123"`和`"456"`，函数将返回字符串`"579"`，这是两个数的和。

基本上，我建立了一个可以自动累加数字的函数，就像我们在学校里学到的那样。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2022 年 12 月 23 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/devadvent-2022-23-adding-big-numbers/)**。**

## *更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。*

**报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)**

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*