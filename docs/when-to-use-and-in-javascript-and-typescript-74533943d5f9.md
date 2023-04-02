# 什么时候使用？?'以及 JavaScript 和 TypeScript 中的' || '

> 原文：<https://javascript.plainenglish.io/when-to-use-and-in-javascript-and-typescript-74533943d5f9?source=collection_archive---------16----------------------->

## 何时使用的简短指南？?'在 JavaScript 和 TypeScript 代码中检查值时使用“||”

![](img/3c554f788579007db5c69a9e519ca6be.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇短文中，我想分享一个简单的方法来记住在 JavaScript 和 TypeScript 代码中检查值时何时使用`??`和`||`。

# 检查一个值时什么时候使用`??`？

`??`是一个“或”运算符，在返回右侧之前，左侧必须为空。

问号`?`就像问自己，“价值存在吗？”

```
var ?? varMustBeEmptyToReturnThisVar
```

## 例子

假设你得到一个对象，它的一些属性是可选的。

```
const obj0 = { required: 0 };
const { optional } = obj0;
console.log(optional ?? 'no optional property exists');
// returns 'no optional property exists'
```

当属性返回一个 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 值时要小心。

```
const obj1 = { required: '' };
const { required } = obj1;
console.log(required ?? 'no required property exists');
// returns ''
```

# 检查数值时何时使用`||`？

`||`是一个“或”运算符，在返回右侧之前，左侧必须为[false](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)。

竖线`|`就像竖起一道屏障，只有[真值](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)能留在左边。

```
var || varMustBeFalsyToReturnThisVar
```

## 例子

假设你得到一个对象，它的一些属性是假的。

```
const obj2 = { required: '' };
const { required } = obj2;
console.log(required || 'required property is falsy');
// returns 'required property is falsy'
```

# 结论

我有时会误用`??`和`||`，并认为我应该给自己写这个提醒。希望这对你也有帮助。

# 在你走之前

这些是你可能喜欢的其他文章:

[](https://betterprogramming.pub/stop-installing-node-js-and-global-npm-packages-use-docker-instead-42597990db13) [## 停止安装 Node.js 和全局 Npm 包，改用 Docker

### 保护您的系统免受漏洞攻击

better 编程. pub](https://betterprogramming.pub/stop-installing-node-js-and-global-npm-packages-use-docker-instead-42597990db13) [](https://medium.com/geekculture/five-scary-linux-commands-you-should-not-run-4222773188bb) [## 你不应该运行的五个可怕的 Linux 命令。

### 你可能想知道这些命令是如何工作的。

medium.com](https://medium.com/geekculture/five-scary-linux-commands-you-should-not-run-4222773188bb) [](https://betterprogramming.pub/how-to-remove-sensitive-data-and-plaintext-secrets-from-github-ca8ca0b7675a) [## 如何从 GitHub 中删除敏感数据和明文秘密

### 保持你的存储库干净，以避免被黑客攻击

better 编程. pub](https://betterprogramming.pub/how-to-remove-sensitive-data-and-plaintext-secrets-from-github-ca8ca0b7675a) [](/postman-secrets-cookies-cryptojs-4051db70e8c2) [## 如何使用 CryptoJS 和 Cookies 在 Postman 中处理秘密

### 在我之前的文章中，我们探讨了如何在 Postman 中使用 cookies 来存储您的秘密。取决于您的安全性…

javascript.plainenglish.io](/postman-secrets-cookies-cryptojs-4051db70e8c2) 

*原载于* [*dev.to*](https://dev.to/miguelacallesmba/when-to-use-and-in-javascript-and-typescript-pfh)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***