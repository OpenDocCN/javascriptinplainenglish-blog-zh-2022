# 使用 Cypress 测试你的 HTML

> 原文：<https://javascript.plainenglish.io/using-cypress-to-test-your-html-6431eaf7e770?source=collection_archive---------11----------------------->

## 深入探究 Cypress 的可操作命令

![](img/0771d53c311b41decc71441b80f0c90f.png)

[Photo by Mark Munsee](https://www.pexels.com/photo/concrete-road-between-trees-1058592)

Cypress 是一个非常有趣的测试工具。作为一名软件开发人员，我喜欢确保我的代码做了它被设计要做的事情。测试本身就是一整套技能，需要很长时间才能精通。因为我们的时间不是无限的，我们需要确保我们的代码不会破坏我们的工作，所以我们需要一种方法来测试页面上的元素，即使是在我们未来构建的基础上。我们如何处理构建、测试特性以及回归测试？输入 Cypress 可操作的命令！

这些允许我们编写与应用程序交互的测试。这使得我们的代码即使在将来也是完全可靠的。因为我们可以设置我们的项目在提交代码到我们的存储库时运行这些测试，我们可以确保我们的新代码不会破坏现有的代码和应用程序的预期功能。让我们深入了解这些漂亮的命令！

# 可操作的命令

在 Cypress 中，我们有几个可操作的命令供我们使用。这些操作包括从单击到双击、选中和取消选中复选框以及键入等等。

## 单击()-单击元素。

这很简单。如果我们有一个按钮或链接，我们可以模拟点击该元素。我们会想告诉 Cypress 我们关心哪个元素，然后从那个元素链接点击功能。

```
✅ Correct usage

  cy.get('.primary-button').click();

❌ Incorrect usage

  cy.click('.primary-button');
```

我们可以传递的参数有`position`、`x or y coordinate`或`options`

```
// Position

cy.get('.primary-button').click('topRight');

// X / Y Coordinates

cy.get('.primary-button').click(10, 12);

// Options(See docs below)

cy.get('.primary-button').click({ 
  altKey: true
});
```

[](https://docs.cypress.io/api/commands/click#Syntax) [## 点击| Cypress 文档

### 单击一个 DOM 元素。正确用法不正确用法发出咔哒声的位置。中间位置…

docs.cypress.io](https://docs.cypress.io/api/commands/click#Syntax) 

## dblclick() —双击一个元素

就像单击一样，我们也可以双击一个元素。

```
✅ Correct usage

  cy.get('.primary-button').dblclick();

❌ Incorrect usage

  cy.dblclick('.primary-button');
```

我们可以传递的参数是`position`、`x or y coordinate`或`options`

```
// Position

cy.get('.primary-button').dblclick('topLeft');

// X / Y Coordinates

cy.get('.primary-button').dblclick(5, 72);

// Options(See docs below)

cy.get('.primary-button').dblclick({ 
  shiftKey: true
});
```

[](https://docs.cypress.io/api/commands/dblclick) [## dblclick | Cypress 文档

### 双击一个 DOM 元素。正确用法不正确用法双击应该发出的位置。的…

docs.cypress.io](https://docs.cypress.io/api/commands/dblclick) 

## 右键单击()-右键单击元素

右键功能允许我们围绕上下文菜单事件编写代码，而不是上下文菜单本身(这是不赞成的(我在下面附上了解释这两者的文档))。

```
✅ Correct usage

  cy.get('#primary-menu').rightclick()

❌ Incorrect usage

  cy.rightclick('#primary-menu');
```

我们可以传入的参数是`position`、`x or y coordinate`或`options`

```
// Position

cy.get('#primary-menu').rightclick('topLeft')

// X / Y Coordinates

cy.get('.primary-button').rightclick(5, 72);

// Options(See docs below)

cy.get('.primary-button').rightclick({ 
  shiftKey: true
});
```

[](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event) [## 上下文菜单事件-Web API | MDN

### 当用户试图打开上下文菜单时，将触发 contextmenu 事件。此事件通常由以下因素触发…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event) [](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contextmenu) [## 上下文菜单-Web API | MDN

### 已弃用:不再推荐此功能。虽然一些浏览器可能仍然支持它，但它可能已经…

开发者. mozilla.org\](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contextmenu) [](https://docs.cypress.io/api/commands/rightclick#Syntax) [## 右键单击| Cypress 文档

### 右键单击 DOM 元素。。右键单击()不会打开浏览器自带的上下文菜单..应该使用右键单击()

docs.cypress.io](https://docs.cypress.io/api/commands/rightclick#Syntax) 

## type() —键入元素

如果您有输入框，并希望确保用户可以在其中输入，这是您的定位命令。

```
✅ Correct usage

  cy.get('.first-name-input').type('Text here');

❌ Incorrect usage

  cy.type('Text here');
```

type()的可用参数是`text`和`options.`

```
// Text

cy.get('.first-name-input').type('Text here');

// Options(See docs below)

cy.get('.first-name-input').type({
  delay: 10
});
```

如果你想模仿用户在打字时按键，你可以传入你想要模仿的按键。例如，如果我想模仿用户在输入前按下 ctrl 键，或者甚至在输入过程中，我们可以这样做(在附加的文档中有更多的例子)

```
cy.get('.test-input').type('{ctrl}test');

// or

cy.get('.test-input').type('test {shift}things');
```

[](https://docs.cypress.io/api/commands/type#Syntax) [## type | Cypress 文档

### 键入一个 DOM 元素。正确用法不正确用法要键入 DOM 元素的文本。文本传递到…

docs.cypress.io](https://docs.cypress.io/api/commands/type#Syntax) 

## clear() —清除`input`或`text area`中的值

这将清除值的输入字段

```
✅ Correct usage

  cy.get('[type="text"]').clear();

❌ Incorrect usage

  cy.clear();
```

对此可用的论据是`options.`

```
// Options(See docs below)

cy.get('[type="text"]').clear({
  log: true
});
```

[](https://docs.cypress.io/api/commands/clear) [## clear | Cypress 文档

### 清除输入或文本区域的值。正确用法不正确用法传入选项对象以更改默认…

docs.cypress.io](https://docs.cypress.io/api/commands/clear) 

## check() —选中复选框或单选元素

这将模拟在复选框内单击以选中一个选项

```
✅ Correct usage

  cy.get('[type="checkbox"]').check();

❌ Incorrect usage

  cy.check('[type="checkbox"]');
```

我们可以传入的参数是`Value`、`Values`和`options.`

```
// Value

cy.get('[type="checkbox"]').check('First Option');

// Values (An Array of options you would want checked)

cy.get('[type="checkbox"]').check([
  'First Option',
  'Second Option',
  'Third Option'
]);

// Options(See docs below)

cy.get('[type="checkbox"]').check({
  log: true
});
```

[](https://docs.cypress.io/api/commands/check#Usage) [## 检查| Cypress 文档

### 选中复选框或单选按钮。此元素必须是 with 类型的复选框或单选按钮。正确用法不正确用法…

docs.cypress.io](https://docs.cypress.io/api/commands/check#Usage) 

## 取消选中()—取消选中复选框

这将模拟在复选框内单击以取消选中某个选项

```
✅ Correct usage

  cy.get('[type="checkbox"]').uncheck();

❌ Incorrect usage

  cy.uncheck('[type="checkbox"]');
```

我们可以传入的参数是`Value`、`Values`和`options.`

```
// Value (This is a String of the value you want selected)

cy.get('[type="checkbox"]').uncheck('First Option');

// Values (An Array of options you would want unchecked)

cy.get('[type="checkbox"]').uncheck([
  'First Option',
  'Second Option',
  'Third Option'
]);

// Options(See docs below)

cy.get('[type="checkbox"]').uncheck({
  log: true
});
```

[](https://docs.cypress.io/api/commands/uncheck) [## 取消选中| Cypress 文档

### 取消选中复选框。应取消选中的复选框的用法值不正确。复选框的值…

docs.cypress.io](https://docs.cypress.io/api/commands/uncheck) 

## select() —在`select`中选择一个`option`

```
✅ Correct usage

  cy.get('.users-select').select('first-user-option');

❌ Incorrect usage

  cy.select('Chewbacca');
```

我们可以传入的参数是`Value`、`Values`和`options.`

```
// Value (This is a String of the value you want selected)

cy.get('.users-select').select('Jeremy');

// Values (An Array of options you would want selected)

cy.get('.users-select').select([
  'Jeremy',
  'Shannon'
]);

// Options(See docs below)

cy.get('.users-select').select({
  log: true
});
```

[](https://docs.cypress.io/api/commands/select) [## 选择| Cypress 文档

### 正确用法错误用法要选择的的值、索引或文本内容。一组值、索引或…

docs.cypress.io](https://docs.cypress.io/api/commands/select) 

我希望这是对 Cypress 可操作事件世界的一次有益的探索。虽然这并不是每一个内置函数，但在我的经验中，这些函数是最有用的。

# 关于我

> 嘿，你好！我是杰里米。我写一些关于前端开发的文章来帮助初学者更好地理解 Web 开发的内部工作。如果你对这篇文章有任何疑问，请在 LinkedIn[*@ JeremyGrice*](https://www.linkedin.com/in/jeremylgrice/)*或在我的个人网站上发表评论，我会尽快回复你*

[](https://medium.com/@vetthatcodes) [## 检查代码-中等

### 从检测介质上代码中读取文字。我在 Red Van Workshop 做全职网页开发人员。我喜欢咖啡…

medium.com](https://medium.com/@vetthatcodes) 

# 如果您觉得这篇文章有帮助或有趣，请不要犹豫点击👏按钮，或者如果您有任何问题，请在下面留下您的评论。

# 另外，别忘了看看我的其他文章

[](/learn-the-javascript-basics-part-1-c4450643fbea) [## 学习 JavaScript 基础知识

### 第 1 部分:声明和使用变量、操作符，以及声明字符串/模板文字的各种方式。

javascript.plainenglish.io](/learn-the-javascript-basics-part-1-c4450643fbea) [](/testing-your-front-end-code-with-cypress-4a3c64ab89d4) [## 用 cypress 测试你的前端代码

### 通过编写端到端测试使您的代码更加安全

javascript.plainenglish.io](/testing-your-front-end-code-with-cypress-4a3c64ab89d4) [](https://enlear.academy/build-deploy-a-great-looking-site-with-nextjs-and-netlify-eb9e59a7e0ad) [## 用 NextJS 和 Netlify 构建和部署一个漂亮的站点

### 想要比说伍斯特郡酱还快地构建和部署您的 javascript 应用程序吗？那看不…

enlear .学院](https://enlear.academy/build-deploy-a-great-looking-site-with-nextjs-and-netlify-eb9e59a7e0ad) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。***