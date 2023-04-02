# 使用这些 JavaScript 快捷键编写更少的代码

> 原文：<https://javascript.plainenglish.io/write-less-code-using-these-javascript-shorthands-f58333907070?source=collection_archive---------12----------------------->

![](img/45008feea3b4af3b13d176444f242a71.png)

Photo by [Pankaj Patel](https://unsplash.com/es/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 1.声明变量

```
let a ;
let b ;
let c = '20';
```

**更好的**

```
let a, b, c ='20';
```

## 2.条件真

```
if(booleanVar ===true) {}
```

**更好的**

```
if (booleanVar) {}
```

## 3.模板文字

```
const name = 'Spencer';
const day = 'Friday'const hello = 'Hi' + name + ', have a great' + day + '!'
```

**更好的**

```
const name = 'Spencer';
const day = 'Friday'const hello = 'Hi $(name), + have a great $(day)!';
```

## 4.箭头功能

```
function hello(name) {
   console.log('hello' + name );}
```

**更好的**

```
const hello = name => console.log('hello' + name);
```

## 5.三元运算符

```
let isQualified;if(marks > 60){
   isQualified = true;}else{
   isQualified = false;}
```

**更好的**

```
let isQualified = marks > 60 ？ true:false;
```

## 6.任意数的幂

```
Math.pow(2,4) //16
```

**更好的**

```
2**4 //16
```

## 感谢您的阅读！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***