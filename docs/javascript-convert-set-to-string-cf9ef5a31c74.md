# 如何在 JavaScript 中将集合转换成字符串

> 原文：<https://javascript.plainenglish.io/javascript-convert-set-to-string-cf9ef5a31c74?source=collection_archive---------14----------------------->

## JavaScript 中把集合转换成字符串的指南。

![](img/2d2b2211688a55151553865e4647e7dd.png)

要在 JavaScript 中将集合转换成字符串，调用带有参数`Set`的`Array.from()`方法，然后在结果数组上调用`join()`方法。例如:

```
const set = new Set(['x', 'y', 'z']);const str1 = Array.from(set).join(' ');
console.log(str1); // x y zconst str2 = Array.from(set).join(',');
console.log(str2); // x,y,z
```

`Array.from()`方法将类似于`Set`的数组对象转换成数组:

```
const set = new Set(['x', 'y', 'z']);console.log(Array.from(set)); // [ 'x', 'y', 'z' ]
```

转换完成后，我们可以在数组上调用`join()`方法。`join()`返回一个字符串，该字符串包含用指定分隔符连接的数组元素:

```
console.log(['x', 'y', 'z'].join('-')); // x-y-zconsole.log(['x', 'y', 'z'].join('/')); // x/y/z
```

**注意:**我们也可以使用 spread 语法(`...`)将`Set`转换成数组:

```
const set = new Set(['x', 'y', 'z']);const str1 = [...set].join(' ');
console.log(str1); // x y zconst str2 = [...set].join(',');
console.log(str2); // x,y,z
```

spread 语法将`Set`的值解包到一个新数组中，我们调用这个新数组`join()`来获取字符串。

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/javascript-convert-set-to-string/)

每周获取新的 web 开发技巧和教程。

![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)

[**订阅**](https://codingbeautydev.com/newsletter)