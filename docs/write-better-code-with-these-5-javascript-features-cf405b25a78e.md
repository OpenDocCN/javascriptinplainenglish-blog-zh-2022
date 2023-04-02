# 利用这 5 个 JavaScript 特性编写更好的代码

> 原文：<https://javascript.plainenglish.io/write-better-code-with-these-5-javascript-features-cf405b25a78e?source=collection_archive---------6----------------------->

## 在运算符、三元和可选链接中使用零化合并

![](img/e27da529bf488b97938b9a99c3b0ccb3.png)

JavaScript 是有史以来最流行的计算机语言之一，原因之一是 JavaScript 的语法非常直观。这还不是最好的部分，最好的部分是大量的新特性被定期添加到语言中。

今天，我们将看到一些新特性帮助我们编写更直观的代码。

# 零化合并算子(？？)

零化合并算子(？？)是逻辑运算符，当其左侧操作数为`null`或`undefined`时，返回其右侧操作数，否则返回其左侧操作数。

```
false || '@sun_anshuman' // returns '@sun_anshuman'

false ?? '@sun_anshuman' // returns false

0 || '@sun_anshuman' // returns '@sun_anshuman'

null || '@sun_anshuman' // returns '@sun_anshuman'

null ?? '@sun_anshuman' // returns '@sun_anshuman'

undefined ?? '@sun_anshuman' // returns '@sun_anshuman'
```

`||`的问题在于它是一个布尔运算符，所以在求值之前，它会将左边的操作数强制转换为布尔，从而使 0 和“”都成为`false`。

# 用例示例

让我们假设你正在构建一个最低分数为 0 的游戏，你认为-1 是一个无效分数。

因此，在您更新用户的分数之前，您需要确保它被设置为有效值或定义的无效分数。

```
// the server returns 0
let score = fetchScoreFromServer(); 

// we only want the score to be -1 only if the score
// is undefined or null because 0 is a valid value

const finalScore = score || -1; 
// but this will give us the invalid value even if,
// the first operand (0) is a valid value, leading to a bug
```

你问，这怎么解决？*(我知道你现在已经知道了，哈哈)*

```
let score = fetchScoreFromServer(); // returns 0 again

const finalScore = score ?? -1;
// finalScore stays score (0 in this case), 
// unless the server returned null or undefined
```

# 逻辑零赋值(？？=)

逻辑零赋值(x？？= y)运算符仅在 x 为空时赋值(`null`或`undefined`)。

```
let user = { name: "anshuman_bhardwaj" };
user.twitter_name ??= "@sun_anshuman"; // assigns '@sun_anshuman'
console.log(user); // {name: "anshuman_bhardwaj", twitter_name: "@sun_anshuman"}
```

这基本上是一个基于`??`操作符的赋值操作。

# 用例示例

```
// the above example can be rewritten like this
let finalScore = fetchScoreFromServer(); // returns 0 again

finalScore ??= -1;
// keeps value of 0
```

另一个使用`??`的好地方是引用对象属性和使用默认值。在这种情况下，我们可以使用逻辑空赋值`??=`为`undefined`属性赋予默认值。

```
const user = { email: 'anshuman_bhardwaj@dev.to', company: '' }

// assign user.name to email username if it's undefined
user.name ??= email.split("@")[0]

// make company Canoo if company not available on user
user.company ??= 'Canoo'
// this time company stays empty string
```

# in 运算符

如果指定的属性位于指定的对象或其原型链中，则 in 运算符返回 true。

```
const user = { email: 'anshuman@gmail.com' } 

'email' in user // return true

'name' in user // return false
```

您还记得使用`undefined`值的时候，因为引用的键在 Object 中丢失了。

值得注意的是，

> *如果您将一个属性设置为未定义，但没有删除它，则 in 运算符将为该属性返回 true。*

# 用例示例

一个很好的用例是在对对象的属性运行操作之前运行健全性检查，以避免进行未定义的检查和错误。

```
// we have an user object
let user = { email: "anshuman_bhardwaj@dev.to" };

// now we want to assign it a name if its not available

// checks if user has email
if ("email" in user) {
  // checks if user has name
  if (!("name" in user)) {
    user["name"] = user.email.split("@")[0];
  } else {
   console.log("Welcome user: " + user.name);
  }
} else {
  console.error("User does not have required property: email");
}
```

在数组上使用 in 检查给定的索引是否为空槽

```
const emptyList = new Array(5)

empties[2]    // returns undefined
2 in empties  // returns false

empties[2] = 'anshuman_bhardwaj'
2 in empties  // returns true
```

# 可选链接(？。)

`?.`操作符类似于。链接运算符，不同之处在于，如果引用为(null 或 undefined ),表达式将短路，返回值为 undefined，而不是导致错误。

```
let user = { name: 'anshuman' }

user.address.zipcode // TypeError

user.addess?.zipcode // returns undefined
```

值得注意的是，

1.  当用于函数调用时，如果给定的函数不存在，则返回 undefined。
2.  可选链接不能用于未声明的根对象，但可以用于未定义的根对象。

# 通过示例使用案例

```
// user can be null or an Object containing email
const user = getUserFromDev() 

// if we do this it will run fine when user is an Object 
// but when user is null this will give a TypeError
console.log(user.email)

// we can fix this by using optional chaining

console.log(user?.email)
// logs the actual user email when user is an Object
// logs undefined if user is null but doesn't crash
```

# 条件三元运算符(？)

三元运算符检查指定的条件是否为真，如果为真则返回第一个表达式，否则返回第二个表达式。

`x ? y : z`，表示如果 x 为真则返回 y，否则返回 z。

```
let user = { age: 22 }

user['status'] = user.age > 18 ? 'adult' : 'minor'
// user.status is 'adult'
```

这个操作符不是 JavaScript 特有的，我第一次在 C++中使用它。

# 用例示例

```
let user = { email: "anshuman_bhardwaj@dev.to" };

// lets consider this code, simple enough?
if ("email" in user) {
  user["name"] = user.email.split("@")[0];
} else {
  user["name"] = "Anonymous";
}

// we can make it even simpler by using ternary
user["name"] = "email" in user ? user.email.split("@")[0] : "Anonymous";
```

> *使用三元是个人偏好，它适合做行内表达式，否则一切都可以放在 if-else*

# 奖金

这里有一些混合搭配上述特征的例子，让我们看看谁能在评论中回答正确。

```
// consider the examples independent of each other

const user = { email: 'anshuman_b@dev.to', lastName: undefined }

// 1
user["firstName"] = "email" in user 
                            ? user.email.split("_")[0] 
                            : "Anonymous";

// 2
user["familyName"] ??= 'Bhardwaj'

// 3
console.log('lastName' in user)

// 4 
console.log('' ?? '@sun_anshuman')
```

# 了解更多信息

你也可以看这个 [YouTube 视频](https://youtu.be/pk50LBGru_Q)，在那里我解释了这些例子。

Write better JavaScript code

你也可以派生出 [CodeSandBox](https://codesandbox.io/s/operators-by-anshuman-51q7y?file=/src/index.js) 来测试例子。

我希望这篇文章对你有帮助。如果您有任何反馈或问题，请随时在下面的评论中提出。我很想听听他们的想法并为之努力。

更多此类内容，请关注我

*   [推特](https://twitter.com/sun_anshuman)
*   [YouTube](https://www.youtube.com/AnshumanBhardwaj)
*   [中等](https://anshuman-bhardwaj.medium.com/)

> *直到下一次*

![](img/31573030d1a65a61fbd5e375cc6c1f55.png)

# 资源

[MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators)

*原载于 2022 年 1 月 17 日*[*https://theanshuman . dev*](https://theanshuman.dev/articles/write-better-code-with-these-5-javascript-features-22km)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区【不和谐】***](https://discord.gg/GtDtUAvyhW) *获取独家写作机会和建议。*