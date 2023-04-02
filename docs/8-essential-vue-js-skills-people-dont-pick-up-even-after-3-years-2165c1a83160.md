# 8 项人们 3 年后也不会掌握的基本技能

> 原文：<https://javascript.plainenglish.io/8-essential-vue-js-skills-people-dont-pick-up-even-after-3-years-2165c1a83160?source=collection_archive---------5----------------------->

![](img/eb0aefb52536b4544b50de240540d185.png)

**武术的这 8 项技能在日常工作中非常有用。一些朋友说他们有三年的工作经验，但他们仍然不知道如何使用它们。你知道如何使用它们吗？那我们来看看:**

**1。使用引号来监听嵌套属性**

话虽如此，我们可以通过使用引号很容易地直接听到嵌套值:

```
watch {
‘$route.query.id’() {
//…
} }
}
```

**2 .是否使用 v-if**

有时，与其使用 v-if，不如使用 v-show，这样性能会更高。

```
<ComplicatedChart v-show=”chartEnabled” />
```

当 v-if 打开或关闭时，它将创建并完全破坏元素。相反，v-show 将创建元素并将其留在那里，通过将其样式设置为显示来隐藏它:无。

如果您要切换的组件渲染成本很高，那么这样做更有效。当然，如果您不需要立即执行昂贵的组件，您可以使用 v-if，这样它会跳过渲染，并使页面加载更快一点。

**3 .重写子组件的样式**

限定范围的 CSS 非常擅长保持内容整洁，并且不会将样式引入到应用程序的其他组件中。但是有时您需要覆盖子组件的样式，超出范围。Vue 有一个深度选择器:

```
<style scoped>
.my-component >>> .child-component {
font-size: 24px;
}
</style>
```

注意:如果使用像 SCSS 这样的 CSS 预处理器，您可能需要使用/deep/来代替。

**4 .倾听你组件中的任何声音**

```
export default {
computed: {
someComputedProperty() {
// Update the computed prop
},
},
watch: {
someComputedProperty() {
// Do something when the computed prop is updated
} }
} }
};
```

我们可以监测:
1。计算属性
2。道具
3。嵌套值

当使用 composition API 时，任何值都可以被观察到，只要它是一个参考或反应对象。

**5。检测元素外部(或内部)的点击**

```
window.addEventListener(‘mousedown’, e => {
const clickedEl = e.target;

if (el.contains(clickedEl)) {
} else {
} }
});
```

**6。多文件单文件组件**

这是**SFC(单文件组件)**的一个鲜为人知的功能。文件可以像普通的 HTML 文件一样导入:

```
<template src=”./template.html”></template>
<script src=”./script.js”></script>
<style scoped src=”./styles.css”></style>
```

如果您需要共享样式、文件或其他任何东西，这将非常方便。

**7。将道具限制在类型列表中**

使用 prop 定义中的 validator 选项，可以将 prop 类型限制为一组特定的值。

```
export default {
name: ‘Image’,
props: {
src: {
type: String,
},
style: {
type: String,
validator: s => [‘square’, ‘rounded’].includes(s)
} }
} }
};
```

该验证函数接受一个道具，如果该道具有效或无效，则返回 true 或 false。当只通过真或假来控制某些条件不能满足要求时，一般用这种方法来做到最好

**8。融合本地和全球风格**

一般来说，在处理样式时，我们希望将它们分成一个单独的组件。

`<style scoped>
.component {
background: green;
} }
</style>`

如果需要，您也可以添加一个非作用域样式块来添加全局样式

```
<style> 
.component p {
margin-bottom: 16px;
} }
</style>
```

```
<style scoped>
.component {
background: green;
} }
</style>
```

但要小心，全球风格很危险，也很难追踪。但有时，它们是完美的逃生舱，正是每个人所需要的

**感谢您的阅读，期待您的关注。**

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****