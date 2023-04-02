# 99%的初学者不明白“for”循环和“forEach”之间的区别

> 原文：<https://javascript.plainenglish.io/99-of-beginners-do-not-understand-the-difference-between-for-loops-foreach-6cb0bc375595?source=collection_archive---------2----------------------->

## 让我们详细看看“for”和“forEach”的区别。

![](img/8114d39c70f75acfbb34f4223c5b09a3.png)

**我们先来看本质区别:**

“for”循环从 JavaScript 开始就存在了。ES5 中引入的‘forEach’是挂载在可迭代对象的原型上的，比如数组集合映射。

**‘forEach’**是负责遍历可迭代对象的迭代器。那么什么是遍历、迭代和可迭代对象呢？这个稍微详细一点，留给大家自己回顾。

知道' forEach '其实是一个迭代器，它和' for '循环的本质区别在于' forEach '负责遍历(数组集合映射)可迭代对象，而' for '循环是一个循环机制，但是它可以通过它遍历一个数组。

**解释:**什么是迭代器？这里，发电机作为一个例子。当它被调用时，会生成一个迭代器对象(iterator object)。它有一个. next()方法，每次调用返回一个对象{value:value，done:Boolean }，value 返回 yield 后的返回值，yield 结束时，done 变为 true，通过依次调用和迭代访问内部值。

迭代器是一种特殊的对象。在 ES6 规范中，它的标志是返回对象的 next()方法，迭代行为判断为 done。迭代器实现遍历而不公开内部表示。参见代码:

```
let arr = [4, 5, 6, 7] let iterator = arr[Symbol.iterator]() console.log(iterator.next()); console.log(iterator.next()); console.log(iterator.next()); console.log(iterator.next()); console.log(iterator.next());
```

从上面我们可以看到，只要是 iterable 对象，调用内部 Symbol.iterator 就会提供一个迭代器，根据迭代器返回的 next 方法访问内部，这也是 for…of 的实现原理。

```
let arr = [4, 5, 6, 7]
for (const item of arr) {
 console.log(item);
}
```

调用 next 方法返回对象的值并保存在 item 中直到 done 为 true 跳出循环，所有 iterable 对象都可以被 for…of 消耗。让我们看看其他可迭代对象:

```
function num(params) {
 console.log(arguments);
 let iterator = arguments[Symbol.iterator]()
 console.log(iterator.next());
 console.log(iterator.next());
 console.log(iterator.next());
 console.log(iterator.next());
 console.log(iterator.next());
}
num(4, 5, 6, 7)let set = new Set(‘4567’)
set.forEach(item => {
 console.log(item);
})
let iterator = set[Symbol.iterator]()
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

那么我们也可以直观的看到 iterable 对象中的 Symbol.iterator 属性在被调用时可以生成一个迭代器，forEach 也生成一个迭代器，在内部回调函数中传递每个元素的值。

**描述:我觉得这里调用的是迭代器，连续调用 next，给回调函数传递参数。可以在评论区留言，谈谈自己的看法。**

“for”循环和“forEach”之间的语法差异:

1.forEach 的参数。
2。中断 forEach。
3。forEach 删除它自己的元素，并且不能重置索引。
4。for 循环可以控制循环的起点。

**forEach 的参数**
让我们了解一下 forEach 的完整参数内容:

```
arr.forEach((self,index,arr) =>{},this)
```

**self:** 数组当前遍历的元素。默认情况下，数组元素按从左到右的顺序获取。

**index:** 数组当前元素的索引，第一个元素的索引为 0，以此类推。

**arr:** 当前遍历的数组。

**这个:**这个是指回调函数。

```
let arr = [4, 5, 6, 7];
let person = {
 name: ‘BOb’
};
arr.forEach(function (self, index, arr) {console.log(`${self} ${index}, ${arr}`);
 console.log(this.name+=’high’);
}, person)
```

我们可以使用 arr 来实现阵列重复数据消除:

```
let arr1 = [4, 5, 4, 6, 4];
let arr2 = [];
arr1.forEach(function (self, index, arr) {
 arr1.indexOf(self) === index ? arr2.push(self) : null;
});
console.log(arr2);
```

**forEach 中断**
JavaScript 中有 break-return-continue 中断函数或跳出循环。我们会在 for 循环中使用一些中断行为，这对于优化数组遍历和搜索非常好，但是因为 forEach 属于迭代器，只能按照顺序遍历完成的顺序进行排序，所以不支持上面的中断行为。

```
*let arr = [4,5,6,7],
i = 0,
length = arr.length;
for (; i < length; i++) {
console.log(arr[i]);
if (arr[i] === 5) {
break;
};
};*
```

```
*arr.forEach((self,index) => { 
 console.log(self);
 if (self === 5) {
 break;
 };
});*
```

```
*arr.forEach((self,index) => {* *console.log(self);
 if (self === 5) {
 continue;
 };
});*
```

如果我必须在 forEach 中跳出循环怎么办？事实上，有一种方法，借助于 try/catch:

```
*try {
 var arr = [4, 5, 6, 7];
 arr.forEach(function (item, index) {
 if (item ===6 ) {
 throw new Error(“LoopTerminates”);
 }** console.log(item);
 });
} catch (e) {
 if (e.message !== “LoopTerminates”) throw e;
};*
```

如果遇到 return，不会报告错误，但不会生效:

```
*let arr = [4, 5, 6, 7];**function find(array, num) {
 array.forEach((self, index) => {
 if (self === num) {
 return index;
 };
 });
};
let index = find(arr, 5);* 
```

**forEach 删除自己的元素，index 无法重置**
在 forEach 中，我们无法控制 index 的值，它只会无意识地递增，直到大于数组的长度，然后跳出循环。因此，不可能通过删除自身来重置索引。让我们看一个简单的例子:

```
*let arr = [4,5,6,7]
arr.forEach((item, index) => {
 console.log(item);
 index++;
});*
```

index 在函数体内增加或减少时不会改变。在实际开发中，遍历一个数组同时删除一个项是很常见的。使用 forEach 删除时要注意。

**for 循环可以控制循环的起点** 如上所述，forEach 循环的起点在没有人为干预的情况下只能是 0，但 for 循环则不同。

前面遍历数组删除育种的操作可以写成:

```
*let data = [];**let data2 = [1,2,3];**data2.map(item=>data.push(item));* 
```

**for 循环和 forEach 的性能差异**
在性能比较方面，我们增加了一个 map 迭代器，它和 filter 一样，生成一个新的数组。我们比较了 for forEach map 在浏览器环境中的性能:

**性能对比:对于 chrome 62 和 Node.js v9.1.0 环境下的>forEach>map**
:for 循环比 forEach 快 1 倍，forEach 比 map 快 20%左右。

**原因分析**

**for:**for 循环没有额外的函数调用栈和上下文，所以它的实现最简单。

**forEach:** 对于 forEach，其函数签名包含参数和上下文，所以性能会低于 for loop。

**map:**map 之所以最慢，是因为 map 返回一个新的数组，数组的创建和赋值会造成内存空间的分配，所以会带来较大的性能开销。如果映射嵌套在循环中，会带来更多不必要的内存消耗。

当使用迭代器遍历数组时，使用 map 而不返回新数组是违背设计意图的。

**感谢您的阅读，期待您的关注。**

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****