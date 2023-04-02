# 如何在 JavaScript 中用分隔符连接字符串

> 原文：<https://javascript.plainenglish.io/javascript-concatenate-strings-with-separator-b2aa5f784d9a?source=collection_archive---------11----------------------->

![](img/1c750ede4b8fe4696debd13a3ce51de1.png)

在本文中，我们将学习如何在 JavaScript 中用我们选择的分隔符连接一串字符串，比如逗号或连字符。

# 数组 join()方法

要用分隔符连接字符串，我们可以创建一个包含字符串的数组，并调用`join()`方法，将分隔符作为参数传递。`join()`方法将返回一个包含用分隔符连接的数组元素的字符串。例如:

```
const str1 = 'html';
const str2 = 'css';
const str3 = 'javascript';const spaceSeparated = [str1, str2, str3].join(' ');
console.log(spaceSeparated); // html css javascriptconst commaSeparated = [str1, str2, str3].join(',');
console.log(commaSeparated); // html,css,javascript
```

# 多字符分隔符

分隔符不一定是单个字符，我们可以传递包含多个字符的字符串，比如单词:

```
const str1 = 'html';
const str2 = 'css';
const str3 = 'javascript';const andSeparated = [str1, str2, str3].join(' and ');
console.log(andSeparated); // html and css and javascript
```

**注意:**如果我们在没有传递参数的情况下调用字符串数组上的`join()`方法，字符串将用逗号分隔:

```
const str1 = 'html';
const str2 = 'css';
const str3 = 'javascript';const withoutSeparator = [str1, str2, str3].join();
console.log(withoutSeparator); // html,css,javascript
```

虽然这样做可行，但如果需要逗号分隔，最好通过将逗号作为参数传递来明确这一点，因为不是每个人都知道默认行为。

**注意:**`join()`方法将返回一个空字符串，如果我们在一个空数组上调用它。例如:

```
console.log([].join(',')); // ''
```

**注意:**元素如`undefined`、`null`或空数组值在连接过程中被转换为空字符串:

```
const joined = [null, 'html', undefined, 'css', []].join();
console.log(joined); // ,html,,css,
```

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/javascript-concatenate-strings-with-separator/)

每周获取新的 web 开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)