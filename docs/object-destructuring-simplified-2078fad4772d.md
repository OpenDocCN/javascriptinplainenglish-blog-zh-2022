# 简化的对象析构

> 原文：<https://javascript.plainenglish.io/object-destructuring-simplified-2078fad4772d?source=collection_archive---------12----------------------->

## 关于 JavaScript 中的对象析构，你需要知道的一切。

![](img/15b90bc753a8d453bb19bb641078f03b.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

析构是一个概念，其中我们分解一种数据类型，并将其单独的属性赋给一个变量。

我们已经在上一篇文章中讨论了数组析构。如果你有同样的兴趣，可以看看这里:

[](/array-destructuring-simplified-10300505499) [## 简化的数组析构

### 如何使用析构的初学者指南？

javascript.plainenglish.io](/array-destructuring-simplified-10300505499) 

现在，让我们看看析构在对象中是如何工作的。

1.  **基本用法**

```
let fullName = {firstName: 'ABC',lastName: 'XYZ',};let { firstName, lastName } = fullName; // Destructuring Blockconsole.log(firstName);    ABCconsole.log(lastName);     XYZ
```

正如您在上面的代码片段中看到的，在析构块中，我们分解了 fullName 对象，并将其赋给表达式左侧定义的变量。
请注意，在上面的场景中，对象的属性名应该与左边表达式中定义的变量相匹配。
如果我们定义了任何其他变量名，那么它的值被标记为已定义。
例如，

```
let { middleName, lastName } = fullName;console.log(middleName);   //undefined
```

因为 middleName 的 fullName 中没有属性，所以它被初始化为 undefined。

2.**自定义变量名**

假设，我们希望析构后变量的名称应该是某个自定义名称而不是与对象属性相匹配的名称。同样可以通过以下方式实现:

```
let fullName = {firstName: 'ABC',lastName: 'XYZ',};let { firstName: a, lastName } = fullName; // Destructuredconsole.log(a);  // ABCconsole.log(lastName); // XYZ
```

注意这里的析构步骤，其中我们将从对象接收的属性 firstName 映射到另一个名为“a”的属性。

**3。分配默认值**

可能存在这样的情况，其中特定属性不存在于对象中。所以，在这种情况下，如果我们想设置一个默认值而不是 undefined，那也是可以实现的。

```
let fullName = {firstName: 'ABC',lastName: 'XYZ',};let { firstName, middleName = 'MNU', lastName } = fullName;console.log(middleName); // MNU
```

因此，在上面的代码片段中，我们将 middleName 的预定义值设为“MNU”。如果 middleName 出现在 object fullName 中，那么它的值将被赋值，否则它的值将被设置为默认值。

**4。拼接新对象**

假设我们想从一个对象中排除一个属性，并从其余属性中创建一个新对象。同样可以通过以下方式实现:

```
let fullName = {firstName: 'ABC',middleName: 'PQR',lastName: 'XYZ',};let { middleName, ...shortName } = fullName;console.log(shortName);    // { firstName: 'ABC', lastName: 'XYZ' }
```

在上面的代码片段中，我们将 middleName 属性分配给一个变量，并使用 rest 运算符(…)将变量的其余部分分配给一个单独的对象。

简单来说，这就是析构在对象中的工作方式。希望你也能理解。

如果你有任何关于数组析构的疑问，请回复我。

关于我——我是一个编程爱好者，喜欢阅读和写作前端设计、JavaScript 和 UI/UX 相关的东西。点击[此处](https://medium.com/@avinash.dev21987)阅读我所有的文章，并告诉我您的反馈。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*