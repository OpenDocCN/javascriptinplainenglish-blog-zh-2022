# JavaScript 中的 Switch 语句

> 原文：<https://javascript.plainenglish.io/the-switch-statement-in-javascript-33827e4ae504?source=collection_archive---------14----------------------->

比使用 if-else 更快地做出决策。

![](img/8bc7e6294e08f406d6843c1c327ead3e.png)

Photo by [Tim Mossholder](https://www.pexels.com/@timmossholder?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/eight-electrical-metric-meters-942316/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

当谈到**通过决策来控制**特定程序的*流程*时，我们通常有两种选择:

*   如果…否则
*   开关盒

在我们之前的文章中，我们已经涵盖了你需要知道的关于 *if 的一切..JavaScript 中的 else* 。以下是链接:

[](https://withinbracket.com/posts/if-else-in-javascript-conditional-statement/) [## 在 JavaScript 条件语句中

### 这就是编程的意义所在。比尔·盖茨曾经说过，“计算机编程是数学计算和制作…

withinbracket.com](https://withinbracket.com/posts/if-else-in-javascript-conditional-statement/) 

现在，让我们来研究 switch case 语句。

# 看看这个简单的例子:

```
**let** fruit = "apple";
**switch** (fruit){
  **case** "apple":
    **console.log**("This is an apple");
    **break;**
  **case** "mango":
    **console.log**("This is a mango");
    **break;**
  **default:**
    **console.log**("This is a fruit");
}*// Output:
This is an apple*
```

如果你不熟悉`switch`，那么控制程序流程是一个相当简单的过程。

## 以下是 switch 的典型语法:

```
**switch**(expression_to_be_checked){
  **case** first_value:
    //do something
    **break**;
  **case** second_value:
    //do something else
    **break**;
  **case** third_value:
   //do something else
   **break**;
 **default**:
   // do what not defined in above cases
}
```

## 让我们分解一下语法:

*   每个`switch`语句都以一个 switch 关键字开始，该关键字包含一个要作为`value` 或`variable`进行检查的表达式
*   然后我们有几个`cases` 来检查表情，并根据`case`做特定的任务
*   在每个`case` 块中，我们都有一个`break` 关键字。它用于**中断**程序的进一步流程，并限制我们执行特定`case` 程序块的任务
*   最后，我们有一个`default` 案例。如果 ***否*** 情况条件满足*，则执行**默认**任务。*

这就是 JavaScript 中的 switch case 语句。

***但是，*** *这里并不会结束，有几个重要的点你在使用之前需要注意。*

## **你可以把*默认*关键字放在任何你想放的地方；没必要放在*末端***

到处你都会发现`default` 关键字被放在每个必需的`case` 块的末尾，但是没有必要把`default` 放在末尾。

事实上，我更喜欢把`default` 放在**开始**的地方，因为如果我使用很多格块，不用担心再有*和*了，这让我感觉很舒服。

无论哪种方式都是一个*主观*的问题，所以你把它放在你想放的地方，没什么大不了的。

```
**let** animal = "mouse";
**switch** (animal){
  **default:**
    **console.log**("This is an animal");
  **case** "rabbit":
    **console.log**("This is an rabbit");
    **break;**
  **case** "lion":
    **console.log**("This is a lion");
}*// Output:
This is an animal*
```

> 事实上，我不需要将`break` 放在最后一个`case` 块，因为*有意义*，它是最后一个`case` ，在最后一个 case 块之后不会检查其他的`case`

## 并非每个 switch 语句都需要默认情况。

是的，你没看错。并不是**强制**在每个`switch` 语句中使用`default` 。您可能有 ***条件*** 而不需要使用默认情况。

```
**let** animal = "mouse";
**switch** (animal){
  **case** "rabbit":
    **console.log**("This is an rabbit");
    **break;**
  **case** "lion":
    **console.log**("This is a lion");
}*// Output:
you might not able to see anything as output*
```

## 如果忘记使用 break 关键字怎么办？

很简单的回答— **无论条件满足与否，所有的 case 块都会被执行** —很简单。

我来注释掉**破**关键词。

```
**let** fruit = "guava";
**switch** (fruit){
  **case** "apple":
    **console.log**("This is an apple");
    *//break****;***
  **case** "mango":
    **console.log**("This is a mango");
    //*break;*
  **default:**
    **console.log**("This is a fruit");
}*// Output:
This is an apple
This is a* mango
```

> **不使用** `**break**` **关键词同样可以带来新的体验。这叫多案操作。**

看看这个:

```
**let** fruit = "guava";
**switch** (fruit){
  **case** "apple":
  **case** "mango":
  **case** "pineapple":
  **case** "guava":
  **case** "watermelon":
    console.log("This is a fruit");
    **break**;
  **default**:
    console.log("This is a thing");
}//Output
This is a fruit.
```

> 这也被称为失败。

这里我们用四个 case 语句执行同样的任务。

# 结论:

所以这就是你使用`switch case.`所需要知道的。有时，switch 语句被用作`if…else.`的替代，但是它们有自己的用例。

还可以看出，如果有太多的**条件**需要检查，那么`switch` 语句在大多数情况下比`if…else`运行得更快。

我已经举例说明了几个例子和场景来解释 switch 语句，但是我强烈建议用您自己的例子来进行调整，以便更好地理解。

因为俗话说，熟能生巧。

谢谢你留下来。我会在新的里见到你。

> 这个故事正式发表在 [**括号内**](https://withinbracket.com/)
> 
> [https://within bracket . com/posts/switch-statement-in-JavaScript/](https://withinbracket.com/posts/switch-statement-in-javascript/)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*