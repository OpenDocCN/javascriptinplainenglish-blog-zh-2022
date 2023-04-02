# 如何用 Cypress 测试你的前端代码

> 原文：<https://javascript.plainenglish.io/testing-your-front-end-code-with-cypress-4a3c64ab89d4?source=collection_archive---------2----------------------->

## 通过编写端到端测试使您的代码更加安全

![](img/769abfa28e2e478c501b428d3abb93bb.png)

[Photo by Johannes Plenio](https://www.pexels.com/photo/forest-covered-in-white-fog-1423600/)

# **关于我**

> 你好。我是杰里米。我写一些关于前端开发的文章来帮助初学者更好地理解 Web 开发的内部工作。如果你对这篇文章有任何疑问，请留下评论，我会尽快回复你，或者登陆 LinkedIn [@JeremyGrice。你可以到我的个人网站查看](https://www.linkedin.com/in/jeremylgrice/)

# **为什么要用柏树？**

Cypress 使您能够编写所有类型的测试:

*   端到端测试
*   集成测试
*   单元测试

Cypress 可以测试任何在浏览器中运行的东西。

Cypress 是一个健壮的测试工具。它有很多非常酷的特性，并且可以做其他测试框架做不到的事情:

*   Cypress 将在您的测试运行时拍摄快照。当程序运行时，您可以将鼠标悬停在命令日志中的命令上，以查看程序运行时到底发生了什么。
*   停止猜测你的测试失败的原因。直接从你熟悉的工具中调试，比如浏览器开发工具。Cypress 使错误更具可读性。
*   不再有异步地狱。您永远不需要在测试中添加等待或休眠，因为 Cypress 会在继续之前自动等待命令和断言。
*   从 CLI 运行时，查看失败时自动拍摄的屏幕截图或整个测试套件的视频。

# **要求**

为此，您将需要以下内容:

*   macOS 10.9 及以上，Linux Ubuntu 12.04 及以上，Fedora 21 和 Debian 8，或 Windows 7 及以上(*仅限 64 位)*
*   Node.js 12 或 14 及以上版本

# **安装**

要安装 cypress，请将 cd 安装到您的项目所在的目录中，并运行这个命令

**NPM**

```
npm install cypress --save-dev
```

**纱线**

```
yarn add cypress --dev
```

之后，事情应该就好办了！

# **利用柏树**

[](https://docs.cypress.io/guides/overview/why-cypress) [## 为什么是柏树？Cypress 文档

### 什么是赛普拉斯，为什么你应该使用它我们的使命，我们相信在关键赛普拉斯的特点类型的测试…

docs.cypress.io](https://docs.cypress.io/guides/overview/why-cypress) 

现在我们已经做好了一切准备，让我们实际使用它。下面，我将介绍一些你可以用柏树做的事情的例子。

**访问网站**

让我们先从最基本的开始。如果我们想让我们的测试访问一个特定的站点呢？让我们利用`cy.visit()`并传入我们想要的 url。

```
describe('Our test', () => {
  it('Visits vetthatcodes', () => {
    cy.visit('https://www.vetthatcodes.com')
  })
})
```

当您运行这个测试时，您会注意到一些事情

*   [命令日志](https://docs.cypress.io/guides/core-concepts/cypress-app#Command-Log)现在显示`VISIT`动作
*   我们的网站被载入右侧的[应用预览](https://docs.cypress.io/guides/core-concepts/cypress-app#Overview)窗格
*   我们的测试是绿色的，这意味着它通过了(我们还没有使用任何断言，所以这是有意义的)

**Get()**

[](https://docs.cypress.io/api/commands/get#Syntax) [## 获取| Cypress 文档

### 通过选择器或别名获取一个或多个 DOM 元素。此命令的查询行为类似于…中的工作方式

docs.cypress.io](https://docs.cypress.io/api/commands/get#Syntax) 

使用 Cypress 时最常用的一个工具是`.get(...)`。这里的文档是。这允许您通过选择器获得一个或多个 DOM 元素。`get(...)`根据选择器返回一个元素——类似于 jQuery 的`$(...)`

举个例子，如果我们想获得一个元素，然后检查它是否被禁用，我们可以做以下事情

```
cy.get('input').should('be.disabled') 
```

关于`cy.get(...)`的几个旁注

*   它会自动重试，直到我们要找的东西存在于 DOM 中。
*   它将自动重试，直到所有链接的断言都已通过
*   它可以在等待 DOM 中存在东西时超时。
*   它可以在等待所有断言通过时超时。

# **断言**

[](https://docs.cypress.io/guides/references/assertions#BDD-Assertions) [## 断言| Cypress 文档

### Cypress 捆绑了流行的 Chai 断言库，以及对 Sinon 和 jQuery 有用的扩展，为您带来…

docs.cypress.io](https://docs.cypress.io/guides/references/assertions#BDD-Assertions) 

> 断言是我们在测试中验证给定步骤的一种方式。这些断言决定了任何给定的步骤是否成功。断言验证测试中的元素、对象或应用程序的期望状态。

根据赛普拉斯的文件，我附上了一些比较常见的。这些我就不赘述了，因为可读性很强。

*   **不是**

```
expect(name).to.not.equal(‘Jeremy’)
```

*   **真**

```
expect(true).to.be.true;
```

*   **长度**

```
cy.get('li.selected').should('have.length', 1)
```

*   **类**

```
cy.get('form').find('input').should('not.have.class', 'enabled')
```

*   **值**

```
cy.get('textarea').should('have.value', 'this site is awesome')
```

*   **能见度**

```
cy.get('p').should('be.visible')// orcy.get('p.hidden').should('not.be.visible')
```

*   **存在**

```
cy.get('[data-cy="loading"]').should('not.exist')
```

*   **状态**

```
cy.get(':radio').should('be.checked')
```

*   **CSS**

```
cy.get('[data-cy="completed"]').should(
  'have.css',
  'text-decoration',
  'line-through'
);
```

*   **禁用属性**

如果我们有一个包含以下内容的 HTML 元素会怎么样

```
<input type="text" data-cy="input" disabled />
```

然后我们可以用

```
cy.get('[data-cy="input"]').should('be.disabled')
```

*   **链接断言**

```
<a data-cy="assertions-link" class="active" href="https://on.cypress.io" target="_blank">Cypress Docs</a>
```

然后，我们可以用一连串的断言来检查多个东西

```
cy.get('[data-cy="assertions-link"]')
  .should('have.class', 'active')
  .and('have.attr', 'href')
  .and('include', 'cypress.io')
```

**柏树上的承诺**

我们可以使用`Cypress.Promise`来创建承诺，所以如果你从像`[.then()](https://docs.cypress.io/api/commands/then)`这样的命令中返回一个承诺，Cypress 将不会继续，直到这些承诺解决。这是超级整洁，非常强大。让我们在下面写一个快速的例子。

```
cy.get('button').then((response) => {
  return *new* Cypress.Promise((resolve, reject) => {
    // write your custom logic here
  })
})
```

我们也可以像这样处理承诺中的错误

```
Cypress.Promise.onPossiblyUnhandledRejection((error, promise) => {
  throw error;
})
```

# **编写我们的第一个测试**

既然我们已经解决了所有这些问题，我确信我们会想要编写一个测试。我们测试的游戏计划如下

*   访问该页面以确保其加载
*   检查我们的主机名、端口和协议的准确性
*   检查标题

现在我们有了一个行动计划，我们想要编写我们的测试。

```
describe('Navigating to our URL', () => {
  it('is successful', () => {
    cy.visit('www.localhost:3000');
    cy.location().should((page) => {
      expect(page.hostname).to.equal('www.localhost');
      expect(page.port).to.equal('3000');
      expect(page.protocol).to.equal('http:');
    });
    cy.title().should('contain', 'cypress-testing');
  })
})
```

# 最佳实践

[](https://docs.cypress.io/guides/references/best-practices#How-It-Works) [## 最佳实践| Cypress 文档

### 2018 年 2 月，我们在 AssertJS 举办了“最佳实践”会议。本视频演示了如何接近…

docs.cypress.io](https://docs.cypress.io/guides/references/best-practices#How-It-Works) 

就像任何编程语言或工具一样，它应该总是有一套最佳实践。赛普拉斯也不例外。

虽然有很多事情你应该知道，但有两件最重要的事情一直在我脑海中挥之不去

1.  不要将基于 CSS 属性的元素作为目标，比如:`id`、`class`、`tag`
2.  添加`data-*`属性，使其更容易定位元素

这两件事都是如何选择和不选择你的元素的最佳实践，因为这两件事将使你的 Cypress 测试不会变得非常脆弱，并且应该防止事情破裂。

让我们很快过一遍。假设我们有这个按钮

```
<button id="primary-button" class="btn btn-small" name="submit-button" role="button" data-cy="submit-button">
  Submit
</button>
```

在我们的测试中选择这个元素的最佳方法是什么？由于在 web 开发中通过 id 来选择任何东西通常都是不好的做法，并且类有时可能会发生变化，所以我们很可能希望基于`data-cy="..."`来选择`.get()`

这是为什么呢？当使用 cypress 时，data-cy 是一个特定于 cypress 的选择器，我们可以将它添加到元素中。这给了我们一些东西，并告诉其他开发人员这是 cypress 特有的。我们可以像这样编写我们的选择器=> `cy.get('[data-cy="submit-button"]').click()`，这将防止我们的测试在将来中断。如果您想了解更多，可以在本节顶部的最佳实践链接中找到。

# 如果您觉得这篇文章有帮助或有趣，请不要犹豫点击👏按钮，或者如果您有任何问题，请在下面留下您的评论。

# 另外，别忘了看看我的其他文章

*   [构建&用 Next.js 和 Netlify 部署一个漂亮的网站](https://medium.com/enlear-academy/build-deploy-a-great-looking-site-with-nextjs-and-netlify-eb9e59a7e0ad)
*   [Async Await:我到底该怎么使用这个东西？](https://medium.com/enlear-academy/async-await-how-the-heck-do-i-use-this-thing-3199f0701041)
*   [通过承诺提升你的 javascript 技能](/level-up-your-skills-in-javascript-with-the-inclusion-of-promises-5a2c84f2fe71)
*   [我的所有文章](https://medium.com/@vetthatcodes)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***