# 在 JavaScript 中的数组开头添加元素

> 原文：<https://javascript.plainenglish.io/add-element-on-beginning-of-the-array-in-javascript-c45ef85369ee?source=collection_archive---------19----------------------->

## 在数组开头添加元素的两种方法

![](img/81e4279987aa08565f1e843fbf8af9d3.png)

Photo by [Alesia Kazantceva](https://unsplash.com/@alesiaskaz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，您需要在数组的开头添加一个新元素。
让我们考虑下面的实际例子:
您有一个下拉选项数组，您想添加
空选项来重置下拉字段值。

## 1.使用拼接方法

`splice()`方法通过移除或替换现有元素和/或在位置添加新元素[来改变数组的内容。要访问数组的一部分而不修改它，请参见](https://en.wikipedia.org/wiki/In-place_algorithm)`[slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)`。

```
const animals = [
    {
      value: 'cat',
      display: 'Cat'
    }, 
    {
      value: 'dog',
      display: 'Dog'
    }, 
    {
      value: 'cow',
      display: 'Cow'
    }
];

const emptyOption = {
    value: null,
    display: ''
};

animals.splice(0, 0, emptyOption);

// result
animals:  [
  { value: null, display: '' },
  { value: 'cat', display: 'Cat' },
  { value: 'dog', display: 'Dog' },
  { value: 'cow', display: 'Cow' }
]
```

## 2.使用非移位方法

`unshift()`方法将一个或多个元素添加到数组的开头，并返回数组的新长度。

```
const animals = [
    {
      value: 'cat',
      display: 'Cat'
    }, 
    {
      value: 'dog',
      display: 'Dog'
    }, 
    {
      value: 'cow',
      display: 'Cow'
    }
];

const emptyOption = {
    value: null,
    display: ''
}

animals.unshift(emptyOption);

// result
animals:  [
  { value: null, display: '' },
  { value: 'cat', display: 'Cat' },
  { value: 'dog', display: 'Dog' },
  { value: 'cow', display: 'Cow' }
]
```

**结论** `splice()`方法非常有用，例如，当你想覆盖数组中第一个元素的值，或者以其他方式改变数组内容时。
采用`unshift()`方法的第二种方案非常优雅，推荐本次操作使用。
类似于 push 方法，但它在数组的开头添加了一个元素。

感谢阅读。

*如果你喜欢这样的故事，并且想继续阅读我的故事，请考虑成为* [*中会员*](https://medium.com/membership) *和我的关注者。每月 5 美元，你可以无限制地访问媒体内容。*

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***