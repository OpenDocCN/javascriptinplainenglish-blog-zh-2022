# 用 JavaScript 创建和生成 UUIDs

> 原文：<https://javascript.plainenglish.io/create-and-generate-uuids-with-javascript-dbd7494c81ed?source=collection_archive---------7----------------------->

## 通用唯一标识符是引用 JavaScript 中各种对象和元素的一种简单方法。让我们看看如何制作它们。

![](img/b322b0a900cf616218cd5e412d7efb11.png)

通用唯一标识符(UUIDs)在软件开发中无处不在，从识别对象元素到网页上的 DOM 元素。它们是唯一的 128 位标识符，由 36 个字符组成，格式为`8-4-4-4-12`——例如`f81e7af3-fcf4-4cdd-b3a3-14a8087aa191`。UUIDs 通常不依赖于注册表或数据库来确保唯一性。UUID 是复制品的可能性不是零，但这种可能性如此之小，以至于大多数人都忽略了这种风险。

在 Javascript 中，有许多方法可以创建 UUIDs。记住这一点，让我们看看如何用 Javascript 创建 UUIDs。

# 选项 1:使用 crypto.randomUUID()方法

`crypto.randomUUID`是一种用原生 Javascript 制作 UUIDs 的相对较新且可靠的方法。所有现代的常青树浏览器都支持它，它可以用一行代码生成一个 UUID。浏览器上的全局`this`对象提供了`crypto`方法——也称为`window`。它也可以在节点上使用。射流研究…

因此，您现在可以在浏览器中生成 UUIDs，如下所示:

```
console.log(this.crypto.randomUUID()); // f81e7af3-fcf4-4cdd-b3a3-14a8087aa191
```

或者，在节点中。来自版本`19.0`的 JS 是这样的:

```
import crypto from 'crypto'
console.log(crypto.randomUUID()); // f81e7af3-fcf4-4cdd-b3a3-14a8087aa191
```

# 选项 2:使用 UUID 软件包

NPM 上有一个非常流行的包叫做`uuid`，它为你做了所有繁重的工作并生成了可靠的 UUIDs。它可以在节点中使用。首先安装 JS 项目，然后在您的代码中运行它。

首先，使用`npm`安装:

```
npm i uuid
```

然后你只需要像这样导入并在你的代码中使用它:

```
import { v4 as uuid } from 'uuid';
let myUUID = uuid(); // Returns a random UUID xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

`uuid`包是在 Node.JS 中创建 UUIDs 的可靠方法。

# 选项 3:使用 crypto.getRandomValues()方法

使用`crypto.getRandomValues()`可以生成您自己的`uuid`函数。这在处理 Node 的情况下很有用。`19.0`之前的 JS 版本，还是得支持老浏览器。`crypto.getRandomValues()`早在 Chrome 11 就支持了。

```
function uuid() {
    return ('10000000-1000-4000-8000-100000000000').replace(/[018]/g, c => (
        c ^ (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))).toString(16)
    );
}
```

这个函数基于[这里的工作](https://gist.github.com/jed/982883)——如果你需要自己的函数来生成可靠的 UUIDs，它会生成可靠的 UUIDs。

# 选项 4: Math.random()(不推荐)

最后一招，也是最糟糕的解决方案是使用`Math.random()`，然而这通常不是一个好主意，因为`Math.random()`在生成 UUIDs 以确保唯一性方面做得不够好。你应该也不需要这个，因为我们现在已经有了广泛可用的`crypto.randomUUID()`方法。

如果您想要一个真正的 UUID，最好避免这种解决方案，但是它可以为您需要一个 UUID fast 进行测试的项目提供一个快速解决方案。当您没有`randomUUID()`支持或`uuid`软件包可用时，这可以作为一种备用方案:

```
function uuid() {
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
    return v.toString(16);
  });
}
```

# 结论

这大概涵盖了用 JavaScript 制作 UUIDs 的所有不同方法。希望你喜欢这个指南— [点击这里](https://fjolt.com/category/javascript)查看更多关于 JavaScript 的内容。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***