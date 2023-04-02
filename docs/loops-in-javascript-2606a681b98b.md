# JavaScript 中的循环介绍

> 原文：<https://javascript.plainenglish.io/loops-in-javascript-2606a681b98b?source=collection_archive---------19----------------------->

## 使用循环做一些重复的任务。

![](img/b7c7a2d905c93ba8f50e015df16bc8f1.png)

无论你属于哪种编程语言，也无论你准备学习哪种编程语言，**循环**都是编程中的根本话题。

它们被用来在`certain condition`下再做一个特定的任务`over and over`一段时间`given number`。

标注以上三个关键词:

*   反复
*   给定数
*   特定条件

这就是编写循环语句所需的全部内容。

# 循环的类型

在任何典型的编程语言中，都存在三种类型的循环:

*   在…期间
*   做..在…期间
*   为

****而*******【do】..而'*** *循环常用于条件为* ***不具体(未知)时。*** *但是* ***对于*** *来说是在条件被* ***固定时使用的。*****

**所以让我们对它们有更多的了解:**

# **“while”循环:**

# **句法**

```
**while(condition){
    // execuatable statement
}**
```

# **做..“while”循环:**

# **句法**

```
**do{
    // execuatable statement    
} while(condition);**
```

# **仔细看看:**

**在 while 循环中:**

*   **先检查一下状况**
*   **然后执行该语句**

**而在 do 中..while 循环:**

*   **执行语句(至少一次)**
*   **然后检查状况**

**让我们通过一个简单的例子来理解其中的区别:**

## **打印从 1 到 10 的数字**

***while 循环***

```
**let num = 1; // declare and assign a variable num with value 1while(num <= 10){ // check while value is less than or equals to 10
   console.log(num); // execute the statement
   num = num+1; // increase the value of num by 1 each time
 }**
```

***做什么..while 循环***

```
**let num = 1; // declare and assign a variable num with value 1
do{
  console.log(num); // execute the statement
  num = num+1; // increase the value of num by 1 each time
}while(num<=10) // check while value is less than or equals to 10**
```

**如果您看到以上 while 和 do 的语法和示例..while 循环中，你可以很容易地提取出它们之间的区别。**

# **for 循环**

**就像我前面提到的,“for”循环与一个固定的条件一起使用。**

# **语法:**

```
**for(initialize; check-for-condition; increment){
    //executable statement
}**
```

****迷茫？别担心。****

**让我们用上面同样的例子来详细说明:**

## **打印从 1 到 10 的数字**

```
**for(let num=1; num<=10; num=num+1){
    console.log(num);
}**
```

*****【for】****让我们在一个单独的程序块中赋值、检查条件和递增。***

**这就是你在接下来的程序中使用 loop 的基本要求。**

**但是等等！**

# **while 和 do 中的非特定(未知)条件怎么办..while 循环**

**很高兴你问了。**

**这些是当您想要检查**条件**时的条件，但是您不知道该条件将被检查多少次。**

**在这种情况下，总是使用**’*，而使用*** 或**’*do..而'*** 循环。**

**以下是一些使用' *while'* 和' *do '的真实场景..【while 循环:***

****1。播放音乐，直到按下暂停按钮****

```
**while(button != pause){
  // play the music
}**
```

****2。重复该问题，直到用户按下是或否****

```
**while(button != yes || button != no){
   // ask question again
}**
```

****2。洗手直到手变脏****

```
**do{
   wash_hands
}while(hands_are_dirty)**
```

**希望这些场景能帮助你理解**‘while’****在哪里做...而现实世界中使用的是'**循环。**

**我们将在以后的文章中更深入地讨论它们。**

**更多参考:**

*   **在 [Quora](https://www.quora.com/) 上查看这个[讨论](https://www.quora.com/What-is-a-real-life-example-of-do-while-loop)**
*   **还有这个[论坛](https://www.codecademy.com/forum_questions/5130254c3ecc9d8c45003f70)上的[code academy](https://www.codecademy.com/)**
*   **还有这个[条](https://betterprogramming.pub/how-to-pick-between-a-while-and-for-loop-14ef217c3776)上的[介质](https://medium.com/)**

**谢谢你留下来。不断学习。**

***本文正式发表于*[*www.withinbracket.com*](http://www.withinbracket.com)**

**[](https://withinbracket.com/posts/loops-in-javascript/) [## JavaScript 中的循环

### 做一些重复性的工作。不管你属于哪种编程语言，也不管你是哪种编程语言…

withinbracket.com](https://withinbracket.com/posts/loops-in-javascript/) 

*📌更多文章* [*在这里*](https://withinbracket.com/archives) *找。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获取独家写作机会和建议。***