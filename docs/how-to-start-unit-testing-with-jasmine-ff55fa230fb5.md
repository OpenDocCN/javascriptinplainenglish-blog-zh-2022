# 如何用 Jasmine 开始单元测试

> 原文：<https://javascript.plainenglish.io/how-to-start-unit-testing-with-jasmine-ff55fa230fb5?source=collection_archive---------10----------------------->

## 用 Jasmine 运行单元测试的初学者指南。

![](img/9e6295283cd2c5b9954f587af2ff02e2.png)

Illustration by the author

在我的[上一篇文章](https://how-to.dev/the-simplest-case-for-unit-tests-pure-functions)中，我展示了单元测试*纯函数*的伪代码示例。作为对那篇文章的回应，我得到了一个很好的问题——那么我如何开始测试我的代码呢？让我们更实际地看看同一个简单的测试案例。

# 获取代码库

我用示例代码准备了一个[库](https://github.com/how-to-js/how-to-unit-test)。主要内容是`pure-functions.js`:

```
export function greet(name, surname) {
  return `Hello ${name} ${surname}!`;
}

export function calculateDiscountedPrice(originalPrice, discount) {
  return originalPrice - originalPrice * discount;
}

export function power(base, exponent) {
  return base ** exponent;
}
```

如您所见，代码很简单。

# 如果你在本地创建一个新的包

如果您想要复制代码文件而不是整个存储库，那么有一个问题。您需要:

1.  使用:`npm init`生成一个包，这样，您的节点依赖项就安装在当前文件夹中。
2.  通过添加到`package.json`，将代码切换为*模块*:

```
{
  …
  "type": "module",
  …
}
```

你可以在[我的回购](https://github.com/how-to-js/how-to-unit-test/blob/main/package.json#L6)里看到是怎么做的。

# 安装茉莉

我们将要测试的代码在 browser 或 Node 上的工作方式是一样的。为了简单起见，让我们在 Node 上测试它。首先，我们需要安装 Jasmine。为此，让我们跟随[官方文件](https://jasmine.github.io/pages/getting_started.html):

```
$ npm install --save-dev jasmine #1

$ npx jasmine init #2
```

这些命令执行以下功能:

1.  将 Jasmine 安装为开发依赖项
2.  在`spec/support/jasmine.json`中生成基本配置:

```
{
  "spec_dir": "spec",
  "spec_files": [
    "**/*[sS]pec.?(m)js"
  ],
  "helpers": [
    "helpers/**/*.?(m)js"
  ],
  "env": {
    "stopSpecOnExpectationFailure": false,
    "random": true
  }
}
```

最后，让我们更新`package.json`来配置测试命令:

```
{
  …
  "scripts": {
    "test": "jasmine"
  },
  …
}
```

# 运行(无)测试

至此，您应该已经完成了所有必要的配置，并且没有进行任何测试。让我们看看它是否像预期的那样工作:

```
$ npm test

> how-to-unit-test@1.0.0 test
> jasmine

Randomized with seed 10285
Started

No specs found
Finished in 0.002 seconds
Incomplete: No specs found
Randomized with seed 10285 (jasmine --random=true --seed=10285)
```

# 示例测试

让我们添加一个简单的测试。我们将创建一个与 Jasmine 约定匹配的新文件`./spec/pure-functions.spec.js`:

*   它在`./spec`文件夹中——遵循在生成的配置的这一行中设置的内容:`"spec_dir": "spec",`
*   它以`spec.js`结束——在`"spec_files": ["**/*[sS]pec.?(m)js"`中建立的另一种命名模式

进入`./spec/pure-functions.spec.js`内部的代码:

```
import { greet } from "../pure-functions.js";

describe("greet", () => {
  it("should greet by name & surname", () => {
    expect(greet("Lorem", "Ipsum")).toEqual("Hello Lorem Ipsum!");
  });
});
```

代码:

*   `import { greet } from "../pure-functions.js";`-从我们的源代码中获取函数。如果没有`package.json`中的`"type": "module",`，这条线将无法正常工作。
*   `describe("", <callback>)`-包装相关测试以获得更好的错误消息。
*   `it("", <callback>)`——单项测试，
*   `expect(<value>).<matcher>(<arguments>);`-这是我们在 Jasmine 中设定期望的方式。你可以在文档中找到[匹配器。](https://jasmine.github.io/api/edge/matchers.html)

# 快跑！

该测试运行:

```
$ npm run test

> how-to-unit-test@1.0.0 test
> jasmine

Randomized with seed 09863
Started
.

1 spec, 0 failures
Finished in 0.004 seconds
Randomized with seed 09863 (jasmine --random=true --seed=09863)
```

# 最终代码

你可以在这里找到我的最终代码。

# 家庭作业

这里有一些家庭作业:获取代码，并继续重新实现第一篇文章中的测试。欢迎大家在评论里分享成绩或者奋斗！

*最初发布于*[*https://how-to . dev*](https://how-to.dev/how-to-start-unit-testing-with-jasmine)*。*

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW)**。**