# 人们实际上写的 45 个有趣的代码注释

> 原文：<https://javascript.plainenglish.io/45-funny-code-comments-that-people-actually-wrote-8408749640e3?source=collection_archive---------6----------------------->

## 这些实际上是在某个地方的代码库中

![](img/ff2696eca74b388cbff40174f8193c0e.png)

Photo by [Tyler Nix](https://unsplash.com/@nixcreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编码中的注释是对计算机程序中正在执行的任务的人类可读的解释。包含它们是为了使代码更容易理解。

在本文中，您将看到代码中实际编写的有趣注释列表。

1.

```
/*
 * You may think you know what the following code does.
 * But you dont. Trust me.
 * Fiddle with it, and youll spend many a sleepless
 * night cursing the moment you thought youd be clever
 * enough to "optimize" the code below.
 * Now close this file and go play with something else.
 */
```

2.

```
// I am not sure if we need this, but too scared to delete.
```

3.

```
# To understand recursion, see the bottom of this fileAt the bottom of the file:# To understand recursion, see the top of this file
```

4.

```
// I don't know why I need this, but it stops the people being upside-down

x = -x;
```

5.

```
/* I did this the other way */
```

6.

```
//Dear future me. Please forgive me. 
//I can't even begin to express how sorry I am.
```

7.

```
//private instance variable for storing age
public static int age;
```

8.

```
/* You are not meant to understand this */
```

9.

```
/* Halley's comment */
```

10.

```
/* IF DOLPHINS ARE SO SMART, HOW COME THEY LIVE IN IGLOOS? */
```

11.

```
// hack for ie browser (assuming that ie is a browser)
```

12.

```
/* Emits a 7-Hz tone for 10 seconds.
  True story: 7 Hz is the resonant frequency of a
  chicken's skull cavity. This was determined
  empirically in Australia, where a new factory
  generating 7-Hz tones was located too close to a
  chicken ranch: When the factory started up, all the
  chickens died.
  Your PC may not be able to emit a 7-Hz tone. */

main()
{
    sound(7);
    delay(10000);
    nosound();
}
```

13.

```
/* These magic numbers are fucking stupid. */
```

14.

```
/* Dear free software world, do you NOW see we are fucking
   things up?! This is insane! */
```

15.

```
/* We will NOT put a fucking timestamp in the header here. Every
   time you put it back, I will come in and take it out again. */
```

16.

```
# However, this only works if there are MULTIPLE checkboxes!
# The fucking JS DOM *changes* based on one or multiple boxes!?!?!
# Damn damn damn I hate the JavaScript DOM so damn much!!!!!! 
```

17.

```
/* TODO: this is obviously not right ... this whole fucking module
   sucks anyway */
```

18.

```
// I have to find a better job
```

19.

```
/* FIXME: please god, when will the hurting stop? Thus function is so fucking broken it's not even funny. */
```

20.

```
/*
This isn't the right way to deal with this, but today is my last day, Ron
just spilled coffee on my desk, and I'm hungry, so this will have to do...
*/ 
```

21.

```
return 12; // 12 is my lucky number
```

22.

```
// I know the line below is wrong, but it came that way from our IP vendor, and  // the driver won't work if you "fix" it. I've had to revert this change 4 times // now. Leave it alone, or I will hunt you down and hurt you 
if (r = 0) {     
 /* bunch of code here */ 
} else {    
 /* even more code here */
} 
```

23.

```
// this comment included for the benefit of anyone grepping for swearwords: shit.
```

24.

```
} catch (PartInitException pie) {
    // Mmm... pie
```

25.

```
// This comment is self explanatory.
```

26.

```
class Act //That's me!!!
{

}
```

27.

```
doRun.run();  // ... "a doo run run".
```

28.

```
// This only exists because Scott doesn't know how to use const correctly
```

29.

```
public boolean isDirty() {
    //Why do you always go out and
    return dirty;
}
```

30.

```
* ...and don't just declare it volatile and think you've solved
 * the problem. You young punks think you know what volatile
 * means... why in my day we had to cast it volatile uphill
 * both ways, and the code still didn't work! Whippersnappers...
```

31.

```
// John! If you'll svn remove this once more,
// I'll shut you, for God's sake!
// That piece of code is not “something strange”!
// That is THE AUTH VALIDATION.
```

32.

```
// TODO: Fix this.  Fix what?
```

33.

```
if i ever see this again i'm going to start bringing guns to work
```

34.

```
//MailBody builders for two outgoing messages
StringBuilder hanz = new StringBuilder();
StringBuilder franz = new StringBuilder();
```

35.

```
uncomment the following line if the program manager changes her mind again this week
```

36.

```
/* Ah ah ah! You'll never understand why this one works. */
```

37.

```
//I wonder if she actually reads these.
```

38.

```
/*
after hours of consulting the tome of google
i have discovered that by the will of unknown forces
without the below line, IE7 believes that 6px = 12px
*/
font-size: 0px;
```

39.

```
#Christmas tree initializer  
    toConnect = []  
    toRead =   [  ]  
    toWrite = [    ]   
    primes = [      ]  
    responses = {}  
    remaining = {}
```

40.

```
//this formula is right, work out the math yourself if you don't believe me
```

41.

```
long time; /* know C */
```

42.

```
{ 
  { 
    while (.. ){ 
      if (..){
          }
      for (.. ){ 
          }
         .... (just putting in the control flow here, imagine another few hundred ifs)
      if(..)   {
            if(..)     {
                   if(..)   {
                ...
                (another few hundred brackets)
                       }
                  }
         } //endif
```

43.

```
// I can't divide with zero, so I have to divide with something very similar
result = number / 0.00000000000001;
```

44.

```
//Mr. Compiler, please do not read this.
```

45.

```
'NO COMMENT
```

## 参考

*   你在 stackoverflow.com 遇到的最好的代码评论

感谢阅读！

如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑[成为一名媒体会员](https://nehalk.medium.com/membership)。一个月 5 美元，你可以无限制地阅读 Medium 上的所有故事。如果你[用我的链接](https://nehalk.medium.com/membership)注册，我会赚一小笔佣金。

[](https://nehalk.medium.com/membership) [## 通过我的推荐链接加入 Medium-Nehal Khan

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

nehalk.medium.com](https://nehalk.medium.com/membership) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*