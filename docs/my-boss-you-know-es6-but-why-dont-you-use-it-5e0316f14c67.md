# 我老板:你知道 ES6，为什么不用？😠

> 原文：<https://javascript.plainenglish.io/my-boss-you-know-es6-but-why-dont-you-use-it-5e0316f14c67?source=collection_archive---------0----------------------->

老板的 10 条抱怨让我受益匪浅。

![](img/2e8fb3b4742f1e1da2c9873ef1fa0476.png)

# 前言

这就是我的老板在代码评审会议上对团队成员咆哮的方式。原因是他发现项目的许多部分仍然在使用 ES5。不是说 ES5 不好，会有 bug，但是会增加代码量，降低可读性。

碰巧我的老板有代码整洁的习惯。涉及到 3 到 5 年经验的员工，他对这个级别的代码极其不满意，不断抱怨代码。不过我还是觉得从他的抱怨中收获很大，所以决定把老板的抱怨录下来，分享给大家。

# 1.关于提取对象值的投诉

提取属性值在程序中很常见，比如从对象 obj 中获取值。

```
const obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  e: 5,
}const a = obj.a
const b = obj.b
const c = obj.c
const d = obj.d
const e = obj.e*// or*
const f = obj.a + obj.d
const g = obj.c + obj.e
```

**老板抱怨**:你为什么不用 ES6 的析构赋值来取值？用 1 行代码做不是更好吗？

```
const { a, b, c, d, e } = obj
const f = a + d
const g = c + e
```

**我反对**:我不用 ES6，因为 API 接口属性名不是我想要的。

**老板抱怨**:看来你还没有完全掌握 ES6 的破坏任务。如果要创建的变量名与对象的属性名不一致，可以这样写:

```
const { a: a1 } = obj || {}console.log(a1)*// 1*
```

# 2.关于合并数据的投诉

比如合并两个数组或者合并两个对象。

```
const a = [ 1, 2, 3 ]
const b = [ 1, 5, 6 ]
const c = a.concat(b) *// [ 1, 2, 3, 1, 5, 6]*const obj1 = {
  a:1,
}
const obj2 = {
  b:1,
}
const obj = Object.assign({}, obj1, obj2) *// { a: 1, b: 1}*
```

**老板的抱怨**:你是不是忘了 ES6 spread 运算符，阵列合并不考虑重复数据删除？

```
const a = [ 1, 2, 3 ]
const b = [ 1, 5, 6 ]
const c = [...new Set([...a,...b])] *// [ 1, 2, 3, 5, 6 ]*const obj1 = {
  a:1,
}
const obj2 = {
  b:1,
}
const obj = {...obj1,...obj2} *// { a: 1, b: 1 }*
```

# 3.关于拼接线的投诉。

```
const name = 'fatfish'
const score = 59
let result = ''if(score > 60){
  result = `${name}passed the exam` 
}else{
  result = `${name}failed in the exam` 
}
```

**老板抱怨**:你这样还不如不用 ES6 字符串模板。你不知道`${}`里可以做操作？我们可以在`${}`中执行任意的 JavaScript 表达式，执行操作，引用对象属性。

```
const name = 'fatfish'
const score = 59
const result = `${name}${score > 60 ? 'passed the exam' : 'failed in the exam'}`
```

# 4.关于使用 if 的投诉

```
if(
    type == 1 ||
    type == 2 ||
    type == 3 ||
    type == 4 ||
){
   *//...*
}
```

**老板的抱怨**:我们在 ES6 中使用数组的 includes 方法不是更好吗？

```
const condition = [ 1, 2, 3, 4 ]if( condition.includes(type) ){
   *//...*
}
```

# 5.关于列表搜索的投诉。

在项目中，有些列表的搜索功能是由前端实现的，搜索一般分为精确和模糊两种。一般我们用过滤的方法来实现。

```
const a = [ 1, 2, 3, 4, 5 ]
const result = a.filter( 
  item => {
    return item === 3
  }
)
```

老板的抱怨:你不会使用 ES6 中的 find 方法进行精确搜索吗？你懂性能优化吗？如果在 find 方法中找到符合条件的项，它将不会继续遍历数组。

```
const a = [ 1, 2, 3, 4, 5 ]
const result = a.find(item => item === 3)
```

# 6.对平面阵列的抱怨。

在 JSON 数据中，属性名是部门 id，值是部门雇员的 id 数组。现在我们需要将 department 的所有成员 id 提取到一个数组集合中。

```
const deps = {
    'department_1':[ 1, 2, 3 ],
    'department_2':[ 5, 8, 12 ],
    'department_3':[ 5, 14, 79 ],
    'department_4':[ 3, 64, 105 ],
}
let member = []for (let item in deps){
    const value = deps[item]
    if(Array.isArray(value)){
        member = [...member,...value]
    }
}
member = [...new Set(member)]
```

**BOSS 的抱怨**:我需要遍历获取对象的所有属性值吗？你忘了 Object.values？为什么不用 ES6 提供的扁平化方法？

```
const deps = {
    'department_1':[ 1, 2, 3 ],
    'department_2':[ 5, 8, 12 ],
    'department_3':[ 5, 14, 79 ],
    'department_4':[ 3, 64, 105 ],
}
let member = Object.values(deps).flat(Infinity)
```

> 备注:使用 Infinity 作为 flat 的参数，所以我们不需要知道 flattened 数组的维数。

# 7.关于获取对象属性值的抱怨。

```
const name = obj && obj.name
```

**老板的抱怨**:你不会在 ES6 中使用可选的链式操作符吗？

```
const name = obj?.name
```

# 8.关于添加对象属性的抱怨。

当我们给一个对象添加属性时，如果属性名动态变化，我们该怎么办？

```
let obj = {}
let index = 1
let key = `topic${index}`obj[key] = 'content'
```

**老板的抱怨**:为什么要创造一个额外的变量。不知道 ES6 中的对象属性名可以用表达式吗？

```
let obj = {}
let index = 1obj[`topic${index}`] = 'content'
```

# 9.对非空判断的抱怨

在处理用户输入时，经常要判断输入框是否已经输入。

```
if(value !== null && value !== undefined && value !== ''){
    *//...*
}
```

**老板的抱怨**:你听说过 ES6 中新的空值合并运算符吗，要写这么多条件吗？

```
if((value ?? '') !== ''){
  *//...*
}
```

# 10.对异步功能的抱怨

异步函数很常见，并且经常作为承诺来实现。

```
const fn1 = () =>{
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(1)
    }, 300)
  })
}
const fn2 = () =>{
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(2)
    }, 600)
  })
}
const fn = () =>{
  fn1().then(res1 =>{
    console.log(res1) *// 1*
    fn2().then(res2 =>{
      console.log(res2)
    })
  })
}
```

**老板的抱怨**:你这样用异步函数，不怕形成回调地狱！

```
const fn = async () =>{
  const res1 = await fn1()
  const res2 = await fn2() console.log(res1) *// 1*
  console.log(res2) *// 2*
}
```

# 最后

欢迎你尝试反驳以上 10 条老板投诉。如果你的反驳是合理的，我会在下次代码审查会上为你反驳。

*本文翻译已获原作者(洪陈连新)授权。*

*原地址为*[*https://juejin.cn/post/7016520448204603423*](https://juejin.cn/post/7016520448204603423)

**感谢您的阅读。**

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*