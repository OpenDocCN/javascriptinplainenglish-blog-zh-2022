# 深度赋值

> 原文：<https://javascript.plainenglish.io/js-object-assign-in-depth-113fad346731?source=collection_archive---------10----------------------->

## 关于分配方法的重要细节的完整概述

![](img/6f673916c280a87384a3ae2e26ec01ef.png)

Photo by [Emile Perron](https://unsplash.com/@emilep?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

[Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 方法(顾名思义)的目的是将一组属性从目的地分配给源对象。
理解这里的整体情况非常重要，所以我想让
回顾一下非常重要的几点。

## 1.源必须不同于 null 或未定义

```
let person = null; // or undefined

Object.assign(person, { name: 'John', surname: 'Doe' });
console.log(person);

// Object.assign(person, { name: 'John', surname: 'Doe' });
// TypeError: Cannot convert undefined or null to object
```

## 2.源必须是对象

如果源值不是 object，该方法将不会引发任何错误

```
Object.assign("", { name: 'John', surname: 'Doe' });
// no errors in this case
```

## 3.属性值的覆盖

```
let person = {
    name: 'John'
};

Object.assign(person, { 
    name: 'Leonardo', 
    surname: 'Doe' 
});

// { name: 'Leonardo', surname: 'Doe' }
```

## 4.多个目标对象

```
let person = {};

Object.assign(person, { name: 'Leonardo', surname: 'Doe' }, { age: 44 });
console.log(person);

// { name: 'Leonardo', surname: 'Doe', age: 44 }
```

## 5.将属性设置为空/未定义

```
let person = {
    name: 'John',
    surname: 'Doe',
    age: 44
};

Object.assign(person, { 
    name: 'Leonardo', 
    surname: 'Doe',
    age: null
});
console.log(person);

// { name: 'Leonardo', surname: 'Doe', age: null }
```

## 6.浅拷贝

然而，关于`Object.assign()`需要记住的一点是，该方法只对对象*执行部分深度复制。*

```
 let person = {
    name: 'John',
    surname: 'Doe',
    age: 44,
    address: {
        city: 'LA'
    }
};

let personCopy = Object.assign({}, person);

personCopy.name = 'Leonardo';
personCopy.address.city = 'New York';
console.log('person: ', person);
console.log('personCopy: ', personCopy);

/*
person  {
  name: 'John',
  surname: 'Doe',
  age: 44,
  address: { city: 'New York' }
}
personCopy:  {
  name: 'Leonardo',
  surname: 'Doe',
  age: 44,
  address: { city: 'New York' }
}
*/
```

感谢阅读。

*如果你喜欢这样的故事，想继续看我的故事，请考虑成为* [*中会员*](https://medium.com/membership) *和我的关注者。每月 5 美元，你可以无限制地访问媒体内容。*

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*

## 希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。