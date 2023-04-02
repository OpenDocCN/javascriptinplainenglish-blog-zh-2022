# 有用的 JavaScript 简写我希望我能早点知道

> 原文：<https://javascript.plainenglish.io/useful-javascript-shorthands-i-wish-i-knew-sooner-a1a3f3ad038b?source=collection_archive---------1----------------------->

## 减少 JavaScript 代码行最常用的快捷方式。

![](img/8f4df0bf2ba05206345cf7a2b1b6bcf8.png)

JavaScript 是一种漂亮的语言，它为常见的代码概念提供了一系列有用的简化方法。它们有利于减少代码行数，提高代码可读性。在这篇文章中，我总结了最常用的速记，并附上了引导你的简写。

1.  **使用 for 循环**

```
const fruits = ['apple', 'peach', 'banana'];
for (let i=0; i < fruits.length; i++) {}; // shorthand
for(let fruit of fruits)// if you want to access index only
for(let fruit in fruits)
```

**2。数学速记**

```
Math.floor(4.9) // shorthand
~~4.9 Math.pow(2,3);// shorthand
2**3
```

**3。查找功能**

```
const members = [
{gender: 'M', name: 'John'},
{gender: 'M', name: 'Tim'},
{gender: 'F', name: 'Jenny'},
{gender: 'F', name: 'Alice'}
]findTim = (name) => {
 for(let member of members) {
  if(member.name === name && member.gender === 'M') {
return member.name
} // shorthand
member = members.find(member => member.gender === 'M' && member.name === 'Tim');
```

**4。使用扩展运算符连接&克隆阵列**

```
const oddNumbers = [3,5,7]
const numbers = [2,4,6].concat(oddNumbers);
// shorthand
const numbers = [2,4,6,...oddNumbers];const array = [1,2,3];
const arrayClone = array.slice();//shorthand
const arrayClone = [...array];
```

**5。数字字符串**

```
const num1 = parseInt("100");
const num1 = parseFloat("100");// shorthand
const num1 = +"100";
```

**6。解构**

```
const id = this.props.id;
const title = this.props.title;
const author = this.props.author;// shorthand
const {id, title, author} = this.props;
```

**7。模板文字**

```
const db = "http://" + host + ":" + port + "/" + database;// shorthand
const db = `http://${host}:${port}/${database}`;
```

**8。声明变量**

```
let a = 3;
let b = 3;
let c = 3; //shorthand
let a=3, b=3, c = 3;
```

**9。三元运算符**

它是传统 if…else 语句的简写。

```
if (condition) {
  return "true"
} else {
  return "false"
}// shorthand
let condition = true;
let result = condition ? 'true' : 'false';
```

**10。无效合并运算符**

它用于将默认值赋给变量，运算符仅在预期值为空时使用默认值。

```
// case 1 
let value = null;
let finalValue = value ?? 'default value'; console.log(finalValue); // 'default value'// case 2
let value = 'intended value';
let finalValue = value ?? 'default value';console.log(finalValue);  // 'intended value'
```

**结论**

我希望上面的解释能帮助你理解代码。然而，在使用 shorthands 时必须小心谨慎，因为最重要的不是编写短代码，而是编写其他开发人员可以轻松阅读的清晰易懂的代码！

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。**