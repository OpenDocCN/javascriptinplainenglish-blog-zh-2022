# 什么是 JavaScript Getters 和 Setters？

> 原文：<https://javascript.plainenglish.io/javascript-getters-and-setters-d5ac2cbb7287?source=collection_archive---------8----------------------->

## 详细探究“get”和“set”关键字。

![](img/704f9d49f7a224e2f7292dbe58c762cd.png)

getters 和 setters 有助于以封装的方式访问和操作对象属性。下面我们来详细探讨一下这些方法。

# 吸气剂

关键字`get`用于创建一个 getter 函数，该函数将返回一个计算值。与普通函数不同，我们不需要调用 getter 函数；相反，我们可以用它的名字直接访问它。

```
const person = {
  first_name: 'Peter',
  last_name: 'Parker',
  get full_name() {
      return `${this.first_name} ${this.last_name}`
  }
}console.log(person.full_name); // Peter Parker
```

`get`关键字将 getter 函数与同名的对象属性绑定在一起。当我们访问这个对象属性时，getter 函数的结果被返回。

请记住，除非我们访问 object 属性，否则永远不会计算它的值。这意味着它不会执行 getter 函数，也不会事先将返回值赋给 object 属性。

# 创建 getters 时要记住的事情

*   它不应该有任何参数。
*   不应存在另一个同名的数据属性或 getter。

像数据属性一样，我们也可以删除 getters。

```
const obj = {
  get data() {
      return 'jscurious';
  }
}
delete obj.data;
console.log(obj.data); // undefined
```

# 作曲者

`set`关键字用于创建一个 setter 函数。`set`关键字将 setter 函数与同名的对象属性绑定在一起。因此，每当我们试图改变这个对象属性的值时，setter 函数就会被执行。

```
const obj = {
  msg: '',
  set message(value) {
    this.msg = value;
  }
}
obj.message = 'Hello';
console.log(obj.msg); // Hello
```

# 创建 setters 时要记住的事情

*   它应该只有一个参数。
*   不应存在另一个同名的数据属性或 setter。但是 getter 和 setter 可以同名。

像数据属性一样，我们也可以删除 setters。

```
const obj = {
  msg: '',
  set message(value) {
    this.msg = value;
  }
}
delete obj.message;
```

# 在类中使用 getter 和 setter

让我们创建一个封装类。该类将有一个私有字段，只能通过 setter 和 getter 访问。

```
class Square {
  #side_value;

  set side(value) {
    this.#side_value = value;
  }
  get side() {
    return this.#side_value;
  }
  get area() {
    return this.#side_value ** 2;
  }
}const sq = new Square();
sq.side = 25;
console.log(sq.side); // 25
console.log(sq.area); // 625
```

"**注:**字段名中的`#`表示类中的[私有字段](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)，不能在类外访问。`area` getter 函数中的`**`(或[取幂运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation))相当于`Math.pow()`。”

# 你可能也喜欢

*   [JavaScript 设置对象以存储唯一值](https://jscurious.com/javascript-set-object-to-store-unique-values/)
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [object . define property()方法简介](https://jscurious.com/object-defineproperty-method-in-javascript/)
*   [JavaScript 中的震动 API](https://jscurious.com/the-vibration-api-in-javascript/)
*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [object . freeze()vs object . seal()vs object . prevent extensions()](https://jscurious.com/difference-between-object-freeze-object-seal-and-object-preventextensions/)
*   [20+ JavaScript 速记编码技巧](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的宝贵时间:)*
***阿米塔夫·米什拉***

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*