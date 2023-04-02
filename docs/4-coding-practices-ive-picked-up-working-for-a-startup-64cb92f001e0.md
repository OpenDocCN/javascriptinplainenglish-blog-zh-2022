# 我在创业公司工作时学到的 4 个编码实践

> 原文：<https://javascript.plainenglish.io/4-coding-practices-ive-picked-up-working-for-a-startup-64cb92f001e0?source=collection_archive---------6----------------------->

![](img/b2df63ec84608d236adc9817cf92a0df.png)

Photo by [Nate Grant](https://unsplash.com/@nateggrant?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在公司的阶梯上向上爬不再依赖于你多年的经验。当然，这可能是决胜局的决定性因素，但它并不能说明你能带来什么。更重要的是你如何编写你的代码，代码的质量，以及将来重用这些代码的可能性。学习业内采用的最佳惯例就像浏览众所周知的开源代码或阅读您正在使用的工具的一页纸一样简单— [Vue](https://v3.vuejs.org/style-guide/) 、 [C#](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) 、 [JavaScript](https://developer.mozilla.org/en-US/docs/MDN/Guidelines/Code_guidelines/JavaScript) 。但这还不是全部——在你继续阅读本文时，会涉及到更多的内容。

## **可扩展性设计**

通常，当我们想到可伸缩性设计时，我们会想到编写以后才会用到的代码。这与事实相差甚远！这样的代码从一开始就不应该存在——它会产生技术债务，如果它最终根本不被使用，还会导致可维护性问题！

可伸缩性的主要思想是从一开始就使用它，以便它可以在未来的短跑或马拉松中以最小的努力和很少或没有变化进行扩展。举个例子，我工作的初创公司已经与许多工资单和 POS 公司合作，为我们的客户提供产品内无缝的第三方集成。虽然每个集成都是独一无二的，但是所需的任务基本上是相同的。

假设当从第三方系统 Gusto 和 BambooHR 中导入员工时，它们应该具有以下设置要求:
-位置映射(与第三方中的位置相对应的员工应该仅被添加到客户选择的位置)
-向所有成功导入的员工发送邀请的选项

这里，解决方案很简单，如下面的示例 Vue.js 代码所示:

```
<template>
  ...
  <location-mapping :set="setMapping"    :integration:"state.integration" v-if="state.index === 0" />
  <employee-invite :set="setInvite" v-if="state.index === 1"/>
  ...
  <button :click="nextTab" v-if="state.index !==1 ">Next</button>>
  <button :click="startImport" v-else">Start Import</button>
</template>
...
setup() {
  const state = reactive({
    index: 0,
    integration: $route.params.integration,
    configuration: {},
  }); function startImport() {
    startBackgroundJob(state.integration, state.configuration);
  } function setMapping(mapping) {
    state.configuration.locationMapping = mapping;
  } function setInvite(canInviteEmployees) {
    state.configuration.inviteEmployees = canInviteEmployees;
  } function nextTab() {
    state.index++;
  } return { state, startImport, setMapping, setInvite, nextTab };
}
```

但是，如果我们添加另一个集成 Zero，它也需要假期类型的映射(例如，将员工可能有的年假、病假和陪产假同步到我们的系统中)，会怎么样呢？我们可以复制上面的模板并添加一个新元素 leave-mapping，或者我们可以重用这个模板并确保集成只看到它们需要的元素。为了做到这一点，大多数开发人员会使用 if 语句，这是我下一次编码实践的完美切入点。

## 除非完全必要，否则避免使用 if 语句

```
if gusto show this:
   ...
if bamboohr show that:
   ...
...
```

虽然这应该可以做到，但是这样做会导致代码不可读，并且可能更难扩展，特别是如果您正在处理比上面提到的 3 个集成更多的集成的话。

相反，以 JavaScript 对象的形式使用定义要快得多，并且使应用程序更容易扩展。看看下面的代码👨‍💻

```
LOCATION_MAPPING = {
  COMPONENT: 'location-mapping',
  ...otherRequiredProperties,
}
EMPLOYEE_INVITE = {
  COMPONENT: 'employee-invite',
  ...otherRequiredProperties,
}
LEAVE_TYPE_MAPPING = {
  COMPONENT: 'leave-type-mapping',
  ...otherRequiredProperties,
}INTEGRATIONS = {
  BAMBOOHR: [LOCATION_MAPPING, EMPLOYEE_INVITE],
  GUSTO: [LOCATION_MAPPING, EMPLOYEE_INVITE],
  ZERO: [LOCATION_MAPPING, LEAVE_TYPE_MAPPING, EMPLOYEE_INVITE],
}
```

我们已经创建了一个对象，它保存了我们正在为这个特定任务处理的所有集成。每个集成都有它将使用的组件的属性，例如，BambooHR 使用 LOCATION_MAPPING 和 EMPLOYEE_INVITE，这反过来为我们提供了与它们相关的有用信息，使我们能够进行扩展。其中一个信息是 COMPONENT，它告诉我们与它们相关的 Vue 模板的名称。通过获得组件的名称，我们可以利用 Vue 的[元组件](https://v3.vuejs.org/api/built-in-components.html#component)，它允许我们根据需要动态地呈现我们需要的组件:`<component :is="componentName" />`

现在，我们的代码应该看起来更加整洁，只需做很少的修改，我们应该能够根据需要将这个特性扩展到许多集成中。它不仅有助于提高可伸缩性，还极大地提高了代码的可读性和可维护性。

```
<template>
  ...
  <component :is="state.currentTab" />
  <button :v-if="state.hasNext" @click="nextTab">Next</button>
  <button :v-else @click="startImport">Start Import</button>
</template>
// import definitions
// import components
...
setup() {
  const state = reactive({
    tabIndex: 0,
    state.integration: $route.params.integration,
    currentTab: computed(() => INTEGRATIONS[state.integration][state.tabIndex].COMPONENT),
    hasNext: computed(() => state.tabIndex + 1 !== INTEGRATIONS[state.integration].length
  }); function nextTab() {
    state.tabIndex++;
  } function startImport() {
    // Do what is needed
  } return { state, nextTab, startImport };
}
```

还有很多原因可以解释为什么应该避免使用`if`语句，但那将是另一篇文章！

## 命名约定

自古以来，给事物命名就一直是个大问题。是的，你可能会将一个变量命名为`alien`、`wizard`，或者有一个`do_things`函数，然而，虽然它会在那一刻完成工作，但它也会让下一个人，甚至是未来的你自己，更难理解变量和函数的用途。您将花费宝贵的工程时间回溯代码，以获得正在发生的事情的一些上下文，而不是直接修复一个 bug 或引入一个新特性。

当涉及到命名变量和函数时，我遵循的一个规则是使用对任何利益相关者来说都很清楚的词语，以便很好地理解变量或函数的用途。卡尔·亚历山大在这方面有一篇很棒的文章[值得一读！](https://carlalexander.ca/importance-naming-programming/)

## 评论

就像 if 语句一样，注释是最好不要写在代码中的东西之一。它有助于程序员更好地理解代码吗？嗯，看情况。请看下面的代码块:

```
// start count
let count = 0;
```

这个评论是否包含了仅通过阅读代码无法获知的信息？一点也不！这样的注释是破坏性的，需要程序员不断切换上下文，这是有代价的。主要的经验法则是编写不需要你用简单的英语解释它做什么的代码。这也意味着拥有一个只做一件事的函数，这与正确命名事物密切相关。拥有一个名为`getThirdPartySalesData`的函数应该可以让我们知道我们可以从这个函数中得到什么，因此根本不需要注释！也就是说，理解函数所需的参数是很棘手的，在这种情况下，更棘手的是知道返回的对象有什么属性。对于这种情况，出于文档的目的，我们可以使用 JSDoc、PHPDoc 等等。

JSDoc 是 JavaScript 的文档生成器，它分析代码并自动生成包含所有文档的静态页面。这在与大型团队合作时非常好，但我们追求的是它与 IDE /代码编辑器的集成，通过自动完成建议使编程更加容易。

*更多内容尽在* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*