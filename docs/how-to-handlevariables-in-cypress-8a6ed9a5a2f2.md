# 如何在 Cypress 中处理变量

> 原文：<https://javascript.plainenglish.io/how-to-handlevariables-in-cypress-8a6ed9a5a2f2?source=collection_archive---------2----------------------->

## 关于如何在 Cypress 中处理变量的教程。

![](img/56e1e73dabd4b0c2b81fffa2bfc74222.png)

在本教程中，我们将学习如何在 Cypress 中处理变量。由于 Cypress 处理承诺的方式，在 Cypress 中处理变量并不像看起来那么简单。让我们来看看——

# 理解问题

```
it("gets the text of the heading and assert the value", () => {
    // get the text
    cy.get("h1.elementor-heading-title").then(($heading) => {
      expect($heading.text()).to.eq("Think different. Make different.");
    })
  });
```

在上面的例子中，我们试图获取元素的文本，然后对其进行断言。如果你想在`cy.get`块之外使用标题文本，该怎么做呢？简单地说，创建这样的变量是行不通的

```
it("gets the text of the heading and assert the value", () => {
    let headingText = '';
    // get the text
    cy.get("h1.elementor-heading-title").then(($heading) => {
      headingText = $heading.text()
      expect($heading.text()).to.eq("Think different. Make different.");
    })
    // X - would print just an empty string
    console.log(headingText); 
  });
```

因为`cy.get`是一个`async`命令，所以`console.log`不会打印任何东西是因为它甚至会在`cy.get`命令被执行之前被打印。因此，我们需要一种方法，先等待`cy.get`命令完成，然后打印出我们的文本。

# 在 Cypress 中处理变量

在 Cypress 中有两种方法可以处理测试块中的变量。

*   **访问同一块内的变量**

```
it("gets the text of the heading and assert the value", () => {
    // get the text
    cy.get("h1.elementor-heading-title").then(($heading) => {
      let headingText = $heading.text()
      expect($heading.text()).to.eq("Think different. Make different.");
      // Use the heading text value here
      console.log(headingText);   
    })
  });
```

这个非常简单，因为只要需要访问上下文或变量，就可以在同一个块中继续创建嵌套块。

*   **访问块外变量**

```
it("gets the text of the heading and assert the value", () => {
    // get the text
    cy.get("h1.elementor-heading-title").then(($heading) => {
      let headingText = $heading.text();
      expect($heading.text()).to.eq("Think different. Make different."); // return the text so it can be used in .then as a parameter
      return headingText; 
    }).then(hText => {
      // hText param holds the value of the above returned text
      console.log(hText);
    })
  });
```

使用`.then`块，您可以访问先前返回的值，然后将其作为参数传递给`.then`块。这样，如果在同一个上下文中，就可以将多个方法链接在一起。
这里需要注意的重要一点是，它只适用于`.then`模块，不适用于`.should`。

# 要了解更多信息，请查看下面的视频——

👩🏻‍💻是时候加入 SDET 大学学院，开始你的 SDET 之旅了👇🏻
[加入学院](https://bit.ly/3Vcqv69)

📧订阅我的[邮件列表](https://automationbro.com/mailing-list)以获取更多类似的内容，并成为令人惊叹的免费赠品的一部分。

👍你也可以在这里关注我的内容

*   [推特](https://twitter.com/automationbro)
*   [领英](https://www.linkedin.com/company/automation-bro)

感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***