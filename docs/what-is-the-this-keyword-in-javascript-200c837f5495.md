# JavaScript 中的‘this’关键字是什么？

> 原文：<https://javascript.plainenglish.io/what-is-the-this-keyword-in-javascript-200c837f5495?source=collection_archive---------7----------------------->

## 了解 JavaScript 中的“this”关键字是什么，以及可以用它做什么。

所以，你已经看到了 ***这个*** 关键词抛来抛去。挺有意思，挺神秘的。你不太确定该怎么做。不要害怕！用不了多久，你也可以像高手一样利用**T5 这款 T7 了！**

![](img/626073da3ef3eba0836879a1a7e715df.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 那么，什么是' ***这个'*** ？

简单来说， ***这个*** 是指一个对象。特别是调用函数的对象。JavaScript 的 ***this*** 的行为与其他语言如 C++和 Java 稍有不同。在 JavaScript 中，你实际上可以使用 ***这个*** 之外的一个函数或方法。我们来看几个例子。

# “这”的例子

```
var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function() {
      console.log(this.firstName + " " + this.lastName);
   }
};Person.fullName(); // "James Bond"
```

首先，我们有一个物体 ***人*** 。人有几个属性: ***名*******姓*****全名* 。 ***名*** 和 ***姓*** 的值相当直接。分别是*詹姆斯*和*邦德*的静态值。 ***全称*** 略有不同。 ***fullName 的*** 值是一个函数。里面的功能就是我们的朋友 ***这个*** 。因为 ***这个*** 是用在 ***人*** 物内， ***这个*** 是指 ***人*** *。*如果我们试图用 ***这个*** 来调用一个不同的变量呢？行得通吗？让我们看看。**

```
**var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function() {
      console.log(this.firstName + " " + this.lastName);
   }
   nickName: function() {
      console.log(this.middleName);
   }
};Person.fullName(); // "James Bond"
Person.nickName(); // undefined**
```

*****昵称*** 返回未定义。但是为什么呢？嗯， ***middleName*** 不是人的财产。如果***middle name***是在***Person****之外定义和初始化的怎么办？*我们还能这样用吗？**

```
**var middleName = "middle name";var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function() {
      console.log(this.firstName + " " + this.lastName);
   }
   nickName: function() {
      console.log(this.middleName);
   }
};Person.fullName(); // "James Bond"
Person.nickName(); // undefined**
```

**没有。我们仍然不确定。又一次…但是为什么？嗯，当 ***这个*** 用在一个对象内的时候，它的作用域就是指那个特定的对象。**

# **还有什么地方可以用'*这个'*？**

**如果 ***这个*** 在一个对象之外被引用，那么它将引用全局对象。这是默认绑定。**

```
**function returnThis() {
   return this;
}console.log(returnThis()); // [object Window]
console.log(this); // [object Window]**
```

*****这个*** 对 HTML 内部的事件处理程序很有用。**

```
**<p onclick="this.style.fontWeight='bold'">
       Hello World!
</p>**
```

**在上面的例子中， ***这个*** 用来访问全局对象和操纵< p >标签的样式。当*你好世界！点击*，字体粗细将变为粗体。**

# **绑定“this”**

**我们也可以用 ***apply()*** 和***call()****方法来绑定这个。请看下面:***

```
***var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function() {
      console.log(this.firstName + " " + this.lastName);
   }
};var Person2 = {
    firstName: "John",
    lastName: "Doe",
}Person.fullName(); // "James Bond"
Person.fullName.apply(Person2); // "John Doe"
Person.fullName.call(Person2); // "John Doe"***
```

***乍一看，***apply()****和 ***call()*** 看起来像是做同一件事，对吗？不完全是。***apply()****接受参数作为数组，而 ***call()*** 接受参数作为普通参数。让我们看看那是什么样子。*****

```
**var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function(adjective1, adjective2) {
      console.log(this.firstName + " is " +
                  adjective1 + " and " + adjective2);
   }
};var Person2 = {
    firstName: "John",
    lastName: "Doe",
}Person.fullName(); // "James Bond"Person.fullName.apply(Person2, ["cool", "fun"]); // "John Doe is cool and fun"Person.fullName.call(Person2, "wise", "funny"); // "John Doe is wise and funny"**
```

**最后， ***bind()*** 方法可以以非常相似的方式使用。**

```
**var Person = {
   firstName: "James",
   lastName: "Bond",
   fullName: function(adjective1, adjective2) {
      console.log(this.firstName + " is " +
                  adjective1 + " and " + adjective2);
   }
};var Person2 = {
    firstName: "John",
    lastName: "Doe",
}const getFullName = Person.fullName.bind(Person2);getFullName(); // "John Doe"**
```

*****bind()****方法允许 ***Person2*** 从 ***Person*** 对象中借用属性 ***fullName*** 。***

# **结论**

**恭喜你。你现在可以将这个添加到你的 JS 知识工具箱中。*‘这个’*关键词很厉害。玩转它的每一个属性，你很快就会成为一名职业玩家。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****