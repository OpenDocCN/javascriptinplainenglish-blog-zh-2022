# 将两个你可能不知道的字符串数字相加的最短和最好的方法

> 原文：<https://javascript.plainenglish.io/the-shortest-and-best-way-to-add-two-string-numbers-that-you-probably-dont-know-f1f965c31717?source=collection_archive---------20----------------------->

## JavaScript 中添加字符串数字的两种方法。

![](img/9193fa5f0656e03707c7eb36b0744b19.png)

Photo by [Roman Skrypnyk](https://unsplash.com/@timesnewroman14?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/calculator?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 大家好👋

怎么了，朋友们，这是雪球。我是一个年轻热情的自学成才的开发人员，并打算成为一名成功的开发人员。

今天，我在这里带来了一件惊人的事情，你可能不知道，但现在你会知道了。快乐阅读！

```
const x = "5"
const y = "4"const z = x + y
```

这是行不通的，因为添加字符串会连接字符串，因此代码的输出将是`"54"`而不是`9`。

在本文中，我将讨论两种添加字符串数字的方法。

# 使用`parseInt()`

```
const x = "5"
const y = "4"const z = parseInt(x) + parseInt(y)
```

这里，字符串被解析为一个数字，因此这段代码的输出必须是`9`，因为`x`和`y`变量都被转换为一个数字。

如果你将`parseInt()`与单词和字母一起使用，它将返回- `NaN`，它代表的不是一个数字。

这种方法很容易使用，但是现在我们采用一种更简单的方法。

# 使用一元加号运算符

如上所述，我们不能仅仅用`+`操作符将两个字符串相加。但是有一种方法可以用`+`操作符将两个字符串数字相加。

让我展示给你看:

```
const x = "5"
const y = "4"const z = +x + +y
```

在一个元素前单独使用`+`操作符表示一个数学运算，并试图将该元素转换为一个数字，如果失败，它将返回`NaN`。

这就是本文的全部内容。我经常分享文章，所以一定要点击关注按钮。

感谢您的阅读，祝您愉快！你的欣赏是我的动力😊

*   在 Twitter 上关注我— [@codewithsnowbit](https://twitter.com/codewithsnowbit)
*   在 YouTube 上订阅我— [用雪球编码](https://www.youtube.com/channel/UCNTKqF1vhFYX_v0ERnUa1RQ?view_as=subscriber&sub_confirmation=1)

*更多内容请看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*