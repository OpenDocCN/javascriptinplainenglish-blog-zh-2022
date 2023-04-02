# 我喜欢 Tailwind CSS 的 10 个原因以及你可能也会喜欢它的原因

> 原文：<https://javascript.plainenglish.io/10-reasons-why-i-love-tailwind-css-and-why-you-may-love-it-too-43b7738558ca?source=collection_archive---------4----------------------->

## 读完这篇文章后，如果你还没有爱上顺风，你也会爱上它。

![](img/ca3b6decf6be4e82273a8f702ee4d41b.png)

Photo by [Clark Van Der Beken](https://unsplash.com/@snapsbyclark?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我从普通 CSS 开始了我的前端之旅，然后去了 SCSS，一旦我学会了 SCSS，学习样式化组件就是小菜一碟，因为从语法角度来说，它们非常相似。有一段时间，SCSS 是我最喜欢的(现在仍然是，但不是每个项目，是的，特别是 SCSS，而不是萨斯)。

然而，我已经推迟使用 Tailwind CSS 很长时间了。后来有一天，我决定开放他们的游乐场，给他们一个机会。我花了一个[小项目](https://codepen.io/kens-visuals/full/dyJyxNz)就上当了。现在我想分享你也应该尝试一下的 10 个理由。

## 1.这很容易设置

是的，很容易安装，你所要做的就是遵循他们的[安装指南](https://tailwindcss.com/docs/installation)。他们也有针对不同框架的。只需安装软件包，就差不多完成了。

## 2.易于配置

为什么我说你差不多完成了？因为，安装只是第一步。接下来，你需要[配置它](https://tailwindcss.com/docs/configuration)根据你当前项目的风格和需求，你可以添加你的配色方案，字体，几乎每个类都可以定制。或者为了方便起见，您可以添加实用程序类。这是一次性的事情，只需在开始时设置一次，并在项目的其余部分使用它。

这是我上当的另一个原因，因为我喜欢我的代码尽可能有条理。这是完美的，因为我的风格的所有配置都在一个文件中。以下是来自[我的副项目](https://github.com/kens-visuals/markdown-notes-app)的`tailwind.config.js`文件的简单示例:

[](https://markdown-notes-app-delta.vercel.app/) [## 降价应用

### 用 NextJS 和 Firebase Firestore 构建的 Markdown 编辑器。由 Kens 编码-视觉

markdown-notes-app-delta . vercel . app](https://markdown-notes-app-delta.vercel.app/) 

```
module.exports = {
  darkMode: 'class',
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        'primary-1000': '#151619',
        'primary-900': '#1D1F22',
        'primary-800': '#2B2D31',
        'primary-700': '#35393F',
        'secondary-600': '#5A6069',
        'secondary-500': '#7C8187',
        'secondary-400': '#C1C4CB',
        'secondary-300': '#E4E4E4',
        'tertiary-200': '#F5F5F5',
        'orange-primary': '#E46643',
        'orange-secondary': '#F39765',
      },
      fontFamily: {
        roboto: ['Roboto', 'sans-serif'],
        'roboto-mono': ['Roboto Mono', 'monospace'],
        'roboto-slab': ['Roboto Slab', 'serif'],
      },
      fontSize: {
        'heading-1': ['2rem', '2.625rem'],
        'heading-2': ['1.75rem', '2.3125rem'],
        'heading-3': ['1.5rem', '2rem'],
        'heading-4': ['1.25rem', '1.625rem'],
      },
    },
  },
  plugins: [require('@tailwindcss/typography')],
};
```

## 3.灵活定制

当然，其中一个优点是它已经有了很多内置的类，但是它并不限制你定制它，使它更加个性化。除了添加自定义类，还可以添加插件，比如 Autoprefixer、排版等。所以，不要担心被几个类和特性所束缚。

## 4.内置工具和功能

说到特性，Tailwind 有几个，它们肯定会让你的工作轻松 10 倍。例如，我最喜欢的内置功能是[黑暗模式](https://tailwindcss.com/docs/dark-mode)。如今，几乎每个网站都有一个黑暗模式，虽然这看起来很容易实现，但对于普通的 CSS 甚至 SCSS 来说就不那么容易了。

使用 Tailwind CSS，你可以简单地在你的样式前添加`dark:`来指定你的黑暗模式。请参见下面的示例:

```
<div class="bg-white **dark:bg-slate-800 dark:text-white** rounded-lg px-6 py-8 ring-1 ring-slate-900/5 shadow-xl">
  ...
</div>
```

> 如果你仍然不相信 Tailwind CSS，并需要在你的下一个项目中添加黑暗模式，我想到了一个非常简单的用 SCSS 和普通 JavaScript 实现黑暗模式的方法。它也可以用于你喜欢的框架，你只需要根据你选择的框架改变 JavaScript 语法。

[](/how-to-create-a-dark-mode-with-sass-scss-and-vanilla-javascript-e1c7835cf474) [## 如何用萨斯/SCSS 和香草 JavaScript 创建一个黑暗模式

### 试图在萨斯/SCSS 创建一个黑暗模式？完成本教程后，你将学会最简单的技术。

javascript.plainenglish.io](/how-to-create-a-dark-mode-with-sass-scss-and-vanilla-javascript-e1c7835cf474) 

T-Pain shameless plug GIF from [GIPHY](https://giphy.com)

## 5.不再有类名

对于普通 CSS 或 SCSS，有一件事一直困扰着我，那就是类的命名。这看起来很简单，但却是一项非常复杂的任务。是的，有不同的约定应该有助于使这个任务更容易，比如 BEM，我曾经在我的每个项目中使用它。然而，为每一个事物想出类名可能是平凡而有问题的。

平凡，因为它就是平凡，从来没有人说过— *“哦，不，我在编程中最喜欢的事情是命名东西，尤其是 CSS 类”。*有问题，因为总是想出一些可重用的、可扩展的、容易被每个人理解的东西是相当困难的。

有多少次你不得不添加一个`div`，它将是某个东西的容器或包装器，但是你已经有了一个名为`.something__container`或`.something__wrapper`的类，现在如果你在它上面添加另一个，那么它或者在命名方面没有任何意义，并且会使其他开发人员困惑。

有了 Tailwind CSS，你就没有这样的问题了，因为没有命名类这样的事情。是的，你可以为你的按钮或标题添加一个或两个工具类。但同时，与其将它们作为类添加，还不如将它们作为组件提取到您喜欢的框架中。

## 6.无内疚感的内联 CSS

这是我对 Tailwind CSS 的第一个想法，*“哦，太酷了，所以我们只是在编写一个内联 CSS，而没有搞砸特殊性或关心类名？爽！”*。除此之外，用 Tailwind CSS 添加或删除特定的样式似乎更加自然。

例如，当某个东西被点击时，你需要添加一个特定的样式，在普通 CSS 或 SCSS 中，你需要想出一个类名，然后添加或删除那个类。

然而，在 Tailwind CSS 中，您可以在组件中添加和删除特定的类。例如，我没有创建一个可以直接在组件中编写的类，而是使用 React，所以语法可能会有所不同:

```
/* If data's length is longer or equal to 5, change overflow to scroll */
<div className={`${data.length >= 5 && ‘overflow-scroll’}`}>
  ...
</div> /* If the theme is dark change opacity to fully visible, if not change it to 50% visible. */
<div className={`transition-all duration-200 ${theme === 'dark' ? 'opacity-100' : 'opacity-50'}`}>
  ...
</div>
```

## 7.非常适合框架

如最后一个例子所示，Tailwind CSS 与 React 或其他框架的兼容性更好。在我看来，对于一个用 HTML 和 Vanilla JS 编写的小项目来说，Tailwind 有点大材小用。在这种情况下，SCSS 甚至普通的 CSS 更适合。

特别是，如果你刚刚开始前端开发，尝试自己做所有的事情，而不是使用库。至少我刚开始做副业的时候是这样的。一旦我学会了如何从零开始构建一切，并理解了我的每一段代码是如何在风格和功能方面工作的，然后我就转向了 Tailwind CSS 和其他库，以使我的工作更容易。

## 8.最小化 CSS

Tailwind CSS 不仅可以最小化你的 CSS，还可以自动清除不用的样式。当然，这可以用普通的 CSS 或 SCSS 来实现，但是你需要额外的插件来实现。然而，我喜欢 Tailwind CSS 为我处理繁重工作的方式。

## 9.顺风照顾无聊的东西

另一件可以被认为是平凡的任务，是重置 CSS。这是一件很无聊但又很必要的事情，以至于我不得不在使用 SCSS 的时候创建一个模板，这样我的重置在我的项目中是一致的。

然而现在，Tailwind CSS 承担了这一负担，它肯定会在项目中保持一致，易于访问，并且与当前的标准和最佳实践保持一致。

## 10.您可以配置一次，然后随时随地使用它

这不是专门针对顺风的，因为我已经提到过我曾经为我的 SCSS 项目准备了一个模板文件，所以我想我也可以为顺风做一些类似的事情。

这就是为什么我为 React 和 Tailwind CSS 创建了这个简单的[样板](https://github.com/kens-visuals/react-tailwind-boilerplate)。为什么？因为我宁愿键入`git clone [git@github.com](mailto:git@github.com):kens-visuals/react-tailwind-boilerplate.git`，然后结束。

然后安装`create-react-app`，安装`Tailwind CSS`，添加其配置，删除不必要的文件，吖哒，吖哒，吖哒。这个样板文件对我来说只是一个起点，克隆回购，然后根据项目进行定制。

# 综上

这既不是由 Tailwind CSS 支付的，也不是由它赞助的，当然，就像所有其他人造的东西一样，Tailwind CSS 并不完美。但它确实很棒，值得一试。刚开始的时候，为了适应这些课程，可能会感觉很奇怪。但是感谢 [Tailwind CSS 扩展](https://tailwindcss.com/docs/editor-setup)，你不需要记忆任何东西。

有些人可能会说——*“但是肯它看起来很丑，一堆课摆在我面前，调试会很难”*、*、*我只会回应——*“有些人只是害怕变化，不想学习新技术，他们只是想找借口，以避免走出他们的舒适区”。*

试一试，如果你因为任何原因觉得它不适合你，就继续前进。没有人会强迫你使用它，除非你的公司正在使用它，那么你的老板会确保你使用它🙃

玩笑归玩笑，永远不要害怕学习新的东西。有时候……其实大多数时候，你的大脑会试图找借口阻止你去做或者学习新的东西，所以你需要意识到，走出自己的舒适区是为你好。

感谢阅读，我希望你从这篇文章中获得一些有用的东西，并且你会考虑学习一些你已经推迟了一段时间的新东西。

[](https://medium.com/@kens_visuals/membership) [## 通过我的推荐链接加入 Medium-Ken Nersisyan

### 用媒介释放你的潜能。立即加入，阅读我和其他顶尖作家的文章。读书，学习，变得更好…

medium.com](https://medium.com/@kens_visuals/membership) 

# 进一步阅读

[](/how-to-fix-tailwind-css-intellisense-in-visual-studio-code-3dede794df21) [## 如何在 Visual Studio 代码中修复 Tailwind CSS 智能感知

### TailwindCSS 智能感知在 VS 代码中不起作用？按照文章中的步骤来修复它。

javascript.plainenglish.io](/how-to-fix-tailwind-css-intellisense-in-visual-studio-code-3dede794df21) [](/why-i-change-the-font-size-to-62-5-in-every-project-45c5ff785fb5) [## 为什么我在每个项目中将字体大小改为 62.5%

### 帮助你简化计算的小开发技巧。

javascript.plainenglish.io](/why-i-change-the-font-size-to-62-5-in-every-project-45c5ff785fb5) [](/how-to-master-problem-solving-as-a-programmer-d16a0b8780ab) [## 作为程序员如何掌握解决问题的能力

### 14 种练习解决问题的资源以及我是如何掌握技能的。

javascript.plainenglish.io](/how-to-master-problem-solving-as-a-programmer-d16a0b8780ab) [](/the-philosophy-of-chess-and-programming-3e435ef8bf14) [## 象棋和编程的哲学

### 我一直在思考国际象棋和编程之间的相似之处，下面是我的体会。

javascript.plainenglish.io](/the-philosophy-of-chess-and-programming-3e435ef8bf14) [](/how-to-master-web-development-in-30-days-8f6d29237361) [## 如何在 30 天内掌握 Web 开发

### 什么是前端导师，它如何帮助我练习技能并走出教程地狱？

javascript.plainenglish.io](/how-to-master-web-development-in-30-days-8f6d29237361) 

# 让我们连接

[](https://twitter.com/kens_visuals) [## 在推特上关注我﹫kens_visuals

### 👨🏻‍💻👾

twitter.com](https://twitter.com/kens_visuals) [](https://github.com/kens-visuals) [## kens-视觉效果—概述

### 前端开发者| JS 爱好者|科技写手。kens-visual 有 67 个存储库。遵循他们的准则…

github.com](https://github.com/kens-visuals) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****