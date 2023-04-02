# JavaScript 数组连接方法

> 原文：<https://javascript.plainenglish.io/javascript-array-concat-method-47d0c24df544?source=collection_archive---------12----------------------->

## concat()方法用于返回合并数组的浅层副本。浅层副本包含与原始数组切片相同的引用。

![](img/c3f4beaf81f931d73589e0f6775c0c22.png)

数组上的`concat`方法用于获取两个数组并将它们连接成一个。它接受任意数量的数组，因此您可以一次连接多个数组:

```
Array.concat(value1, value2, value3, ...valueN)
```

添加到`concat`方法中的每一项必须是数组类型。让我们看一个简单的例子。下面，我们结合两个数组:

```
let myArray = [ 1, 2, 3, 4, 5 ];
let newArray = [ 'n', 'a', 'e', 'k' ] 
let mergedArray = myArray.concat(newArray);
console.log(mergedArray); // [ 1, 2, 3, 4, 5, 'n', 'a', 'e', 'k' ]
```

`concat`不删除重复——但是如果你对一个可以删除重复的数据结构感兴趣的话，[你可能想看看我的 Javascript 集合指南](https://fjolt.com/article/javascript-sets)。

`concat`方法创建了它所应用的数组的浅层副本，并在末尾添加了其他数组。[你可以在这里](https://fjolt.com/article/javascript-shallow-copies)了解更多关于浅拷贝的知识。

这意味着尽管看起来创建了一个新数组，但它仍然与您修改的原始数组有联系。事实上，你在`concat`中提到的每一个数组都是原始数组的肤浅拷贝。考虑下面的例子:

```
let myArray = [ { name: "John" }, 1, 2, 3, 4, 5 ];
let newArray = [ { name: "Jacob" }, 'a', 'e', 'k' ] 
let mergedArray = myArray.concat(newArray);
myArray[0].name = "Jingleheimer";
newArray[0].name = "Schmidt";
newArray[1] = 5;
console.log(mergedArray, myArray); // [ { name: "Jingleheimer" }, 1, 2, 3, 4, 5, { name: "JSchmidtacob" }, 'a', 'e', 'k' ]
```

你可能认为改变`myArray`和`newArray`上的`name`不会影响`mergedArray` -但它会。但是`newArray[1] = 5`对`mergedArray`没有影响。

你可以在这里了解[为什么这样工作的细节](https://dev.to/smpnjn/(https://fjolt.com/article/javascript-shallow-copies))，但是基本前提是我们在`concat`中使用的数组在内存中保持与原始数组相同的引用。更新`name`会更新`mergedArray`和原始数组，因为它们都存储在同一个位置。然而，输入`newArray[1]`告诉 Javascript 在`mergedArray`的位置`[1]`放置一个全新的值。

当您遇到奇怪的 Javascript 数组错误时，记住这一点很重要。

# 串联多个数组

我们已经了解了如何连接两个数组，但是连接更多的数组也是同样的方式。您在`concat`函数中列出了所有的数组，如下所示:

```
let myArray = [ 1, 2, 3, 4, 5 ];
let newArray = [ 'n', 'a', 'e', 'k' ] 
let anotherArray = [ 7, 1, 5, 7 ] 
let mergedArray = myArray.concat(newArray, anotherArray);
console.log(mergedArray); // [ 1, 2, 3, 4, 5, 'n', 'a', 'e', 'k', 7, 1, 5, 7 ]
```

这些数组按照它们被提及的顺序进行合并。

# 串联嵌套数组

嵌套数组以同样的方式连接在一起。外部数组被移除，这意味着嵌套元素成为第一个数组的一部分:

```
let myArray = [ [1, [2, 3], 4], 5 ];
let newArray = [ ['n', 'a'], 'e', 'k' ] 
let mergedArray = myArray.concat(newArray);
console.log(mergedArray); // [ [1, [2, 3], 4], 57, ['n', 'a'], 'e', 'k' ]
```

# 串联数组中的值

如果你给`concat`传递一个简单的值，它会把它当作一个数组元素。这意味着如果你传入的是`'value'`而不是`['value']`，它无论如何都会强制它传入`['value']`:

```
let myArray = [ 1, 2, 3, 4, 5 ];
let mergedArray = myArray.concat(1, 2, 3);
console.log(mergedArray); // [ 1, 2, 3, 4, 5, 1, 2, 3 ]
```

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*