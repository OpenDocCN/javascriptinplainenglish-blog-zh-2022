# 如何让旧代码干净清晰

> 原文：<https://javascript.plainenglish.io/how-to-make-old-code-clean-and-clear-44918a318d1c?source=collection_archive---------13----------------------->

## 干净的代码冒险

![](img/9024339170bdfc2ecd85bafa0b37270c.png)

这篇文章的想法是从一个没有考虑干净代码原则的函数开始，用一种干净清晰的方式重写它。整个过程将由测试驱动。

目的是验证一种*的工作方式*，这种方式可以用来重构旧的代码基础并提高它们的质量。

我们将创建一组在不同抽象层次分解原始函数算法的函数，从旧代码中汲取灵感，并尽可能重用它。

此外，我们将跟踪每个新引入的特性覆盖了旧代码的哪些行，以确保我们实现了所有的旧特性。

我们从我在一篇旧文章中描述的一个函数开始:自然排序的高性能比较算法。

这是旧代码:

没错，是晦涩难懂。我们手中力量的阴暗面。
是的，代码不能处理包含前导零的数字部分。但是修改它来处理它们是非常容易的。而且干净的代码重构之后会更容易！

我理想的高级功能如下:

```
**const** *natural_sort_comparison* = **(**a: string, b: string**) =>**
  compare*_chars_or_numbers_of***(**
    a,
    *with_corresponding_char_or_number_of***(**b**)**
  **)**
```

这与维基百科中自然排序的定义非常接近:

> 在计算中，**自然排序顺序**(或**自然排序**)是按照[字母顺序](https://en.wikipedia.org/wiki/Alphabetical_order)对字符串进行的[排序，除了多位数被自动处理，即，就像它们是单个字符一样。](https://en.wikipedia.org/wiki/Collation)

它准确地反映了算法的本质，但包含了一个技术难点:它需要使用一个函数，该函数关闭另一个有效执行任务的函数中的参数 b。

有人可能会说使用闭包会使代码晦涩难懂。所以我会选择一个更简单、不那么优雅的版本:

```
**const** *natural_sort_comparison* = **(**a: string, b: string**)** **=>**
  compare*_chars_or_numbers***(**a, b**)**
```

但是我的最终解决方案将使用我的第一个想法，因为我不认为优雅和复杂会损害清晰。

下面我将使用这三个常量:

```
**const** EQUAL = 0
**const** SMALLER = -1
**const** BIGGER = 1
```

我们的初始测试集将验证循环在字符串 a 的字符上的正确“移植”。出于这个简单的目的，测试字符串只包含字母字符，并且每个字符串都不是另一个字符串的前缀。

```
*test***(**'Basic string comparisons', **() => {**
  expect**(***natural_sort_comparison***(**'abc', 'bc'**))**.toBe**(***SMALLER***)
**  expect**(***natural_sort_comparison***(**'bc', 'abc'**))**.toBe**(**BIGGER**)
**  expect**(***natural_sort_comparison***(** 'abcde', 'abcde'**))**.toBe**(**EQUAL**)**
**))**
```

我们覆盖了原始代码的第 2、3、4、5、24、25 行和部分第 28 行。

代码是这样的:

```
**const** compare*_chars_or_numbers* = **(**a, b**)** **=> {**
  **let** charIndex = 0
  **while (** charIndex < a.lenght **)** **{**
    **const** comparisonResult =
      *compare_one_char_or_number***(**a, b, charIndex**)**
    **if (**comparisonResult !== EQUAL**)** **return** comparisonResult
    charIndex++
  **}**
  **return** EQUAL
**}****const** *compare_one_char_or_number* = **(**a, b, charIndex**)** **=>** **{**
  **const** aCode = a.charCodeAt**(**charIndex**)**
  **const** bCode = b.charCodeAt**(**charIndex**)**
  **return** aCode - bCode
**}**
```

我用*替换了*循环的*,而*是因为在最终代码中，我想将第 3 行的增量的*和第 21 行的增量合并成一条指令。*

下一步是重新组织前缀的解决方案。

这些是附加测试:

```
*test***(**'Strings that are prefixed by the other', **() => {**
  expect**(***natural_sort_comparison***(**'abc', 'abcd'**))**.toBe**(***SMALLER***)
**  expect**(***natural_sort_comparison***(**'abcd', 'abc'**))**.toBe**(**BIGGER**)**
**))**
```

第 6 行和第 28 行的检查应该插入到*compare _ one _ char _ or _ number*函数中，但是我们需要找到一种方法将第 28 行的测试包含到 *a* 元素的循环中:

```
**const** compare*_chars_or_numbers* = **(**a, b**)** **=> {**
  **let** charIndex = 0
  **const** maxComparisonChars = a.length + OneMoreToCheckIfAisPrefixOfB
  **while (** charIndex < maxComparisonChars **)** **{**
    **const** comparisonResult =
      *compare_one_char_or_number***(**a, b, charIndex**)**
    **if (**comparisonResult !== EQUAL**)** **return** comparisonResult
    charIndex++
  **}**
  **return** EQUAL
**}****const** OneMoreToCheckIfAisPrefixOfB = 1
```

现在，该函数必须处理一个超过字符串大小的 charIndex。这不是一个大问题，因为在这种情况下 *chartAt(i)* 返回 *NaN。*还要注意，现在比较相等的字符串，我们得到的 charIndex 超过了两个字符串的大小。

```
**const** *compare_one_char_or_number* = **(**a, b, charIndex**)** **=>** **{**
  **const** aCode = a.charCodeAt**(**charIndex**)**
  **const** bCode = b.charCodeAt**(**charIndex**)**
  **return** *compare_char_codes***(**aCode, bCode**)**
**}****const** *compare_char_codes* = **(**aCode, bCode**)** **=>** **{**
  **if (**are_strings_equal**(**aCode, bCode**))** **return** EQUAL
  **if (**is_the_string_prefix_of_the_other**(**aCode**))** **return** SMALLER
  **if (**is_the_string_prefix_of_the_other**(**bCode**))** **return** BIGGER
  return aCode - bCode
**}****const** is_the_string_prefix_of_the_other =
  charCode **=>** isNaN**(**charCode**)****const** are_strings_equal =
  **(**aCode, bCode**)** **=>** isNaN**(**aCode**)** && isNaN**(**bCode**)**
```

这个改进版本的*compare _ one _ char _ or _ number*覆盖了第 5 行和第 28 行的其余部分。

下一步是处理带有数字部分的字符串。首先要考虑的是*compare _ one _ character _ or _ one _ number*现在可以一次比较多个字符(一个数字可以由多个数字组成)。
在相等的子字符串的情况下，比较的字符数用于递增*compare _ chars _ or _ numbers*中的循环计数器，因此该函数必须向调用者返回两个值。
在这些情况下，一个众所周知的习语(广泛用于 React 挂钩)是返回一个向量并使用 ES6 语法提取值:

```
**const** compare*_chars_or_numbers* = **(**a, b**)** **=> {**
  **let** charIndex = 0
  **const** maxComparisonChars = a.length + OneMoreToCheckIfAisPrefixOfB
  **while (** charIndex < maxComparisonChars **)** **{**
    **const [**comparisonResult, comparedChars**]** =
      *compare_one_char_or_number***(**a, b, charIndex**)**
    **if (**comparisonResult !== EQUAL**)** **return** comparisonResult
    charIndex += comparedChars
  **}**
  **return** EQUAL
**}****const** *compare_one_char_or_number* = **(**a, b, charIndex**)** **=>** **{**
  **const** aCode = a.charCodeAt**(**charIndex**)**
  **const** bCode = b.charCodeAt**(**charIndex**)
  const** comparedChars = 1
  **return [***compare_char_codes***(**aCode, bCode**),** comparedChars]
**}**
```

注意 *charIndex* 递增，直到两个子字符串相等，但是当它们变得不同时 *comparedChars* 不被使用。

单元测试的重新运行确保了变更不会引入中断。

现在我们准备好为带有数字部分的字符串定义测试。我们从长度为 1 的数字部分开始。

```
*test***(**'Strings that are prefixed by the other', **() => {**
  expect**(***natural_sort_comparison***(**'ab2c1', 'ab2c2'**))**.toBe**(***SMALLER***)
**  expect**(***natural_sort_comparison***(**'ab2c2', 'ab2c1'**))**.toBe**(**BIGGER**)**
**))**
```

函数*compare _ one _ char _ or _ number*应区分标准字符和数字序列:

```
**const** *compare_one_char_or_number* = **(**a, b, charIndex**)** **=>** **{**
  **const** aCode = a.charCodeAt**(**charIndex**)**
  **const** bCode = b.charCodeAt**(**charIndex**)
  if (**is_digit**(**aCode**)** && is_digit**(**bCode**)) {
    return** *compare_digits***(**a, b, charIndex**)
  }
  const** comparedChars = 1
  **return [***compare_char_codes***(**aCode, bCode**),** comparedChars**]**
**}****const** *compare_digits* = **(**a, b, charIndex**) => {**
  return [a - b, 1]
}**const** *is_digit* = charCode **=>** charCode>=48 && charCode<=57
```

注意 *is_digit(NaN)* 为 false，所以前缀和相等字符串的处理只发生在 *compare_char_codes* 内部。

*compare _ one _ char _ or _ number*中的两个返回语句有问题:我们混合了两个不同层次的抽象:谁负责返回两个函数值？我们不能从 *compare_digits* 中提取这个责任，所以我们甚至在字母字符的情况下委托它。

```
**const** *compare_one_char_or_number* = **(**a, b, charIndex**)** **=>** **{**
  **const** aCode = a.charCodeAt**(**charIndex**)**
  **const** bCode = b.charCodeAt**(**charIndex**)
  if (**is_digit**(**aCode**)** && is_digit**(**bCode**)) {
    return** *compare_digits***(**a, b, charIndex**)
  }**
  **return** *compare_one_char_code_pair***(**aCode, bCode**)**
**}****const** *compare_one_char_code_pair* = **(**aCode, bCode**) => {
  const** comparedChars = 1
  **return [***compare_char_codes***(**aCode, bCode**),** comparedChars**]
}**
```

*compare _ one _ char _ or _ number*的最终版本也覆盖了旧代码的第 7 行。

下一步是比较不同长度的数量。

```
*test***(**'Strings that are prefixed by the other', **() => {**
  expect**(***natural_sort_comparison***(**'abc2', 'abc11'**))**.toBe**(***SMALLER***)** expect**(***natural_sort_comparison***(**'abc111', 'abc21'**))**.toBe**(**BIGGER**)**
**))**
```

数字越多的数字越大。因此，计算两个字符串中连续数字的个数并比较计数器就足够了。

```
**const** *compare_digits* = **(**a, b, charIndex**) => {**
  **const** aDigits = *number_of_consecutive_digits***(**a, charIndex**)**
  **const** bDigits = *number_of_consecutive_digits***(**b, charIndex**)
  if** **(**aDigits > bDigits**)** **return** [BIGGER]
  **if** **(**aDigits < bDigits**)** **return** [SMALLER]
  // cannot be here for the moment
**}****const** *number_of_consecutive_digits* = **(**str, startIndex**) => {
  let** lastIndex
  **for (**lastIndex=startIndex+1; lastIndex<str.length; lastIndex++**)**
    **if (**!*is_digit***(**str.charCodeAt**(**lastIndex**)))**
      **return** lastIndex - startIndex
  **return** lastIndex - startIndex
**}**
```

好了，现在是最后一步:测试数字部分长度相同的字符串。

```
*test***(**'Strings that are prefixed by the other', **() => {**
  expect**(***natural_sort_comparison***(**'abc12', 'abc12'**))**.toBe**(***EQUAL***)** expect**(***natural_sort_comparison***(**'abc11', 'abc12'**))**.toBe**(***SMALLER***)** expect**(***natural_sort_comparison***(**'abc13', 'abc12'**))**.toBe**(**BIGGER**)**
**))**
```

如果两个数字部分具有相同的长度，只需检查其数字的字符代码顺序。

```
**const** *compare_digits* = **(**a, b, charIndex**) => {**
  **const** aDigits = *number_of_consecutive_digits***(**a, charIndex**)**
  **const** bDigits = *number_of_consecutive_digits***(**b, charIndex**)
  if** **(**aDigits > bDigits**)** **return** [BIGGER]
  **if** **(**aDigits < bDigits**)** **return** [SMALLER]
  **return** compare_equal_length_numbers**(**a, b, charIndex, aDigits**)**
**}****const** compare_equal_length_numbers =
 **(**a, b, startIndex, numberOfDigits**) => {
   for (let** charIndex = startIndex;
        charIndex < startIndex + numberOfDigits;
        charIndex++**) {
     const** aCode = a.charCodeAt(charIndex)
     **const** bCode = b.charCodeAt(charIndex)
     **if (**aCode < bCode**) return** [SMALLER]
     **if (**aCode > bCode**) return** [BIGGER]
 **}
  return** [EQUAL, numberOfDigits]
**}**
```

函数*compare _ equal _ length _ numbers*覆盖旧代码的第 13-18 行，而 *compare_digits* 覆盖第 8-11 行

仅此而已。但是在展示整个重构的代码之前，请记住我在开头说过的话……我更喜欢优雅和复杂的代码。毕竟，闭包是语言的一部分…

```
**const** *natural_sort_comparison* = **(**a: string, b: string**) =>**
  compare*_chars_or_numbers_of***(**
    a,
    *with_corresponding_char_or_number_of***(**b**)**
  **)****const** compare*_chars_or_numbers_of* = **(**a, compare_with_b**)** **=> {**
  **let** charIndex = 0
  **const** maxComparisonChars = a.length + OneMoreToCheckIfAisPrefixOfB
  **while (** charIndex < maxComparisonChars **)** **{**
    **const [**comparisonResult, comparedChars**]** =
      compare_with_b**(**a, charIndex**)**
    **if (**comparisonResult !== EQUAL**)** **return** comparisonResult
    charIndex += comparedChars
  **}**
  **return** EQUAL
**}****const** *with_corresponding_char_or_number_of* = b **=> {
  const** compare_with_b = **(**a, charIndex**) =>** *compare_one_char_or_number***(**a, b, charIndex**)**
  **return** compare_with_b
**}**
```

我只修改了主函数的名称和签名，并在它的主体中调用了对 *compare_with_b* 的调用:一个在 b 上关闭的函数，它调用了*compare _ one _ char _ or _ number*以及所有需要的参数。
一个黑暗的片段在干净的代码天空中幸存下来，允许对顶级函数进行富有表现力的调用。

好了，代码行增加了一倍(考虑到旧清单中没有 skipDigit 函数),但是我们添加了很多信息，现在代码可以像小说一样阅读了。

很好奇大家对这个实验的看法，尤其是黑暗碎片。请不吝赐教。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***