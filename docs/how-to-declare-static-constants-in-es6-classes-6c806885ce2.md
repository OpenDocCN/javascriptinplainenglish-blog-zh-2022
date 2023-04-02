# 如何在 ES6 类中声明静态常量？

> 原文：<https://javascript.plainenglish.io/how-to-declare-static-constants-in-es6-classes-6c806885ce2?source=collection_archive---------4----------------------->

![](img/92bb4f544a8f4559f35946981ed7cac6.png)

Photo by [Daan Stevens](https://unsplash.com/@daanstevens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 JavaScript 类中声明静态常量。

在本文中，我们将研究如何在 ES6 类中声明静态常量。

# 在我们的类中添加 Getters

为了在我们的 ES6 类中声明静态常量，我们可以在类外声明常量，并添加 getters 来返回我们的类中的常量。

例如，我们可以写:

```
const constant1 = 3,
  constant2 = 2;
class Example {
  static get constant1() {
    return constant1;
  } static get constant2() {
    return constant2;
  }
}console.log(Example.constant1)
console.log(Example.constant2)
```

我们声明`constant1`和`constant2`。

然后在`Example`类中，我们创建了`constant1`和`constant2`getter。

我们在`get`之前添加了`static`关键字，这样我们就可以创建静态。

然后在 getter 函数中，我们分别返回`constant1`和`constant2`值。

同样，我们可以写:

```
class Example {
  static get constant1() {
    return 3
  } static get constant2() {
    return 2
  }
}Object.freeze(Example);
console.log(Example.constant1)
console.log(Example.constant2)
```

这相当于我们上面写的。

所以当我们记录`Example.constant1`和`Example.constant2`的值时，我们分别看到 3 和 2。

# 对象.冻结

我们可以冻结类，使整个类不可变。

为此，我们写道:

```
class Example {}
Example.constant1 = 3
Example.constant2 = 2
Object.freeze(Example);
console.log(Example.constant1)
console.log(Example.constant2)
```

我们用以下内容添加静态属性:

```
Example.constant1 = 3
Example.constant2 = 2
```

这是可行的，因为类是构造函数，而构造函数是对象。

这也意味着我们可以在`Example`上使用`Object.freeze`方法来使`Example`类不可变。

因此我们可以记录`Example.constant1`和`Example.constant2`属性的值并获取它们的值。

我们应该分别看到 3 和 2。

# 结论

我们可以在 JavaScript 类中声明静态常量，方法是声明静态 getters，它返回在类外声明的常量。

同样，我们可以用`Object.freeze`方法冻结这个类，因为它是一个常规对象。

这使得该类不可变。

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*