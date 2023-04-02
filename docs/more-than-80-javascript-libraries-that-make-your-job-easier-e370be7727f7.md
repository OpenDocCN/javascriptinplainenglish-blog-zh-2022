# 80 多个 JavaScript 库，让您的工作更轻松

> 原文：<https://javascript.plainenglish.io/more-than-80-javascript-libraries-that-make-your-job-easier-e370be7727f7?source=collection_archive---------3----------------------->

![](img/0fc64e41dcc3c162773290459c5a5c3f.png)

Photo by [Jez Timms](https://unsplash.com/@jeztimms?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/library?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

这是一篇“为我而记”的文章。在本文中，我添加了一个有用的 JavaScript 库列表，它将节省我们的时间，让我们的生活变得更加轻松。因为在本文中我们有许多库，所以我按照用例将它们分开。我希望这将有助于更容易阅读。

因为这可能是一篇很长的文章，所以我做了一个目录:

```
[Date Time](#6f3c)
[String and number](#6e7b)
[Storage](#b3b9)
[API](#1916)
[Routing](#3e09)
[Editor](#3b6e)
[Reactive programming](#9dd2)
[Functional programming](#414b)
[Animation](#2ae9)
[Other libraries](#68c1)
```

# 日期时间

![](img/57d6a8659dfbed93d84fe07bed7eedf9.png)

Photo by [alexandru vicol](https://unsplash.com/@alex_vicol?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/clock?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

从前端到后端，日期和时间是许多项目不可或缺的。这就是为什么我们有许多 JavaScript 库来支持我们流畅地处理日期和时间。这里有一些我认为会对你有帮助的库:

**关于日期和时间的常用库:**

*   [瞬间](https://github.com/moment/moment):我想这个图书馆已经无需多言了。是我很多项目的好伙伴。
*   [日期](https://github.com/MatthewMueller/date):你喜欢用字符串处理日期和时间(“10 分钟后”、“两个月后”…)。我认为约会会是你的好朋友。
*   dayjs :又一个很棒的日期时间库，它有一个很大程度上兼容 Moment.js 的 API，大小只有 2kb。
*   [moment-timezone](https://github.com/moment/moment-timezone) :如果你喜欢 moment，并且在一个需要使用多个时区的项目中需要它，那么 **moment-timezone** 将是一个不错的选择。
*   [fecha](https://github.com/taylorhakes/fecha) :如果你喜欢处理数据，并且你需要一个好的工具来格式化数据以友好的输出。fetcha 会支持你的。
*   [date-fns](https://github.com/date-fns/date-fns) :与 **fetcha** 相同，给我们许多助手，支持我们处理多个日期时间数据。
*   ms.js :它是为需要毫秒级工作的开发人员设计的。来自 Vercel 的有用的库。

**时间前库和倒计时库:**

*   这是一个适合我的老朋友 jquery 的库。很有帮助，也很好用。
*   timeago.js :非常小(2kb)的库——time ago。

# 字符串和数字

![](img/e9d6e6ff0b20a60ac530c221fb49d723.png)

Photo by [Waldemar Brandt](https://unsplash.com/@waldemarbrandt67w?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/word-and-number?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

上面我们已经和你分享了一些支持日期和时间的库。除了日期和时间，我们通常还处理字符串和数字。这就是为什么在这一部分，我将与您分享支持处理字符串和数字的库:

**字符串:**

*   [何](https://github.com/mathiasbynens/he):也称为“HTML 实体”，是一个健壮的工具，面向那些想要使用 HTML 和字符串(编码器、解码器……)的开发者
*   [下划线](https://github.com/esamattis/underscore.string):我想很多人都知道**下划线. js** ，这是对该库的一个扩展，以支持处理字符串。
*   [string.js](https://github.com/jprichardson/string.js) :这个库的名字几乎告诉了我们关于它的一切。一个轻量级的(< 5kb)库，当我们使用 string 时，它可以帮助我们解决问题。
*   [voca](https://github.com/panzerdp/voca) :一个操纵字符串的 JavaScript 库，非常好用。
*   [sprintf.js](https://github.com/alexei/sprintf.js) :在其他编程语言中，我们有函数 sprintf 来 sprint 一个带格式的字符串。如果你想在 JavaScript 中应用类似的东西，我认为这个库可以帮助你。

**路径字符串:**

*   [query-string](https://github.com/sindresorhus/query-string) :一个帮助我们解析和字符串化 URL 字符串的库。
*   URI.js :一个支持 URIs 的旧 JavaScript 库。也许我们不再需要那个图书馆了，但是我仍然建议你把它作为一个选择。
*   [url-pattern](https://github.com/snd/url-pattern) :如果你不想花太多时间在 url 的正则表达式字符串匹配模式上，我认为你可以考虑使用这个库。

**编号:**

*   一个很好的用于格式化和操作数字的 JavaScript 库。
*   [chance.js](https://github.com/chancejs/chancejs) :如果你需要一个有用的随机生成器助手，可以试试这个库，它为我们提供了很多生成数据的方法。

# `Storage`

![](img/e3fdc7151b81eeff7104280b93335cf4.png)

Photo by [Shane](https://unsplash.com/@theyshane?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/storage?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我们将在每个项目中处理的事情之一是存储数据。除了 API，我们还使用 cookie、localStorage、sessionStorage 和 JavaScript 存储数据。我们必须支持它:

*   [store.js](https://github.com/marcuswestin/store.js) :很多网站都在用的好库，简单易用，支持多种存储。
*   js-cookie :一个简单、轻量级的库，支持你处理 cookie。
*   [cookies.js](https://github.com/ScottHamper/Cookies) :又一个支持我们使用 cookies 的库，简单易用，非常小(1.2kb)。
*   [basket.js](https://github.com/addyosmani/basket.js) :缓存和加载 localStorage 的有用脚本。
*   basil.js :一个很好的库，它帮助我们处理许多存储(cookie、localStorage、session storage……)和统一的 API 来处理它们。
*   [local feed](https://github.com/localForage/localForage):Github 上有很多明星的牛逼库。这个库将帮助我们使用本地存储和异步存储(IndexedDB 或 WebSQL)。
*   [db.js](https://github.com/aaronpowell/db.js/) :如果你只需要使用 IndexedDB，而你需要一个能让你使用 IndexedDB 更容易的库，db.js 是一个不错的选择。
*   [跨域存储](https://github.com/zendesk/cross-storage):我认为这个库对于需要使用跨域本地存储的开发者来说是个好东西。

# `API`

![](img/49bdbaae42b4b5749aa29f4bb3f3cdf0.png)

Photo by [Alessandro La Becca](https://unsplash.com/@alessandrolabecca?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/boad?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

单页应用程序(SPAs)已经成为许多现代网站的流行架构。在那个网站中，调用 API 与服务器通信是一件必须的事情。目前，我们可以很容易地用浏览器的默认工具进行调用，但我们有许多库来支持我们的这项工作。这就是为什么我要向您展示一些使用 API 的好库。当然，这些不仅仅是针对 spa 的，我们可以在很多地方使用它们，从正常的网站到服务器端。

*   Axios :最适合这项工作的 API 库之一。这是一个很棒的图书馆，不需要多介绍了。(Btw:我有一篇关于[上 **Axios** 的文章在这里](https://blog.sangnguyen.dev/handle-refresh-token-with-axios-1e0f45e9afa))。
*   来自 Vercel 的又一个令人敬畏的库。如果你正在使用 React 并且需要一个支持数据获取的钩子。让我们试试 **swr** 。
*   [坏蛋](https://github.com/elbywan/wretch):就像我上面说的，目前浏览器给了我们很多使用 API 的好工具，fetch 就是其中之一。如果你喜欢用 fetch 工作，但仍然需要一个助手，你用 fetch 更容易。我认为你可以尝试使用**无名小卒**，一个很小的(~3kb)有助于 fetch 的包装器。
*   瓶颈:我想当你看到这个库的名字时，你就能猜到它的主要特点是什么。这是一个帮助你处理 API 极限率问题的库。
*   [optic](https://github.com/opticdev/optic) :如果你想尝试一个支持设计、文档和测试 API 的库，看看 **optic** 。
*   [jquery.rest](https://github.com/jpillora/jquery.rest) :又一个旧库，帮助您使用 jquery 和 REST APIs(使它们更容易使用)。我知道我有许多旧项目需要维护，这个库是一个完美的建议。

# 按指定路线发送

![](img/7b0e6a066eca5a940e617d465716117e.png)

Photo by [Javier Allegue Barros](https://unsplash.com/@soymeraki?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/route?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

目前，我们有许多前端和后端框架。几乎都支持路由。但是如果你想找一个图书馆来支持你这么做，我有一些建议:

*   [navaid](https://github.com/lukeed/navaid) :浏览器的轻量级路由器库。
*   [page.js](https://github.com/visionmedia/page.js) :针对熟悉 Express，想在客户端找到与之相同的路由器库的开发者。
*   主任:如果你想找一个支持我们客户端、服务器端 HTTP 和 CLI 的路由器库，我认为这是一个不错的选择。这个库易于使用，有许多有用的 API 可用于许多环境。
*   轻量级且易于使用，这就是我要谈论的库。

# 编者ˌ编辑

![](img/d52c9f9a7daf333604713054aabcb409.png)

Photo by [Susan Weber](https://unsplash.com/@havasuartist?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我认为这是一个“大”的部分，许多图书馆将被建议。我们有许多网站，有许多功能的编辑器。为了支持我们，创建了许多图书馆。当然，我们有很多很棒的图书馆。下面是我推荐的一些库:

*   tinymce :一个受很多网站信任的流行的富文本编辑器。易于使用许多 API 和插件。
*   [ckeditor](https://github.com/ckeditor) :当我建议 **tinymce** 的时候，我猜有人在想 ckeditor。这是一个很好的库，可以创建许多版本的编辑器，并支持许多框架。
*   [medium-editor](https://github.com/yabwe/medium-editor) :顾名思义，这个库的灵感来自于 Medium inline toolbar。如果您想要一个带有内嵌工具栏编辑器，您可以尝试一下。
*   Daft.js :来自脸书的强大库，React 的好朋友，简单的 UI，实体模型，不可变 js ，易于扩展我们的特性。
*   [王牌](https://github.com/ajaxorg/ace):被称为 Ajax.org cloud 9 的 Aols 编辑。对于那些想做代码编辑器的人来说，这是一个很棒的库。ace 支持多种语言，有许多主题，以及许多其他令人敬畏的特性。
*   [CodeMirror](https://github.com/codemirror/CodeMirror) :为想做代码编辑器的开发者提供的另一个很棒的库。该库支持多种语言，并为我们提供了许多遵循流行代码编辑器的主题(子行文本、Emacs 等)。
*   [quill](https://github.com/quilljs/quill) :如果你想做一个功能强大的编辑器，给我们从基本格式到媒体、代码块等许多强大的工具， **quill** 会帮你做一个那样的编辑器。
*   一个漂亮的库，简单的用户界面，易于安装，支持许多版本的引导程序，有许多插件。
*   如果你是 markdown 的粉丝或者仅仅是一个 make-friendly 编辑器，试试 simplemde 。开发人员设置起来很简单，编写人员使用 Markdown 编写一些东西也很简单。
*   [笔](https://github.com/sofish/pen):关于 Markdown 的另一个库。如果您不熟悉 Markdown 语法，但希望得到 Markdown 格式的输出，可以试试这个。
*   [jsoneditor](https://github.com/josdejong/jsoneditor) :简单的 JSON 编辑器，为用户提供了许多查看、编辑、格式化和验证 JSON 的工具。
*   [wysihtml5](https://github.com/tiff/wysihtml5) ， [bootstrap-wysihtml5](https://github.com/jhollingworth/bootstrap-wysihtml5) ， [raptor-editor](https://github.com/PANmedia/raptor-editor) ， [popline](https://github.com/kenshin54/popline) :有一些老的库来构建 wysiwys，它们与 jQuery 和 bootstrap 配合得很好。它们是旧版本的库，但只是推荐给需要用这个旧版本库维护项目的开发人员。

# `Reactive programming`

![](img/8e0f376af150cead78bf9431ca30ae7f.png)

Photo by [T K](https://unsplash.com/@realaxer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pipeline?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在我们的行业中，我们有许多关于数据流的问题或工作需要处理。有人称之为“反应式编程”。老实说，我还没做过更多的工作。但是我刚刚给你推荐了一些图书馆。

*   [RxJS](https://github.com/reactivex/rxjs) :来自[react vex](https://reactivex.io/)的反应式编程的著名 JavaScript 库之一。很多人在开始反应式编程的时候都会选择 **RxJS** 。我认为这个图书馆对每个人来说都是不错的选择。
*   [cyclejs](https://github.com/cyclejs/cyclejs) :一个功能性和反应性的框架，有很多专门的包。我认为这将有助于我们处理数据流和其他相关的东西。
*   bacon.js :一个函数式反应式编程，通过许多有用的工具，帮助我们使事件处理流程变得更加清晰。也支持并使用 TypeScript 编写。
*   most :对于想从事反应式编程的开发人员来说，这是一个很好的工具包。它将帮助您更容易地操作您的数据或事件流。
*   高地:处理数据流的人的好朋友。使用这个库，您可以轻松地管理同步和异步代码。

# `Functional programming`

![](img/6689f9cdf23ab552f6b3a67f1d8619ae.png)

Photo by [Austrian National Library](https://unsplash.com/@austriannationallibrary?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/factory-line?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如果你是那些喜欢玩函数和管道的程序员，我有一些你会喜欢的库。

*   [下划线](https://github.com/jashkenas/underscore):JavaScript 的实用库。它为我们提供了许多使用数组、对象、集合的方法，以及许多有用的特性。
*   [lodash](https://github.com/lodash/lodash) :处理数组、数字、对象的最流行的库之一，它通过提供清晰的工作流程和工作流程管道使我们的工作变得更容易。
*   [Sugar](https://github.com/andrewplummer/Sugar) :你熟悉 JavaScript 中默认类型的 API(Number，Array，Object，Date…)，你可以接受，但仍然需要对这些类型的一些支持。让我们试试糖。
*   [lazy . js](https://github.com/dtao/lazy.js):JavaScript 的功能实用库，类似于下划线和 Lodash，性能更好。此外，权衡的东西。
*   rambda :一个轻量级的库，以一种简单的方式将你带入函数式编程的世界。

# `Animation`

![](img/80a8f71aabeab2db530d0b2d61f17db7.png)

Photo by [Tetiana SHYSHKINA](https://unsplash.com/@shyshkina?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/paint-draw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

上面我已经建议了许多存储库、数据类型库、反应式编程库、编辑器库。但是也许我已经忘记了 JavaScript 的一个“重要部分”。这就是动画，JavaScript 早期的主要特性之一。我们有许多令人惊叹的库，帮助用户创造令人惊叹的体验。这里有一些我想与你分享的图书馆:

*   [animate.css](https://github.com/animate-css/animate.css) :顾名思义，这个库是最好的动画库之一。如果你想用简单的方式制作一部又酷又好玩的动画，为什么不试试呢？
*   [impress.js](https://github.com/impress/impress.js) :如果你想找一个帮你玩 CSS3 变换和转场的朋友，打电话 **impress.js** 。
*   [动漫](https://github.com/juliangarnier/anime/):对于想制作让用户惊喜的动画的开发者来说，试试这个库吧:它是轻量级的，为你提供了强大的 API。
*   正如我在这个图书馆的 Github 上读到的，许多大公司都在用它来做他们的网站。我认为你可以用这个库制作一些很酷的动画。
*   [GSAP](https://github.com/greensock/GSAP) :一个健壮的 JavaScript 工具集，面向想要构建高性能动画的开发者。它可以处理很多东西，从 CSS，SVG，canvas 到流行的框架，比如 React，Vue 等等。
*   [dynamics.js](https://github.com/michaelvillar/dynamics.js) :如果你喜欢创作基于物理的动画，我想这个库可以支持你。
*   jquery.transit :对于使用 jquery 的开发人员来说，如果他们想找到一个库来帮助他们顺利地使用 CSS3 转换和过渡，可以试试这个库。
*   [move.js](https://github.com/visionmedia/move.js) :如果需要制作流程清晰、脚本清晰的动画，可以试试这个库。 **move.js** 是一个轻量级的库，有许多 API 支持你。
*   [particles.js](https://github.com/VincentGarreau/particles.js) :想玩粒子？试试这个。这是一个轻量级的库，我认为它可以帮助你做到这一点。
*   [tsparticles](https://github.com/matteobruni/tsparticles) :另一个支持我们玩粒子但是使用 TypeScript 的库。这个库是轻量级的，兼容很多框架(React、Angular、Vue、jQuery……)。
*   [smoothState.js](https://github.com/miguel-perez/smoothState.js) :需要一个库来用 jQuery 进行平滑的页面过渡？试试看。
*   一个老库，支持你用 jQuery 制作一些有趣的文本效果。
*   [bounce.js](https://github.com/tictail/bounce.js) :又一个老库，帮助我们更容易地处理`scale`、`rotate`、`translate`和`skew`。

# 其他图书馆

![](img/ade07e719e87923771f42ea62d5ae54c.png)

Photo by [Etienne Girardet](https://unsplash.com/@etiennegirardet?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/factory-building?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

除了我上面提到的 JavaScript 库之外，还有一些用于其他任务的其他库。希望其中一些对你有帮助。

*   **颜色:** [TinyColor](https://github.com/bgrins/TinyColor) ， [randomColor](https://github.com/davidmerfield/randomColor) ， [chroma.js](https://github.com/gka/chroma.js) ， [color](https://github.com/Qix-/color) ， [colors](https://github.com/mrmrs/colors) 。
*   **安全数据:** [DOMPurify](https://github.com/cure53/DOMPurify) ， [js-xss](https://github.com/leizongmin/js-xss) 。
*   **显示调试日志:** [日志](https://github.com/adamschwartz/log)，[日志级别](https://github.com/pimterry/loglevel)。
*   **CSV&PDF:**[papa parse](https://github.com/mholt/PapaParse)， [jsPD](https://github.com/parallax/jsPDF) ， [pdf.js](https://github.com/mozilla/pdf.js) 。
*   **翻译:** [i18next](https://github.com/i18next/i18next) ， [babelfish](https://github.com/nodeca/babelfish/) ， [polyglot.js](https://github.com/airbnb/polyglot.js) 。

# 最后的想法

JavaScript 是最流行的编程语言之一，每天都有一个很棒的社区为它做出贡献。这就是为什么我们有许多令人惊叹的库、工具和框架。它真的节省了我们很多时间和精力，让我们的生活更轻松。

我希望这篇文章对你有帮助。感谢开发人员为这些令人惊叹的库做出了贡献。

感谢阅读！

![](img/db0e8eca2ecfd2110e07b692633054ed.png)

Photo by [Josue Michel](https://unsplash.com/@josuemichelphotography?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

通过 [Linkedin](https://www.linkedin.com/in/thaisangnguyen3894/) 或 [Twitter](https://twitter.com/tasyit) 联系我。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*****[***免费每周简讯***](http://newsletter.plainenglish.io/) ***。*** *在我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***中获取独家写作机会和建议。******