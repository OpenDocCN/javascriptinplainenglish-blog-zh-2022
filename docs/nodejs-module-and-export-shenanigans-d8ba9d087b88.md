# Node.js 模块和导出诡计

> 原文：<https://javascript.plainenglish.io/nodejs-module-and-export-shenanigans-d8ba9d087b88?source=collection_archive---------4----------------------->

**琐事:**假设我们有一个包含以下内容的`test.js`文件:

```
console.log(arguments);
```

输出会是什么？

![](img/beeb04807eb4a5b12e4e43130fcee457.png)

image_credit — NodeJS — The Complete Guide (incl. MVC, REST APIs, GraphQL)

输出将是这样的:

```
[Arguments] {
  '0': {},
  '1': [Function: require] {
    resolve: [Function: resolve] { paths: [Function: paths] },
    main: Module {
      id: '.',
      path: '/Users/ayesha/nodejs',
      exports: {},
      filename: '/Users/ayesha/nodejs/test-module.js',
      loaded: false,
      children: [],
      paths: [Array]
    },
    extensions: [Object: null prototype] {
      '.js': [Function (anonymous)],
      '.json': [Function (anonymous)],
      '.node': [Function (anonymous)]
    },
    cache: [Object: null prototype] {
      '/Users/ayesha/modejs/test-module.js': [Module]
    }
  },
  '2': Module {
    id: '.',
    path: '/Users/ayesha/nodejs',
    exports: {},
    filename: '/Users/ayesha/nodejs/test-module.js',
    loaded: false,
    children: [],
    paths: [
      '/Users/ayesha/nodejs/node_modules',
      '/Users/ayesha/node_modules',
      '/Users/node_modules',
      '/node_modules'
    ]
  },
  '3': '/Users/ayesha/nodejs/test-module.js',
  '4': '/Users/ayesha/nodejs'
}
```

所以基本上，当 Node.js 执行一个文件时，它把它放在一个函数中。这些是 Node.js 发送给这个函数的参数。所以，上面的文件被解释为:

```
//function (exports, module, require, __filename, __dirname) {console.log(arguments);// return module.exports//}
```

注释掉的行是节点在执行前添加的行。并且它还返回`module.exports`对象。

所以，当我们写`exports.somevariable = 5`时，我们使用的是 Node 传递给函数的参数。返回也是自动的，我们不需要显式地返回任何东西，Node 会为我们做的。

这就是为什么我们要添加 API 或变量来暴露给`module.exports`对象。事实上，参数`exports`是`module.exports`的别名。我们可以通过`exports`或`module.exports`公开变量或 API，因为`module`也作为参数发送给我们。然而，需要注意的是——我们不能做类似于`export = () => {}`的事情，因为我们在这里没有给一个对象赋值——我们实质上破坏了模块和导出之间的赋值引用。但是我们被允许这样做`module.exports = () => {}`，因为 Node 将返回`module.exports`并且我们可以改变我们返回的内容。

类似地，当我们使用`require()`时，也是在使用`require`参数。

Node 对它执行的每个文件都这样做。

# 导出— 4 种方式

## 简单对象导出:

所以现在，在我们的`test.js`文件中——如果我们想要暴露一些变量，我们可以这样做——

```
exports.val1 = 20;
exports.val2 = 'test';
```

如果我们有另一个文件——

```
const testApi = require('./test');
console.log(testApi.val1, testApi.val2);
//20 'test'
```

对于这样的简单导出——我们不需要使用`module.exports`,我们可以使用`exports`,如上例所示。当我们想要使用这些来自`test.js`的公开值时，我们简单地导入它们，并得到一个简单的对象作为回报。

## 数组导出:

当顶层 API 是数组时，我们可以直接赋给`module.exports`。例如，我们称之为`test2.js`:

```
module.exports = [23,33,55];
```

现在，当我们导入这个类时，我们直接得到整个数组。

```
const arrayImport = require('./test2.js');
console.log(arrayImport)
//[ 23, 33, 55 ]
```

## 字符串导出:

这是完全不言自明的。当我们想导出一个字符串时，我们也直接将它赋给`module.exports`

## 函数导出:

这种出口非常有用。当我们的顶级 API 是一个函数时，我们使用它。例如，考虑下面的代码`test3.js`:

```
module.exports = (param1, param2) => `${param1} + ${param2} = ${param1+param2}`;
```

现在我们这样使用这个函数:

```
const sum = require('./test3.js');
console.log(sum(13, 10));
//13 + 10 = 23
```

希望这对理解 Node.js 中的模块和导出有所帮助。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*