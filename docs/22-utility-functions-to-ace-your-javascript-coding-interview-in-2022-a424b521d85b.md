# 2022 年 JavaScript 编码面试中的 22 个实用函数

> 原文：<https://javascript.plainenglish.io/22-utility-functions-to-ace-your-javascript-coding-interview-in-2022-a424b521d85b?source=collection_archive---------3----------------------->

## JavaScript 编码评估备忘单 2022

![](img/a1731156db02a6268a8e56a4db569d4f.png)

Photo by [J. Kelly Brito](https://unsplash.com/@heykellybrito?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您可能会遇到的一种 JavaScript 编码面试问题涉及到您为给定的问题编写 1-2 行代码。这些问题通常很简单，可以在 5 分钟内回答，但有时我们会因为面试的压力而纠结。这些功能将帮助你为 2022 年的 JavaScript 面试做好准备。

为了减轻压力，我们提前做好准备吧！

# 1.从数组中删除重复项

*   数组:这些是我们可以用来从一个数组中删除重复项的简便方法。

1.  **使用 lodash**

```
let array = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let arrayuniq = _.uniq(array);//*[2, 1, 5, 6, 7, 8, 9, 10]*
```

2.**使用过滤器**

```
let array = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let list = array.filter((x, i, a) => a.indexOf(x) == i);//*[2, 1, 5, 6, 7, 8, 9, 10]*
```

3.**使用设定**

```
let array = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let setuniq = [...new Set(array)];//*[2, 1, 5, 6, 7, 8, 9, 10]*
```

# 2.从对象数组中删除重复项

*   **对象数组:**这些是我们可以用来从一个对象数组中删除重复项的简便方法。

1.  **使用 lodash**

```
let users = [{ id: 1, name: "ted" },{ id: 1, name: "bob" },{ id: 3, name: "sara" },{ id: 4, name: "test" },{ id: 4, name: "test" },{ id: 5, name: "abc" }];let uniqueUsersByID = _.uniqBy(users, "id");//[{"id":1,"name":"ted"},{"id":3,"name":"sara"},{"id":4,"name":"test"},{"id":5,"name":"abc"}]
```

使用此代码，我们可以检查具有多个属性的唯一数据。

```
const uniquewithMultipleProperties = _.uniqWith(
    users,
    (a, b) => a.id === b.id || a.name === b.name
);
//[{"id":1,"name":"ted"},{"id":3,"name":"sara"},{"id":4,"name":"test"},{"id":5,"name":"abc"}]
```

2.**使用过滤器**

```
let filteruniquebyID = users.filter(
    (v, i, a) => a.findIndex(t => t.id === v.id) === i
);
//[{"id":1,"name":"ted"},{"id":3,"name":"sara"},{"id":4,"name":"test"},{"id":5,"name":"abc"}]
```

使用此代码，我们可以检查具有多个属性的唯一数据。

```
let filteruniquebyIDName = users.filter(
    (v, i, a) => a.findIndex(t => t.id === v.id || t.name === v.name) === i
);
//[{"id":1,"name":"ted"},{"id":3,"name":"sara"},{"id":4,"name":"test"},{"id":5,"name":"abc"}]
```

3.**使用设定**

```
var set1 = Array.from(users.reduce((m, t) => m.set(t.id, t), new Map()).values());//[{"id":1,"name":"bob"},{"id":3,"name":"sara"},{"id":4,"name":"test"},{"id":5,"name":"abc"}]
```

你可以在这里查看 StackBlitz。

[https://stack blitz . com/edit/remove-duplicates-arrayofobjects](https://stackblitz.com/edit/remove-duplicates-arrayofobjects)

# 3.在数组中查找项目

*   下面是一些在数组中查找项目的方法

1.  **includes:** 该方法确定数组的条目中是否包含某个值，根据情况返回`true`或`false`。

```
console.log(array.includes(2)); // returns true
```

2. **every:** 该方法测试数组中的所有元素是否通过了由提供的函数实现的测试。它返回一个布尔值。

```
let testevery1 = array.every(val=> val>3); //false
```

3. **some:** 该方法测试数组中是否至少有一个元素通过了所提供函数实现的测试。它返回一个布尔值。

```
let testsome1 = array.some(val=> val>3); //true
```

4. **lodash 包括:**检查`value`是否在`collection`中。如果找到了`value`，则返回`true`，否则返回`false`。

```
let lodashtest9 =_.includes(array, 1); // truelet lodashtest10 =_.includes(array, 3, 2); // false
```

5. **findIndex:** 该方法返回满足提供的测试函数的数组**中第一个元素的**索引**。否则返回`-1`，表示没有元素通过测试。**

```
let  testindex = array.findIndex(val => val > 1);
//0
```

6. **find:** 该方法返回所提供数组中满足所提供测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`。

```
let testfind = array.find(el => (el > 2));
//5
```

**7。filter:** 这个方法**创建一个新的数组**，所有通过测试的元素都由提供的函数实现。

```
let testfilter1 = array.filter(val=> val>3);
//*[5, 6, 7, 8, 9, 9, 10]*
```

8. **map:** 这个方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。

```
let val = [];
array.map(item => { if(item >= 3) val.push(item); });
//*[5, 6, 7, 8, 9, 9, 10]*
```

你可以在这里查看 StackBlitz。

[https://stackblitz.com/edit/find-item-array](https://stackblitz.com/edit/find-item-array)

# 4.在对象数组中查找项目

*   这些是可用于在对象数组中查找项目的方法。

1. **every:** 该方法测试数组中的所有元素是否通过了由提供的函数实现的测试。它返回一个布尔值。

```
let testevery2 = users.every(val=> val.id>3);
//false
```

2. **some:** 该方法测试数组中是否至少有一个元素通过了所提供函数实现的测试。它返回一个布尔值。

```
let testsome2 = users.some(val=> val.id>3); //true
```

3. **lodash 包括:**检查`value`是否在`collection`内。如果找到了`value`，则返回`true`，否则返回`false`。

```
let lodashtest11 =_.includes({ 'a': 1, 'b': 2 }, 1);
//true
let lodashtest12 =_.includes('abcd', 'bc');
//true
```

4. **findIndex:** 该方法返回满足提供的测试函数的数组**中第一个元素的**索引**。否则返回`-1`，表示没有元素通过测试。**

```
let  testindex2 = users.findIndex(val => val.id > 1);
//3
```

5. **find:** 该方法返回所提供数组中满足所提供测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`。

```
let testfind2 = users.find(el => (el.id > 2));
//{"id":3,"name":"sara"}
```

**6。filter:** 这个方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。

```
let testfilter2 = users.filter(val=> val.id>3);
```

7. **map:** 这个方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。

```
let val2 = [];users.map(item => { if(item.id >= 3) val2.push(item); });
```

你可以在这里查看 StackBlitz。

[https://stackblitz.com/edit/find-item-array](https://stackblitz.com/edit/find-item-array)

# 5.排序数组项目

可以使用 sort 方法对数组进行排序。

`**sort()**`方法将数组 [*中的元素在*](https://en.wikipedia.org/wiki/In-place_algorithm) 中排序，并返回排序后的数组。默认的排序顺序是升序，建立在将元素转换为字符串，然后比较它们的 UTF-16 代码单元值序列的基础上。

```
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```

# 6.具有特定属性的对象的排序数组

*   这些方法可用于使用对象的特定属性对对象数组进行排序。

**1。简单排序:**该方法对数组 [*中的元素进行排序，并返回排序后的数组。*](https://en.wikipedia.org/wiki/In-place_algorithm)

```
let data = [{
        id: "3",
        city: "toronto",
        state: "TR",
        zip: "75201",
        price: "123451"
    },
    {
        id: "1",
        city: "anand",
        state: "AN",
        zip: "94210",
        price: "345678"
    },
    {
        id: "5",
        city: "sudbury",
        state: "SB",
        zip: "00110",
        price: "789045"
    }
];let sorttest2 = data.sort((a, b) => (a.id < b.id ? -1 : Number(a.id > b.id)));console.log("sort test 2 ", sorttest2);//output
{
    "id": "1",
    "city": "anand",
    "state": "AN",
    "zip": "94210",
    "price": "345678"
}, {
    "id": "3",
    "city": "toronto",
    "state": "TR",
    "zip": "75201",
    "price": "123451"
}, {
    "id": "5",
    "city": "sudbury",
    "state": "SB",
    "zip": "00110",
    "price": "789045"
}]
```

**2。localCompare:** 这个方法返回一个数字，指示一个引用字符串在排序顺序中是在给定字符串之前还是之后，或者是否与给定字符串相同。

```
let sorttest2 = data.sort((a, b) => (a.id < b.id ? -1 : Number(a.id > b.id)));//output
[{
    "id": "1",
    "city": "anand",
    "state": "AN",
    "zip": "94210",
    "price": "345678"
}, {
    "id": "3",
    "city": "toronto",
    "state": "TR",
    "zip": "75201",
    "price": "123451"
}, {
    "id": "5",
    "city": "sudbury",
    "state": "SB",
    "zip": "00110",
    "price": "789045"
}]
```

**3。多字段排序**

`**parseInt()**`函数解析字符串参数并返回指定的[基数](https://en.wikipedia.org/wiki/Radix)(数学数字系统中的基数)的整数。

```
let sorttest4 = data.sort(function(left, right) {
    var city_order = left.city.localeCompare(right.city);
    var price_order = parseInt(left.price) - parseInt(right.price);
    return city_order || -price_order;
});//output
[{
    "id": "1",
    "city": "anand",
    "state": "AN",
    "zip": "94210",
    "price": "345678"
}, {
    "id": "5",
    "city": "sudbury",
    "state": "SB",
    "zip": "00110",
    "price": "789045"
}, {
    "id": "3",
    "city": "toronto",
    "state": "TR",
    "zip": "75201",
    "price": "123451"
}]
```

**4。Lodash _sortBy:** 创建一个元素数组，按照每次迭代运行集合中每个元素的结果，按升序排序。

```
let sorttest6 = _.sortBy(data, ["id", "city"]);
//output
[{
    "id": "1",
    "city": "anand",
    "state": "AN",
    "zip": "94210",
    "price": "345678"
}, {
    "id": "3",
    "city": "toronto",
    "state": "TR",
    "zip": "75201",
    "price": "123451"
}, {
    "id": "5",
    "city": "sudbury",
    "state": "SB",
    "zip": "00110",
    "price": "789045"
}]
```

# 7.日期排序数组

**1。使用排序**

```
let isDescending = false; //set to true for Descending
let dates = ["1/7/2021", "1/6/2021", "8/18/2020", "8/6/2020"];let sorteddates = dates.sort((a, b) => isDescending ? new Date(b).getTime() - new Date(a).getTime() : new Date(a).getTime() - new Date(b).getTime());console.log(sorteddates);
//*["8/6/2020", "8/18/2020", "1/6/2021", "1/7/2021"]*
```

**2。使用 Lodash**

```
let arr = [{
        name: "test1",
        date: "1/7/2021"
    },
    {
        name: "test2",
        date: "1/6/2021"
    },
    {
        name: "test3",
        date: "1/5/2020"
    }
];
arr = _.sortBy(arr, function(dateObj) {
    return new Date(dateObj.date);
});
console.log("sort date", arr);
//[{"name":"test3","date":"1/5/2020"},{"name":"test2","date":"1/6/2021"},{"name":"test1","date":"1/7/2021"}]
```

**3。使用 Lodash(按年月排序)**

```
let  yearAndMonth  =  [
    { "year": 2016, "month": "FEBRUARY" },
    { "year": 2015, "month": "MARCH" },
    { "year": 2021, "month": "JANUARY" },
    { "year": 2021, "month": "FEBRUARY" }
]let value= _.sortBy(yearAndMonth, a => new Date(1 + a.month + a.year));
console.log('Sorted Result: ', value);
//[{"year":2015,"month":"MARCH"},{"year":2016,"month":"FEBRUARY"},{"year":2021,"month":"JANUARY"},{"year":2021,"month":"FEBRUARY"}]
```

你可以在这里查看 StackBlitz。

[https://stackblitz.com/edit/sort-array](https://stackblitz.com/edit/sort-array)

# 8.从数组中删除项目

**1。pop:** 该方法从数组中移除最后一个**元素并返回该元素。此方法更改数组的长度。**

```
let arraypoptest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];let testpop = arraypoptest.pop();
console.log("array pop", testpop,"-", arraypoptest);
//10 - [2, 1, 2, 5, 6, 7, 8, 9, 9];
```

**2。shift:** 这个方法从数组中移除第一个元素并返回移除的元素。此方法更改数组的长度。

```
let arrayshifttest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let testshift = arrayshifttest.shift();
console.log("array shift", testshift,"-", arrayshifttest);
//2 - [1, 2, 5, 6, 7, 8, 9, 9, 10]
```

**3。slice:** 这个方法将数组的一部分的浅拷贝返回到从`start`到`end`(不包括`end`)中选择的一个新的数组对象中，其中`start`和`end`表示该数组中项目的索引。原始数组不会被修改。

```
let arrayslicetest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let testslice = arrayslicetest.slice(0, 3);
console.log("array slice", testslice, arrayslicetest); 
//not changed original array
//[2, 1, 2] - [2, 1, 2, 5, 6, 7, 8, 9, 9, 10]
```

**4。splice:** 该方法通过移除或替换现有元素和/或在适当的位置添加新元素[来改变数组的内容。](https://en.wikipedia.org/wiki/In-place_algorithm)

```
let arraysplicetest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let testsplice = arrayslicetest.splice(0, 3);
//[2, 1, 2]
```

**5。filter:** 这个方法**创建一个新的数组**，其中所有通过测试的元素都由提供的函数实现。

**数组:**

```
let testarr = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let testarr2 = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let filtered = testarr.filter(function(value, index, arr) {
    return value > 5;
});
let filtered2 = testarr2.filter(item => item !== 2);
console.log("filter example 1", filtered);
//[6, 7, 8, 9, 9, 10]
console.log("filter example 2", filtered2);
//[1, 5, 6, 7, 8, 9, 9, 10]
```

*   **移除多个值的过滤器:**

```
let forDeletion = [2, 3, 5];
let mularr = [1, 2, 3, 4, 5, 3];
mularr = mularr.filter(item => !forDeletion.includes(item));
console.log("multiple value deletion with filter", mularr);
//[1, 4]
```

6。删除操作符:JavaScript`**delete**`**从对象中删除一个属性；如果不再持有对同一属性的引用，它最终会自动释放。**

```
let ar = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
delete ar[4]; // delete element with index 4
console.log(ar);
//[2, 1, 2, 5, undefined, 7, 8, 9, 9, 10]
```

****7。lodash remove:** `_remove`从`array`中移除`predicate`返回 the 的所有元素，并返回移除元素的数组。**

```
let arrlodashtest = [2, 1, 2, 5, 6, 7, 8, 9, 9, 10];
let evens = _.remove(arrlodashtest, function(n) {
    return n % 2 == 0;
});
console.log("lodash remove array", arrlodashtest);
//[1, 5, 7, 9, 9]
```

# **9.从对象数组中移除一项**

****1。pop:** 该方法从数组中移除最后一个**元素并返回该元素。此方法更改数组的长度。****

```
let users1 = [{
    id: 1,
    name: "ted"
}, {
    id: 2,
    name: "mike"
}, {
    id: 3,
    name: "bob"
}, {
    id: 4,
    name: "sara"
}];let testpop1 = users1.pop();console.log(
    "array of objects pop",
    JSON.stringify(testpop1),"-"
    JSON.stringify(users1)
);
//{"id":4,"name":"sara"} - [{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

****2。shift:** 这个方法从数组中移除第一个元素并返回移除的元素。此方法更改数组的长度。**

```
let users2 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testshift1 = users2.shift();console.log("array of objects shift", JSON.stringify(testshift1),"-", JSON.stringify(users2));
//{"id":1,"name":"ted"} - [{"id":2,"name":"mike"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

****3。slice:** 该方法将数组的一部分的浅拷贝返回到从`start`到`end`(不包括`end`)中选择的新数组对象中，其中`start`和`end`表示该数组中项目的索引。原始数组不会被修改。**

```
let users3 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testslice1 = users3.slice(0, 3);console.log("array of objects slice", JSON.stringify(testslice1));
//not changed original array
//[{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

****4。拼接:**该方法通过移除或替换现有元素和/或在位置添加新元素[来改变数组的内容。](https://en.wikipedia.org/wiki/In-place_algorithm)**

```
let users4 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let testspice1 = users3.splice(0, 3);console.log("array of objects splice", JSON.stringify(testsplice));
//[{"id":1,"name":"ted"},{"id":2,"name":"mike"},{"id":3,"name":"bob"}]
```

****5。filter:** 这个方法**创建一个新的数组**，其中所有通过测试的元素都由提供的函数实现。**

```
let users7 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let filterObj = users7.filter(item => item.id !== 2);console.log("filter example array of objects", filterObj);//[{"id":1,"name":"ted"},{"id":3,"name":"bob"},{"id":4,"name":"sara"}]
```

****6。lodash remove:** `_remove`从`array`中移除`predicate`返回 the 的所有元素，并返回一个移除元素的数组。**

```
let users8 = [{ id: 1, name: "ted" },{ id: 2, name: "mike" },{ id: 3, name: "bob" },{ id: 4, name: "sara" }];let evensObj = _.remove(users8, function(n) {
    return n.id % 2 == 0;
});console.log("lodash remove array of object", JSON.stringify(evensObj));//[{"id":2,"name":"mike"},{"id":4,"name":"sara"}]
```

**你可以在这里查看 StackBlitz。**

**[https://stackblitz.com/edit/array-remove-item](https://stackblitz.com/edit/array-remove-item)**

# **10.在数组中查找给定字符串的字符数**

****1。字符串匹配方法****

**`**match()**`方法检索将*字符串*与[正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)匹配的结果。(来源: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/) )**

```
const test1 = ("atit patel".match(/a/g)||[]).lengthconsole.log(test1); //2
```

****2。字符串拆分方法****

**`**split()**`方法将一个`[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)`分成一个有序的子字符串列表，将这些子字符串放入一个数组，并返回该数组。**

```
const test2 ="atit patel".split("a").length-1console.log(test2); //2
```

****3。方法索引****

**`**indexOf()**`方法返回第一次出现指定值的调用`[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)`对象中的索引，从`fromIndex`开始搜索。如果找不到该值，则返回`-1`。**

```
let  stringsearch = "a" ,str = "atit patel";for(var count=-1,index=-2; index != -1; count++,index=str.indexOf(stringsearch,index+1) );console.log(count); //2
```

****4。过滤方法****

**`**filter()**`方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。**

```
const mainStr = 'atit patel';const test3 = [...mainStr].filter(l => l === 'a').length;console.log(test3); //2
```

****5。减少方法****

**`**reduce()**`方法对数组的每个元素执行一个 **reducer** 函数(您提供的),产生一个输出值。**

```
const mainStr1 = 'atit patel';const test4 = [...mainStr1].reduce((a, c) => c === 'a' ? ++a : a, 0);console.log(test4); //2
```

# **11.查找数组中给定字符串中每个字符出现的次数**

****1。我们可以添加 reduce 方法，我们可以在迭代后返回对象****

```
let s = 'atit patel';let test5 = [...s].reduce((a, e) => { a[e] = a[e] ? a[e] + 1 : 1; return a }, {});console.log(test5); //{a: 2,e: 1,i: 1,l: 1,p: 1,t: 3}
```

****2。与方法 6 相同，使用“或”运算符****

```
let test6 = [...s].reduce((res, char) => (res[char] = (res[char] || 0) + 1, res), {})console.log(test6);//{a: 2,e: 1,i: 1,l: 1,p: 1,t: 3}
```

**你可以在这里玩积木。**

**[https://stackblitz.com/edit/numberofoccurance-string](https://stackblitz.com/edit/numberofoccurance-string)**

# **12.重命名对象数组中的对象属性**

****1。使用 Map:** 这个方法**创建一个新的数组**，用调用数组中每个元素的函数的结果填充。**

```
let countries = [{ id: 1, name: "india" },{ id: 2, name: "canada" },{ id: 3, name: "america" }];const transformed = countries.map(({ id, name }) => ({label: id,value: name}));console.log("1", JSON.stringify(transformed));[{"label":1,"value":"india"},{"label":2,"value":"canada"},{"label":3,"value":"america"}]
```

****2。使用带参数的地图****

```
const transformed2 = countries.map(({ id: label, name: value }) => ({label,value}));console.log("2", JSON.stringify(transformed2));[{"label":1,"value":"india"},{"label":2,"value":"canada"},{"label":3,"value":"america"}]
```

****3。使用 lodash:** `_.mapKeys`方法创建一个与`object`具有相同值的对象，并通过运行`object`到`iteratee`各自的可枚举字符串 keyed 属性生成关键字。**

```
const test1= _.mapKeys({ a: 1, b: 2 }, function(value, key) {return key + value;});console.log("3",test1);
//*{a1: 1, b2: 2}*
```

**如果我们想重命名对象键呢？让我们来看看解决方案。**

****4。对值的对象使用 lodash****

```
var users = {'atit':    { 'user': 'atit',    'age': 40 },'mahesh': { 'user': 'mahesh', 'age': 15 }};const test2 = _.mapValues(users, function(o) { return o.age; });console.log("4",test2);
//*{atit: 40, mahesh: 15}*//shorthandconst test3 =_.mapValues(users, 'age');console.log("5",test3);
//*{atit: 40, mahesh: 15}*
```

****5。使用对象析构:****析构赋值**语法是一个 JavaScript 表达式，它可以将数组中的值或对象中的属性解包到不同的变量中。**

```
const rename = (({id: a_b_c, ...rest}) => ({a_b_c, ...rest}))console.log(rename({id: 1, val: 2}))
//*{a_b_c: 1, val: 2}*
```

**你可以在这里玩积木。**

**【https://stackblitz.com/edit/rename-object-keys】**

# **13.如何合并两个数组，创建一个新的数组？**

**这可以简单地通过使用 spread 运算符来实现。**

```
var arr1 = ['a', 'b', 'c']
var arr2 = ['d', 'e']var merged = [...arr1, ...arr2]console.log(merged)
```

# **14.一组数字的总和**

1.  ****reduce** 可用于遍历数组，将当前元素值加到之前元素值的总和上。**

```
console.log(
  [1, 2, 3, 4].reduce((a, b) => a + b, 0)
)
console.log(
  [].reduce((a, b) => a + b, 0)
)//10
```

****2。使用 Lodash****

```
array = [1, 2, 3, 4];
sum = _.sum(array); // sum == 10
```

> ***让我们检查一些对编码评估有帮助的复杂场景***

# **15.比较两个对象数组，删除重复项，根据属性合并对象**

**我们确实需要比较两个不同的对象数组，如果它们匹配特定的属性值，我们希望合并这两个对象。这可以通过使用过滤方法来实现。**

**`**filter()**`方法**创建一个新数组**，其中所有通过测试的元素都由提供的函数实现。(来源: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) )**

**让我们创建测试数据。**

```
let array1 = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 }];let array2 = [{ id: "53", active: "a", value: 10 },{ id: "51", active: "a", value: 11 },{ id: "52", active: "a", value: 13 }];
```

***让我们创建函数。***

```
let res = array2.filter(val =>
    array1.some(({
        value
    }) => (val.value as any) === (value as any))
);console.log("1", JSON.stringify(res));
//[{"id":"53","active":"a","value":10},{"id":"51","active":"a","value":11}]
```

# **16.比较两个对象数组，合并并更新值(假设数组 3，4 共享相同的 ID)**

**我们有时确实需要用新的属性值来合并这两个不同的值。我们可以使用 map 创建一组新的对象数组，并在更新新值之前使用 find 方法匹配特定的属性。**

**`**map()**`方法**创建一个新的数组**,其中填充了调用数组中每个元素的函数的结果。**

**`find()`方法返回满足测试函数的数组中第一个元素的值。如果没有满足测试函数的值，则返回`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`。(来源: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/) )**

***让我们创建测试数据。***

```
let array3 = [{ id: "50", active: "a", value: 12 },{ id: "51", active: "a", value: 15 }];let array4 = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 },{ id: "52", active: "a", value: 13 }];
```

***让我们创建函数。***

```
let arr = [];
array3.map(id =>
    arr.push({
        id: id.id,
        newValue: array4.find(o => o.id === id.id).value + 2
    })
);
console.log("2", JSON.stringify(arr));
//[{"id":"50","newValue":12},{"id":"51","newValue":13}]
```

# **17.比较对象数组并查找唯一的对象**

**如果我们想比较两个对象数组，并检查其中哪些是唯一的对象，我们可以使用过滤器来实现这些功能。**

***让我们创建测试数据。***

```
const array5 = [{ id: "50", active: "a", value: 12 },{ id: "51", active: "a", value: 15 }];const array6 = [{ id: "50", active: "a", value: 12 },{ id: "51", active: "a", value: 15 },{ id: "52", active: "a", value: 13 }];
```

***让我们创建函数***

```
const ids = array5.map(e => e.id);
let filtered = array6.filter(e => ids.includes(e.id));
console.log("3", JSON.stringify(filtered));
//[{"id":"50","active":"a","value":12},{"id":"51","active":"a","value":15}]
```

# **18.基于匹配值比较和更新属性**

**当我们想要比较两个对象数组并基于匹配值更新特定属性时，我们可以使用这些函数。**

***让我们创建测试数据***

```
const array7 = [{ id: "50", active: "a", value: 12 },{ id: "51", active: "a", value: 15 }];const array8 = [{ id: "50", active: "a", value: 12 }];
```

***让我们创建函数***

```
const idSet = new Set(array8.map(o => o.id));const res1 = array7.map(o => ({ ...o, value: idSet.has(o.id) ? "0" : o.value }));console.log("4", JSON.stringify(res1));
//[{"id":"50","active":"a","value":"0"},{"id":"51","active":"a","value":15}]
```

# **19.比较两个数组对象并得到它们的区别**

**当我们想要比较两个不同的对象数组并得到它们之间的差异时，我们可以使用这些函数。**

***让我们创建测试数据***

```
let a = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 }];let b = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 },{ id: "52", active: "a", value: 13 }];
```

***让我们创建函数***

```
let valuesArray1 = a.reduce(function(a, c) {
    a[c.value] = c.value;
    return a;
}, {});
let valuesArray2 = b.reduce(function(a, c) {
    a[c.value] = c.value;
    return a;
}, {});
var result = a
    .filter(function(c) {
        return !valuesArray2[c.value];
    })
    .concat(
        b.filter(function(c) {
            return !valuesArray1[c.value];
        })
    );
console.log("5", result);
//[{"id":"52","active":"a","value":13}]//shorthandlet ab = b.filter(o => !a.find(o2 => o.id === o2.id));console.log("6", ab);
```

# **20.比较两个对象数组合并并删除重复项**

**如果我们需要比较两个对象数组，删除重复的对象，合并两个数组，我们可以使用这个方法。**

***让我们创建测试数据***

```
let arr1 = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 }];let arr2 = [{ id: "50", active: "a", value: 10 },{ id: "51", active: "a", value: 11 },{ id: "52", active: "a", value: 13 }];
```

***让我们创建函数***

```
const arr1IDs = new Set(arr1.map(({ id }) => id));const combined = [...arr1, ...arr2.filter(({ id }) => !arr1IDs.has(id))];console.log(JSON.stringify(combined));
//[{"id":"50","active":"a","value":10},{"id":"51","active":"a","value":11},{"id":"52","active":"a","value":13}]
```

*   ****使用 lodash****

**Lodash 支持`_differenceBy`和 `_differenceWith`方法来找出两个数组之间的差异。**

```
let lodashtest1 = [{ id: "50" }, { id: "51" }];let lodashtest2 = [{ id: "50" }, { id: "51" }, { id: "52" }];let lodashresult = _.differenceBy(lodashtest2, lodashtest1, "id");console.log("7", JSON.stringify(lodashresult));
//[{"id":"52"}]let dif = _.differenceWith(lodashtest2, lodashtest1, _.isEqual);console.log("8",JSON.stringify(dif));
//[{"id":"52"}]
```

# **21.比较对象并找到唯一的值**

**当我们处理嵌套对象时，有时很难弄清楚如何迭代和比较两个嵌套对象并从中获得一些独特的对象。我们可以使用`Object.keys`和`Object.values`方法进行迭代。**

***让我们创建测试数据***

```
let obj1 = {val1: "test",stream: { prop1: false, prop2: true }};let obj2 = {val1: "test",stream: { prop1: true, prop2: true }};interface Data {stream: { [key: string]: boolean };}
```

***让我们创建函数:***

```
function objFilter(objA: Data, objB: Data): Data {let out: Data = { stream: {} };Object.keys(objA.stream).filter((value, idx) =>Object.values(objA.stream)[idx] === Object.values(objB.stream)[idx]? (out.stream[value] = Object.values(objA.stream)[idx]): false);return out;}console.log(JSON.stringify(objFilter(obj1, obj2))); //prop2
//{"stream":{"prop2":true}}
```

**如果你想玩 StackBlitz，你可以在这里找到:[https://stackblitz.com/edit/compare-objects-javascript](https://stackblitz.com/edit/compare-objects-javascript)**

# **22.如何在一个循环中处理多个服务调用**

****1。如果我们不想等待所有的服务呼叫结束****

```
let data = [{ id: 0 }, { id: 1 }, { id: 2 }, { id: 3 }];async function getDetails(values) {
    for (const data of values) {
        const result = await axios.get(
            `serviceURL/${data.id}`
        );
        const newData = result.data;
        this.updateDetails(newData);
        console.log(this.response);
    }
}function updateDetails(data) {
    this.response.push(data);
}getDetails(data); //call service to get data
```

****2。如果我们想等到所有的服务呼叫完成****

**我们可以使用`promise.all`来等待，直到所有的承诺都得到解决。**

**`**Promise.all()**`方法将一个可迭代的承诺作为输入，并返回一个解析为输入承诺结果数组的单个`[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)`。(来源: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) )**

```
let data = [{ id: 0 }, { id: 1 }, { id: 2 }, { id: 3 }];async function getDetails(values) {
    const dataPromises = values.map(entry => {
        return axios.get(
            `serviceURL/${entry.id}`
        );
    });const resultData = await Promise.all(dataPromises);resultData.forEach((res: any) => {
        this.updateDetails(res.data);
    });
    console.log(this.response);
}function updateDetails(data) {
    this.response.push(data);
}getDetails(data); //call service to get data
```

## **进一步阅读**

**[](https://bit.cloud/blog/sharing-javascript-utility-functions-across-projects-l557lr9k) [## 跨项目共享 JavaScript 实用函数

### 所以，你已经建立了这个令人敬畏的效用函数，并花了几个小时在上面。几个月后，你意识到你需要…

比特云](https://bit.cloud/blog/sharing-javascript-utility-functions-across-projects-l557lr9k)** 

***更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****