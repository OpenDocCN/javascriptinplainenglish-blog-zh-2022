# 如何到达无限滚动🖱️页面的末尾

> 原文：<https://javascript.plainenglish.io/how-to-get-to-the-end-of-a-page-with-infinite-scrolling-%EF%B8%8F-4c10c3ab4b89?source=collection_archive---------11----------------------->

## 无限滚动到一个网页的末尾是不是时间太长了？你可以用一个小脚本作弊！🤖

![](img/91eb4e973800e6f22781c5c5f6d98771.png)

Photo by [**Vojtech Okenka**](https://www.pexels.com/@vojtech-okenka-127162?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [**Pexels**](https://www.pexels.com/photo/person-holding-apple-magic-mouse-392018/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

你可能已经浏览过一个带有**无限滚动**的网页。但是，你曾经需要**加载所有的结果**吗？🤔

最近，我不得不使用这个功能来抓取网页的数据，我必须做出选择:要么**向下滚动并等待**新的结果来加载几次**，要么我可以通过编程来尝试找到一种方法来做这件事**。****

**我让你猜猜我做了什么选择！😝**

**幸运的是，如果你懂这种语言，去无限滚动页面底部的 JavaScript 代码非常简单。或者如果你在这篇文章上！😉**

**只需打开 *DevTools* (带`F12`)并将**下面的脚本**粘贴到控制台中。**

```
// Declare some constants
const MAXIMUM_NUMBER_OF_TRIALS = 5;
const MINIMUM_SLEEPING_TIME_IN_MS = 500;
const MAXIMUM_SLEEPING_TIME_IN_MS = 2000;// Utility functions
const sleep = (time) => new Promise((resolve) => setTimeout(resolve, time));
const randomNumber = (minimum, maximum) => Math.floor(Math.random() * maximum) + minimum;
const randomSleep = () => sleep(randomNumber(MINIMUM_SLEEPING_TIME_IN_MS, MAXIMUM_SLEEPING_TIME_IN_MS));// How to get at the bottom of an infinity scroll
let currentScrollHeight = 0;
let manualStop = false;
let numberOfScrolls = 0;
let numberOfTrials = 0;while (numberOfTrials < MAXIMUM_NUMBER_OF_TRIALS && !manualStop) {
  // Keep the current scroll height
  currentScrollHeight = document.body.scrollHeight; // Scroll at the bottom of the page
  window.scrollTo(0, currentScrollHeight); // Wait some seconds to load more results
  await randomSleep(); // If the height hasn't changed, there may be no more results to load
  if (currentScrollHeight === document.body.scrollHeight) {
    // Try another time
    numberOfTrials++; console.log(
      `Is it already the end of the infinite scroll? ${MAXIMUM_NUMBER_OF_TRIALS - numberOfTrials} trials left.`,
    );
  } else {
    // Restart the number of consecutive trials
    numberOfTrials = 0; // Increment the number of successful scroll
    numberOfScrolls++; console.log(`The scroll #${numberOfScrolls} was successful!`);
  }
}console.log('We should be at the bottom of the infinity scroll! Congratulation!');
console.log(`${numberOfScrolls} scrolls were needed to load all results!`);
```

**我加了很多评论，你应该很容易搞清楚。如果服务器响应时间过长，您可能需要调整脚本顶部的**常量**。**

> *****提示*** *:如果你加载了足够多的结果，你可以通过在控制台中键入* `*manualStop = true*`随时 ***停止脚本*** *。***

**希望这能帮助你滚动到时间的尽头！😇**

**如果你喜欢阅读这样的故事，并想支持我成为一名作家，可以考虑[报名成为**媒体成员**](https://benjaminrancourt.medium.com/membership) 。每月 5 美元，你可以无限制地阅读媒体上的故事。如果你用我的链接注册，我会赚一点佣金。**

**[](https://benjaminrancourt.medium.com/membership) [## 通过我的推荐链接加入 Medium-Benjamin Rancourt

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

benjaminrancourt.medium.com](https://benjaminrancourt.medium.com/membership)** 

***原载于 2021 年 12 月 2 日*[*www . Benjamin rancourt . ca*](https://www.benjaminrancourt.ca/how-to-get-to-the-end-of-a-page-with-infinite-scrolling)*。***

***更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。****