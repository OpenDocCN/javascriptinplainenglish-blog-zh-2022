# 如何解决 Jest 中的 replaceAll 错误

> 原文：<https://javascript.plainenglish.io/how-to-solve-the-replaceall-error-in-jest-815dc296c34b?source=collection_archive---------9----------------------->

![](img/066d70ebac512035fcbbcd3857678f90.png)

Photo by [David Pupaza](https://unsplash.com/@dav420?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 不要忘记保持所有项目配置的同步。

有一次我在一个遗留的 React 项目上工作，我运行了一个最近添加的单元测试，我得到了这个错误:

**问题**

*Jest: TypeError: replaceAll 不是函数*

一开始我很困惑，因为在浏览器中，该组件使用 [replaceAll](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replaceAll) 方法工作得非常好，但结果是 *replaceAll 是一个新功能，并不是在所有浏览器或旧版本的 Node.js 中都实现了。*

**解决方案**

安装 replaceAll polyfill 并将其添加到 jest 设置配置文件中。

1.  安装 replaceAll

```
npm i string.prototype.replaceall
```

2.修改您的 Jest 配置，添加一个 *setupFilesAfterEnv* 属性，如下所示:

```
{ "jest": { "setupFilesAfterEnv": ["<rootDir>/jestSetup.js"] }}
```

3.将以下代码添加到您的 *jestSetup* 文件中

```
import replaceAllInserter from 'string.prototype.replaceall'; replaceAllInserter.shim();
```

编码快乐！

[来源](https://stackoverflow.com/questions/65295584/jest-typeerror-replaceall-is-not-a-function/67877325#67877325)

嗨，[在这里](https://davidjsmoreno.dev/)我们谈论软件开发、JavaScript、自学教育和其他东西。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。***