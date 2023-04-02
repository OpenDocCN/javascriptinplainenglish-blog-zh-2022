# TXT 记录的正则表达式是什么？

> 原文：<https://javascript.plainenglish.io/whats-the-regular-expression-of-txt-record-897d54841a43?source=collection_archive---------20----------------------->

![](img/1806c85a6f824dd1f665639296dce7b5.png)

TXT 记录可以在下面输入关键字。

```
a-z  
A-Z  
0-9  
Space  
- (hyphen)  
! " # $ % & ' ( ) * + , - / : ; < = > ? @ [ \ ] ^ _ ` { | } ~ .
```

允许你只输入这个的正则表达式是什么？

底部是我做的。

**————————回答——————**

```
const txt_rex = /[#\&\\+\-%@=\/\\\:;,\.\'\"\^`~\_|\!\/\?\*$#<>()\[\]\{\}]/i;const txt_rex = /^[\w !"#$%&'()*+,\/:;<=>?@[\]^`{|}~.-]+$/;
```

`\w` = 'A-Za-z0-9_'
`[...]+` =一个字符集，1 个或多个
`^...$` =从开始...直到结束

HTML 示例:

```
input:invalid{box-shadow: 0 0 0 4px red;}<input pattern="[\w !\x22#$%&'()*+,/:;<=>?@[\]^`{|}~.-]+">
```

## **有更好的主意吗？发个纸条，我来更新。**

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***