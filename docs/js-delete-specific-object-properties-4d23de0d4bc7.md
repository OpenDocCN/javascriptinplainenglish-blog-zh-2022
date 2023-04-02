# 删除 JavaScript 中的特定对象属性

> 原文：<https://javascript.plainenglish.io/js-delete-specific-object-properties-4d23de0d4bc7?source=collection_archive---------7----------------------->

## 删除对象属性的优雅方式

![](img/89d01d238f2a133d16dec0eb37d626d8.png)

Photo by [Jess Bailey](https://unsplash.com/@jessbaileydesigns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大的物体必须变轻，这是你有时需要的。因此，我们的想法是创建一个 util 方法，它可以使用以下方法删除整个应用程序中的对象属性:

*   创建实用程序类
*   创建接受对象和属性过滤器谓词函数的静态方法
*   对每个过滤的对象特性执行删除

```
 const person = {
 name: 'John',
 surname: 'Doe',
 age: 40
}

class Objects {

 static deleteProperties(object, predicate) {
  Object.keys(object)
    .filter(predicate)
    .forEach(property => delete object[property]);
 }

}

Objects.deleteProperties(person, (property) => property === 'age');
```

请注意，我们有以下方法和操作符:

*   [Object.keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
*   [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
*   [array . propto type . foreach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
*   [删除操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)

如果我们检查 person 对象的新状态，我们将
看到 age 属性被成功删除。

```
{
   "name": "John",
   "surname": "Doe"
}
```

感谢阅读。

*如果你喜欢这样的故事，想继续看我的故事，请考虑成为* [*中等会员*](https://medium.com/membership) *。每月 5 美元，你可以无限制地访问媒体内容。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**