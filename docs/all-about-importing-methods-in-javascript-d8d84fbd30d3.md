# 关于在 JavaScript 中导入方法的所有内容

> 原文：<https://javascript.plainenglish.io/all-about-importing-methods-in-javascript-d8d84fbd30d3?source=collection_archive---------7----------------------->

## 知道在什么情况下使用什么语法。

![](img/3cc0bc28ef37f53fa32e7877d91c0c5a.png)

Photo by [Sudharshan TK](https://unsplash.com/@shantk18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

所以我们都见过 JavaScript 中导入方法的各种方式。您可以按名称、名称*或别名导入它们。

```
import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
var promise = import("module-name");
```

希望在阅读完本文后，您会对在什么场景中如何使用什么语法有更好的了解。

在我们看这些之前，让我们试着理解默认导入和命名导入之间的区别。

![](img/721d47fea4579e85d15889f3e5c6d53b.png)

## **默认导入和名字导入有什么区别？**

***默认导入语法*** —我们导入模块中的所有方法，并存储在名为`defaultExport`的变量中。这基本上是导入模块的默认导出。

```
import defaultExport from "module-name";
```

***Named Imports 语法*** —我们析构模块，只导入我们需要的符号/方法。这将只导入命名的方法，而不是所有的方法。

```
import { method1 } from "module-name";
import { method1, method2 } from "module-name";
```

## **使用*** 导入整个模块

你也可以使用*导入整个模块，就像一个命名空间。

```
import * as name from "module-name";
```

现在，如果 module-name 有一个名为`myCustomMethod()`的方法，您可以这样调用它:

```
name.myCustomMethod();
```

## **从模块导入命名方法**

您也可以从模块中仅导入特定的方法，如下所示:

```
import {myExport} from '/modules/my-module.js';import {method1, method2} from '/modules/my-module.js';
```

您也可以在导入时使用别名，将方法名称更改为更方便使用的名称。

```
import {reallyReallyLongModuleExportName as shortName}
  from '/modules/my-module.js';import {
  reallyReallyLongModuleExportName as shortName,
  anotherLongModuleName as short
} from '/modules/my-module.js';
```

## **只为副作用导入一个模块**

您也可以仅导入整个模块的副作用，而不导入任何内容。这会运行模块的全局代码，但实际上不会导入任何值。

```
import '/modules/my-module.js';
```

这也适用于动态导入，如下所示:

```
(async () => {
  if (condition) {
    // import module for side effects
    await import('/modules/my-module.js');
  }
})();
```

要了解更多关于动态导入的信息，请查看:

[](/require-vs-import-in-js-82a7a47671f) [## 比较 JavaScript 中的 require()和 import()

### 探索 JavaScript 中 require()和 import()方法的特性。

javascript.plainenglish.io](/require-vs-import-in-js-82a7a47671f) 

## **默认导入一个模块**

如上所述，您也可以很容易地使用默认导出来导入模块。

```
import defaultExport from "module-name";
```

您也可以将它与上面的任何符号混合使用。

```
import defaultExport, * as myModule from '/modules/my-module.js';
import defaultExport, {method1, method2} from '/modules/my-module.js';
```

![](img/ac7beafc7ee912d7cde1ca4fed100ff5.png)

如果您选择使用**动态导入**，您仍然可以使用默认导出和命名导出的组合，但是它的工作方式有点不同。您需要从返回的对象中析构并重命名“default”键。

```
(async () => {
  if (condition) {
    const { default: defaultExport, method1, method2 } = await import('/modules/my-module.js');
  }
})();
```

## 最佳实践是什么？

现在是整篇文章中最重要的部分。您应该使用什么符号，最佳实践是什么？

我已经浏览了很多社区帖子和最佳实践文档，简而言之，没有直接的答案。这完全取决于你的使用。

这对于您的团队和社区来说更容易管理，也更容易进行代码审查。两者各有利弊。例如，Angular 主要使用命名导入，而 React 既有命名导入，也有默认导入，并且都有自己的用例。

我个人更喜欢使用默认导出和命名导出的组合。

```
import CustomModule, {method1, method2} from '/modules/CustomModule.js';
```

这里唯一需要注意的是组件文件必须和组件同名。该组件导出为 `*default*` *。*

你也可以在这里阅读一些其他有趣的文章:

[](/let-vs-var-what-is-the-actual-difference-5acdb1f1c83) [## let' vs 'var ':实际区别是什么？

### 这里有一个关于 JavaScript 中 let 和 var 之间的区别的快速阅读，可能会派上用场。很高兴…

javascript.plainenglish.io](/let-vs-var-what-is-the-actual-difference-5acdb1f1c83) [](/code-splitting-in-react-all-you-need-to-know-392b0dfeb1fa) [## React 中的代码拆分—您需要知道的一切

### React 中对代码拆分的深入探讨。

javascript.plainenglish.io](/code-splitting-in-react-all-you-need-to-know-392b0dfeb1fa) 

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*