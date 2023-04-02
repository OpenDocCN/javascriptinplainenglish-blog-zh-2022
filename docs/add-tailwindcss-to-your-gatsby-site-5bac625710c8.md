# 将 TailwindCSS 添加到您的 Gatsby 站点

> 原文：<https://javascript.plainenglish.io/add-tailwindcss-to-your-gatsby-site-5bac625710c8?source=collection_archive---------19----------------------->

## Gatsby 使得用插件添加 CSS 框架变得很容易，比如 *TailwindCSS* 和 *PostCSS*

![](img/22957a285be185b69278fbb68480f8a5.png)

Photo Illustration by David Fekke

*原发布于*[*https://fek . io*](https://fek.io/blog/add-tailwindcss-to-your-gatsby-site)*。*

我正在尝试了解所有新的 CSS 技术。在过去的几年里，其中一项技术变得越来越流行，那就是尾翼。

如果您不熟悉 Tailwindcss，它是一个 css 框架，为 web 开发人员提供了一组低级组件来设计网站。与 Bootstrap 等框架不同，它不是为一个按钮提供一个类，而是允许您使用多个类，用特定的类来专门设计元素的样式。使用 Tailwind 设计按钮样式的一种方法如下所示；

```
<button class="bg-green-500 text-white px-4 py-2 mt-3 mb-4 rounded">Press Me</button>
```

前面的代码将创建一个如下所示的按钮；

![](img/30a6209d9f6ba8a092f8ae41af6c2721.png)

虽然一开始使用所有这些类似乎有些冗长，但它让 web 开发人员可以非常精确地控制他们的布局，而不必编写大量的 CSS。

# 给盖茨比加上顺风

另一件令人高兴的事情是，他们有关于所有组件类以及如何将 Tailwind 与 Next.js、Vite 和 Gatsby 等其他框架集成的非常好的文档。我想用这篇文章来展示给现有的 Gatsby 站点添加 Tailwind 是多么容易。

您需要做的第一件事是将以下模块添加到您的 Gatsby 站点中；

```
> npm install -D tailwindcss postcss autoprefixer gatsby-plugin-postcss
```

这将添加 Tailwind 模块和 gatsby 插件，您将需要使用 Tailwind 和 Gatsby。添加完这些模块后，您需要使用以下命令初始化 Tailwind

```
> npx tailwindcss init -p
```

这将创建`tailwind.config.js`文件和`postcss.config.js`文件。

接下来，我们需要在我们的`gatsby.config.js`文件中启用 PostCSS。将以下插件添加到这个配置文件中。

```
module.exports = { plugins: [ 'gatsby-plugin-postcss', ],}
```

现在我们已经将 PostCSS 插件添加到 Gatsby 中，我们可以配置`tailwind.config.js`文件来扫描模板中的任何 tailwind 类用法。这可以通过将我们的源路径添加到`tailwind.config.js`文件来完成。

```
module.exports = { content: [ "./src/**/*.{js,jsx,ts,tsx}", ], theme: { extend: {}, }, plugins: [],}
```

现在让我们在`src`文件夹下添加一个`styles`文件夹。在`styles`文件夹中，我们将创建一个名为`global.css`的文件。将以下`@include`行添加到` global.css 文件中。

```
@tailwind base;@tailwind components;@tailwind utilities;
```

现在我们已经添加了一个`global.css`文件，我们可以将它作为导入添加到`gatsby-browser.js`文件中。如果您没有一个`gatsby-browser.js`文件，那么创建一个并添加下面一行。

```
import './src/styles/global.css'
```

# 开始使用 Tailwindcss

现在我们已经在 Gatsby 站点中配置了 Tailwind，我们现在可以运行`gatsby develop`或`gatsby build`来开始在我们的项目中使用 Tailwindcss。

# 结论

Tailwind 和 Gatsby 都使得集成到其他框架中变得非常容易。Tailwind 3.0 和更高版本的另一个好处是它只添加了你的站点需要的 CSS。以前版本的 Tailwind 包含了所有的 CSS 组件，但是当前版本是非常轻量级的。

[TailwindCSS 盖茨比集成指令](https://tailwindcss.com/docs/guides/gatsby)

[盖茨比 TailwindCSS 指令](https://www.gatsbyjs.com/docs/how-to/styling/tailwind-css/)

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***