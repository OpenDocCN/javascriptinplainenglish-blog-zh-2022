# 关于 JavaScript 数组您需要知道的一切

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-javascript-arrays-6ea79a6b8fd5?source=collection_archive---------14----------------------->

## 这里列出了几乎所有你想在数组上执行的操作，以及如何在 JavaScript 中执行。

![](img/d9b1fc29d4acd2713a58e88ba0f7af26.png)

对于数组，通常有一组你想要实现的特定的事情。下面是你想在数组上执行的几乎所有操作的列表，以及如何在 JavaScript 中执行。如果你还有更多，请在下面的评论中告诉我。

# 1.通过值查找元素的索引

使用`indexOf`:

```
let arr1 = [ 'potato', 'banana', 'ravioli', 'carrot' ];// Returns 1
console.log(arr1.indexOf('banana'));// Returns -1 since not found
console.log(arr1.indexOf('beetroot'));
```

# 2.在索引处删除

使用`splice()`:

```
let arr1 = [ 'potato', 'banana', 'ravioli', 'carrot' ];// Returns [ 'banana', 'ravioli', 'carrot' ], since potato has index 0.
arr1.splice(0, 1);
console.log(arr1);
```

# 3.按值在索引处删除

使用`splice()`和`indexOf`:

```
let arr1 = [ 'potato', 'banana', 'ravioli', 'carrot' ];
let itemIndex = arr1.indexOf('ravioli');// Returns [ 'potato', 'banana', 'carrot' ], since ravioli has an index of 2
arr1.splice(itemIndex, 1);
console.log(arr1);
```

# 4.获取数组的最后一个元素

使用`arr.length() - 1`:

```
let arr1 = [ 'potato', 'banana', 'ravioli', 'carrot' ];// Returns carrot
console.log(arr1[arr1.length - 1]);
```

# 5.在索引处插入

使用`splice()`。[你也可以在这里阅读关于插入索引的详细内容](https://fjolt.com/article/javascript-how-to-insert-at-index-array)。

```
let arr1 = [ 'potato', 'banana', 'ravioli', 'carrot' ];// Inserts broccoli at position 2, after deleting 0 items
arr1.splice(2, 0, 'broccoli');// Returns [ 'potato', 'banana', 'ravioli', 'brccoli', 'carrot' ]
console.log(arr1);
```

# 6.移除数组的最后一个元素

使用`pop()`:

```
let arr1 = [ 1, 2, 3, 4, 5, 6 ];// Returns 6
console.log(arr1.pop()); // Returns [ 1, 2, 3, 4, 5 ] - last element is removed
console.log(arr1);
```

# 7.以同样的方式改变数组的所有值

使用`map()`:

```
let arr1 = [ 1, 2, 3, 4, 5, 6 ];let newArr = arr1.map(function(arrElement) {
    return arrElement + 3;
})// ES6 version for modern browsers and NodeJS
let anotherVersion = arr1.map( el => el + 3);// Returns [ 4, 5, 6, 7, 8, 9 ] for both
console.log(newArr);
console.log(anotherVersion);
```

# 8.将字符串、映射或集合转换为数组

使用`Array.from()`:

```
let newSet = new Set([ 'orange', 'apple', 'potato', 'spinach' ]);
let newMap = new Map([ 'orange', 'apple', 'potato', 'spinach' ]);
let newString = 'apple';console.log(Array.from(newSet)); // Returns [ 'orange', 'apple', 'potato', 'spinach' ]
console.log(Array.from(newMap)); // Returns [ 'orange', 'apple', 'potato', 'spinach' ]
console.log(Array.from(newString)); // Returns [ 'a', 'p', 'p', 'l', 'e' ]
```

# 9.检查它是否是一个数组

使用`Array.isArray()`:

```
let arr1 = [ 'orange', 'apple', 'potato', 'spinach' ];
let obj1 = { myKey: "myValue" }console.log(Array.isArray(arr1)); // Returns true
console.log(Array.isArray(obj1)); // Returns false
```

# 10.检查数组中的每个元素

使用`forEach`:

```
let arr1 = [ 'orange', 'apple', 'potato', 'spinach' ];arr1.forEach(function(item) {
    console.log(item); // Returns each array item individually
});
```

# 11.合并两个数组

使用`...`或`concat`:

```
let arr1 = [ 'orange', 'apple' ];
let arr2 = [ 'potato', 'spinach' ];// For legacy browsers (ES5);
// Returns [ 'orange', 'apple', 'potato', 'spinach' ]; 
let someArray = arr1.concat(object);// For modern Javascript (ES6/NodeJS)
// Returns [ 'orange', 'apple', 'potato', 'spinach' ]; 
let someOtherArray = [ ...arr1, ...arr2 ];
```

# 12.将对象名转换成数组

使用`Object.keys`:

```
let object = { 
    name1: "value",
    name2: "value",
    name3: "value"
};// Returns [ 'name1', 'name2', 'name3' ]; 
let array = Object.keys(object);
```

# 13.将对象值转换成数组

使用`Object.values`:

```
let object = { 
    name1: "value",
    name2: "value",
    name3: "value"
};// Returns [ 'value', 'value', 'value' ]; 
let array = Object.values(object);
```

# 14.反转数组

使用`reverse()`:

```
let arr1 = [ 'potato', 'banana', 'carrot' ];arr1.reverse();// Returns [ 'carrot', 'banana', 'potato' ]
console.log(arr1);
```

# 15.对数组中的所有元素求和

使用`reduce()`:

```
let arr1 = [ 1, 2, 3, 4, 5 ];// For legacy browsers
let getTotal = arr1.reduce(function (accumulator, currentNumber) {
    return accumulator + currentNumber
});// ES6 for modern browsers and NodeJS
let theTotal = arr1.reduce((accumulator, currentNumber) => accumulator + currentNumber);// Returns 15
console.log(getTotal);
```

# 16.将元素添加到数组的末尾

使用`push()`:

```
let arr1 = [ 'banana', 'potato' ];arr1.push('broccoli');// Returns [ 'banana', 'potato', 'broccoli' ]
console.log(arr1);
```

# 17.检查数组的每个元素是否都通过了测试

使用`every()`

```
let arr1 = [ 1, 2, 3, 4, 5, 6, 7 ];// Will return true and console log 'great'
if(arr1.every(value => value < 10)) {
    console.log('great!')
}
```

这个题目到此为止。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***