# 编码面试前你需要知道的 17 个 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/17-javascript-array-methods-you-need-to-know-before-your-coding-interviews-c756974453cb?source=collection_archive---------0----------------------->

## JavaScript 数组的快速备忘单

![](img/e6b68bfb3e3b3cd8a031b90eb1cf9a2e.png)

Photo By [fabio](https://unsplash.com/@fabioha)

朋友们好，

因此，最近我一直在申请软件工程职位，有人要求我参加评估，以测试我的编码能力。使用我选择的语言——如 C、C++、Java 和 JavaScript——评估要求我开发一个干净的算法来满足提示。

为了准备这样的评估，我自然倾向于 JavaScript。这是一种非常灵活和宽容的语言。

本文的重点是强调我选择用 JavaScript 进行评估的一个主要原因:原生数组方法。在这篇文章中，我将创建一个快速的备忘单来帮助你和我在未来的评估中获得高分。

> ***边注:*** *如果你正在准备编码面试，我真的很鼓励你在*[*CodeWars*](https://www.codewars.com/)*练习你的开发技巧。那里的提示很可能是我评估的一个提示。很像。*

说了这么多，我们开始吧。

*在 JavaScript 在线编译器中随意测试这些代码片段:*[*Programiz*](https://www.programiz.com/javascript/online-compiler/)*。*

## array.concat

```
let array1 = [1,2];
let array2 = [3,4];
let array3 = [5,6,7];
let array4 = array1.concat(array2, array3)
console.log(array4)// [1,2,3,4,5,6,7]
```

*   将两个或多个数组连接成一个数组。

concat 方法中可以有无限数量的参数。

还可以做:

```
let array1 = [1,2];
let array2 = [3,4];
let array3 = [5,6,7];
let array4 = [...array1, ...array2]
console.log(array4);
```

## 数组.长度

```
var name = "Kyle";
console.log(name.length) // 4var array = [1,2,3,4,5];
console.log(array.length); //5
```

*   用于获取数组或字符串的长度

## 数组.连接

```
let students = ["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"];
let welcomeMessage = "Hello " + students.join(" and ")
console.log(welcomeMessage);
/* PRINTS
Hello Anthony and Beth and Cersi and Dario and Elizabeth and Farrah
*/
```

*   将数组中的元素连接在一起，并将其转换为字符串

连接方法的一个参数(分隔符)

*   例如，我们使用“and”来连接数组中的所有元素。您可以使用空格" "或逗号" "或任何您想要的东西。

## 数组. pop

```
let students = ["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"];
let removed = students.pop();
console.log(removed); //Farrah
console.log(students); //["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth"] students.pop();
console.log(students); //["Anthony", "Beth", "Cersi" , "Dario"]
```

*   移除数组最末端的元素

方法返回被移除的元素。这是可选的。也可以只使用`students.pop()`本身。

## 数组. push

# let students = ["Anthony "，" Beth "，" Cersi "，" Dario "，" Elizabeth "，" Farrah "]；
students.push(“乔治”)；
console.log(学生)；

```
/* Prints: ["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah", "George]*/
```

*   在数组末尾添加元素

## 数组. shift

```
let students = ["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"];
students.shift();
console.log(students);/*PRINTS:
["Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"]
*/
```

*   移除数组最开头的元素

## array.unshift

```
let students = ["Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"];
students.unshift("Zander");
console.log(students);
/*PRINTS:
["Zander", "Anthony", "Beth", "Cersi" , "Dario", "Elizabeth", "Farrah"]
*/
```

## 数组.切片

```
var name = "Jennifer Aniston"
var firstName = name.slice(0,8);
console.log(firstName); //Jennifer var array = [1,2,3,4,5,6,7];
console.log(array.slice(0,3)); //[1,2,3]var array = ["Index 1", "Index 2", "Index 3", "Index 4"];
console.log(array.slice(1)); //[ 'Index 2', 'Index 3', 'Index 4' ]
```

*   返回从开始索引到结束索引的元素(加一)
*   **不改变原数组**

切片方法的一个参数

*   从给定索引**开始提取元素，直到数组**结束。

切片方法的两个参数:(开始索引，结束索引+ 1)

*   提取从给定索引(第一个参数)开始到给定索引(第二个参数)结束的元素
*   因为我们想要提取“Jennifer ”,所以我们从索引 0 开始。詹妮弗的最后一封信在索引 7 处。所以第二个参数是 8

## 阵列.拼接

```
let array1 = [1,2,3,6,7,6,7,8,9];
array1.splice(3, 6)
console.log(array1); //[ 1, 2, 3 ]
```

*   用于添加、移除或替换数组中的元素

拼接方法的两个参数

*   第一个参数是要添加、移除或替换元素的索引
*   第二个参数是要从数组**中移除的元素的数量，从第一个参数**中提到的索引开始
*   例如，我们想在第一个参数中定义的索引 3 处开始添加、删除或替换数组**中的元素。**(记住，数组使用从零开始的索引)。我们将**移除第二个参数**中定义的 6 个元素

```
let array1 = [1,2,3,6,7,6,7,8,9];
array1.splice(3, 2, 4, 5 )
console.log(array1); // [1,2,3,4,5,6,7,8,9]
```

拼接方法的三个或更多参数

*   第一个参数是要添加、移除或替换元素的索引
*   第二个参数是要从数组**中移除的元素数量，从第一个参数**中提到的索引开始
*   剩余的参数(可以无限多)将从第一个参数中提到的索引开始插入到数组**中**
*   例如，我们想要在第一个参数中定义的索引 3 处开始添加、移除或替换数组**中的元素。**(记住，数组使用从零开始的索引)。我们将**删除第二个参数中定义的 2 个元素。**这将使数组位于[1，2，3，6，7，8，9]。然后，**在第一个参数**中定义的索引 3 处，我们将插入由其余参数指定的值。在这种情况下，我们有第三和第四个参数。我们在索引 3 处插入这两个。显然，如果我们有第三个、第四个、第五个、、、、、和第二十个参数，我们会插入所有这些参数。

## 数组.反转

```
let array1 = [1,2,3,6,7,6,7,8,9];
console.log(array1.reverse()); // [ 9, 8, 7, 6, 7, 6, 3, 2, 1 ]
```

*   反转数组的顺序

## 数组.排序()

```
//ASCENDING NUMBER SORT
let array1 = [5, 1, 8, 3];
array1.sort((a, b) =>  a-b);
console.log(array1) //[ 1, 3, 5, 8 ]//DESCENDING NUMBER SORT
let array1 = [5, 1, 8, 3];
array1.sort((a, b) =>  b-a);
console.log(array1) //[ 8, 5, 3, 1 ]//DESCENDING NUMBER SORT
let array1 = [5, 1, 8, 3];
array1.sort((a, b) =>  a-b).reverse();
console.log(array1) //[ 8, 5, 3, 1 ]//ASCENDING ALPHABET SORT
let array1 = ["apples", "carrots", "zendaya", "tapioca"];
array1.sort();
console.log(array1)//DESCENDING ALPHABET SORT
let array1 = ["apples", "carrots", "zendaya", "tapioca"];
array1.sort().reverse();
console.log(array1)
```

# 字符串方法

## string.concat

```
let name = "Kyle";
let age = 21;
let city = "Los Angeles"
let sentence = name.concat(" is " , age , " years old and lives in ", city);console.log(sentence);
```

*   将两个或多个字符串连接成一个字符串。

concat 方法中可以有无限数量的参数。你也可以用`+`代替`,`来分隔每个字符串/变量

## string.indexOf

```
let sentence = "Publish today on Medium";
console.log(sentence.indexOf("today")) //8
```

*   查找字符串第一个匹配项的索引
*   如果找不到字符串，则返回-1

## string.lastIndexOf

```
let sentence = "a dog went to a dog park on a tuesday night. ";
console.log(sentence.lastIndexOf("a ")); //28
```

*   查找字符串最后一个匹配项的索引
*   如果找不到字符串，则返回-1

## 字符串分割

```
let name = "Kyle DeGuzman";
let nameArray = name.split(" ");
console.log(nameArray) //['Kyle', 'DeGuzman']let alphabet = "abcdefghijklmnopqrstuv";
let alphabetArray = alphabet.split("");
console.log(alphabetArray) //['a','b','c','d','e','f','g','h'....]let favoriteThings = "Raindrops on Roses, Whiskers on Kittens, Bright Copper Kettles, Warm Woolen Mittens, Brown Paper Packages Tied Up With String";
let favoriteThingsArray = favoriteThings.split(",");
console.log(favoriteThingsArray) 
```

*   将字符串转换为数组

分割方法的一个参数(分隔符)

*   分隔符定义了切割字符串的位置
*   例如，第一次分割会在空间处进行切割。因此，结果在每个空间被分割。
*   例如，第二次拆分在""处进行切割，基本上是在每个字符之间。
*   例如，只要有逗号，第三次拆分就会产生一个剪切。

## string.toLowerCase()

```
let name = "kYle";
let name = name.toLowerCase(); 
console.log(name); //kylelet string = ("triumph").toLowerCase(); 
console.log(string); //triumph
```

*   将字符串中的所有字母转换为小写

如果您正在测试用户输入的字符串，这将非常有用。

例如:

```
if (input == "apple"){
...
}
```

因此，如果用户输入 aPple、appLE、Apple 等等，它们将是无效的。

```
if (input.toLowerCase() == "apple"){
}
```

*   这是一个更好的方法

## string.toUpperCase()

```
let name = "kYle";
let name = name.toUpperCase(); 
console.log(name); //KYLElet string = ("triumph").toUpperCase(); 
console.log(string); //TRIUMPH
```

*   将字符串中的所有字母转换为大写

## 字符串.修剪

```
let firstName = "Kyle\n\n\n\n";
let lastName = "Deguzman      ";
console.log(firstName + lastName);
console.log(firstName.trim() + lastName)
```

*   从字符串的左侧和右侧删除空白

我们的备忘单到此结束。如果您有任何要补充的信息，请在评论中分享。

感谢您的阅读:)

# 如果您想要更多的阅读材料，请查看:

[学习如何计算算法的时间复杂度](https://medium.com/@kyledeguzmanx/give-me-5-minutes-and-ill-teach-you-how-to-find-the-time-complexity-of-an-algorithm-23be4d4179ee)

[如何使用数组方法:映射、约简和过滤(初学者)](/how-to-use-array-methods-map-reduce-and-filter-for-beginners-565ee4663f29)

[关于 JavaScript 数组你需要知道的 7 个小窍门](https://medium.com/@kyledeguzmanx/7-tricks-you-need-to-know-about-javascript-arrays-5712a37b1d86)

*多内容于* [***浅显。io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区纠纷***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。*