# Angular vs. Vue.js:两种 JavaScript 框架的比较

> 原文：<https://javascript.plainenglish.io/angular-vs-vue-15a8bc88de8d?source=collection_archive---------7----------------------->

## 将全功能框架与渐进式框架进行比较。

![](img/14e21828e72c496b2d619bb510442fc9.png)

Photo by [Rob Wingate](https://unsplash.com/@robwingate?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

就在几周前，我写了一篇比较 [Angular vs React](/angular-vs-react-c07cc7711423?source=your_stories_page----------------------------------------) 的文章。灵感来自于在一次面试中被问到有什么不同，却没有一个好的答案。在比较了两者之后，我对每一个都有了更好的理解。但现在，这让我开始思考 Vue.js 与 Angular 有多相似或不同。Vue.js 是另一个我只是偶尔使用的框架，但是已经开始用得更多了。我目前的工作甚至融入了一些 Vue.js，所以我想现在是更熟悉它的好时机。

因此，在今天的文章中，我们将看看 Angular 和 Vue.js 之间的一些主要差异。

# **构图差异**

要考虑的第一个区别是每个的架构。Angular 是作为一个完整的框架创建的。它是用打字稿写的，由谷歌开发和维护。Angular 本身就是一个完整的解决方案。作为一个完整的框架，框架控制着流程，这意味着当你插入你需要的代码时，Angular 决定何时调用代码。Angular 的架构是基于组件的，遵循 MVC(模型-视图-控制器)框架。Angular 之所以被认为是一个框架，是因为它为应用程序提供了强大的功能，比如结构、模板和单元测试工具。

另一方面，Vue.js 是一个渐进的框架。一个渐进的框架意味着它不是“全有或全无”。本质上，您可以将 Vue.js 插入到应用程序的各个部分，或者您可以使用它的核心库进行扩展。渐进式框架也意味着它被用作 HTML(超文本标记语言)的扩展。这个扩展意味着随着 Vue.js 模型的更新，浏览器的 HTML 也会更新。Vue.js 使用 MVVM(模型-视图-视图模型)框架模型，由尤雨溪开发，由他和活跃的核心团队成员共同维护。

Angular 和 Vue.js 的另一个区别是它是常规的还是虚拟的 DOM(文档对象模型)。Angular 使用常规 DOM，这是一个表示 HTML 和 XML 文档页面的接口，因此程序可以改变结构、样式和内容。作为一个常规的 DOM，当结构或内容改变时，HTML 标签的整个树结构被更新。如果你正在做一个小项目，这应该不是问题。但是，随着项目规模的扩大和同一页面上数据请求数量的增加，每个页面请求都要替换 HTML，性能可能会受到负面影响。这种较慢的性能可能会损害用户的体验。

Vue.js 使用虚拟 DOM，它更新的是 HTML 代码块中的特定部分，而不是整个树结构。由于这种差异，虚拟 DOM 是常规 DOM 的更快替代。为了避免更新整个树结构，虚拟 DOM 会比较之前和当前的 HTML，然后只在必要的地方进行更改。

下一个需要注意的差异是数据绑定。Angular 使用双向绑定，这意味着当模型状态改变时，UI 元素也会改变。同样，如果 UI 元素发生更改，模型状态也将发生更改。这显示了双向绑定。另一方面，Vue.js 使用单向数据绑定。这意味着当模型状态改变时，UI 元素也会更新。然而，当 UI 元素改变时，相应的模型状态不会改变。这显示了单向数据绑定。

如上所述，Angular 使用的是 MVC 框架，而 Vue.js 使用的是 MVVM 框架。MVC 框架将应用程序划分为组件，这些组件将 UI 层与应用程序逻辑层分开。这将长代码简化为多个部分，在编写多页复杂 web 应用程序时非常有用。在 MVVM 框架中，模型包含应用程序逻辑层，而视图层包含 UI 逻辑。这是“MV”部分。在“VM”部分中，视图和模型相互交互，以将数据从一个传递到另一个。这个 MVVM 为数据创建了一个双向通信，这是一个数据绑定的双向流。

# **灵活性和易用性**

当考虑易用性时，首先要考虑的是学习曲线。然而，这是另一个场景，其中一个比另一个更容易，并不意味着它只是简单。两者都有一个学习曲线，可能会有点困难，特别是对于初学者。不过，Angular 是一个功能齐全的框架，它会让你的学习曲线变得陡峭起来。另一方面，Vue.js 是一个进步的框架，这意味着比较起来更容易学习。从经验来看，刚开始尝试这两种方法时，总会有一段曲线需要去适应。不过，一旦跨过了这个门槛，学习和扩张就不会有太大的困难。所以，它们最初都是陡峭的曲线，但逐渐变得更容易理解。与 Angular 相比，Vue.js 更容易上手，尽管它还有一段曲线需要习惯。

Vue.js 和 Angular 的速度都很快，至少和以前的技术相比是这样。不过，由于 Vue.js 有一点点更大的灵活性，而且可以分段使用，因此 Vue.js 更快。这不仅仅是因为框架，还因为比较常规 DOM 和虚拟 DOM 时，虚拟 DOM 更快。说到灵活性，这也是一个值得考虑的因素。灵活性不同的主要原因是因为 Angular 有一个完整的框架结构，而 Vue.js 没有那么结构化。

在可伸缩性方面，Angular 使用模块化开发，因此更容易伸缩。它还提供了大型应用程序中代码的可重用性。另一方面，Vue.js 使用基于模板的开发，所以这损害了代码的整体可重用性，因此 Angular 更适合缩放。

在测试时，Vue.js 的指导原则更少，这使得全面测试一个应用程序更加困难。另一方面，Angular 有一个测试系统，该系统配有各种工具来分别检查代码的每一部分。

既然我们已经了解了这两者的背景和功能，那么让我们来看看它们各自的一些好处。

# **Angular 和 Vue.js 的优势**

Angular 的一个优点是双向数据绑定，允许应用程序的单一行为，这有助于最小化潜在错误的风险。虽然已经很快了，但是新的特性允许更快的复杂性，而且还有其他新特性，比如 HttpClient 启动。对于学习，Angular 提供了详细的文档，其中包含了开发人员在向同行论坛提问之前可以参考的大量信息。然而，这确实需要更多的研究。另一个优点是角度的模块化。

Vue.js 的一个优势是它非常轻量级，因为它很小，这有助于速度和灵活性。Vue.js 也有详细的文档，可以帮助缩短学习的时间。另一个优点是，即使在缩放过程中一些模板的可重用性可能很困难，但由于结构简单，其他模板可以高度可重用和可缩放，而不必花费额外的时间。Vue.js 在集成方面非常灵活，因为它既可以用于小型应用程序，也可以用于更复杂的界面。最后一个优点是，它是为 empower HTML 而构建的，优化了块处理和不同组件的使用。

有了一些优点，现在让我们来看看两者的一些缺点。

# **Angular 和 Vue.js 的缺点**

Angular 的一个缺点是语法复杂，这意味着它有一个陡峭的学习曲线。对于初学者来说，习惯语法可能需要时间，但 Angular 5 使用 TypeScript 2.4，这是最难学习的版本，尽管它仍然很难。另一个缺点是，从旧版本迁移到最新版本时会出现迁移问题。

Vue.js 的一个缺点是灵活性上的风险。这种风险是 Vue.js 在集成到一些大型项目时可能会遇到问题，因为目前还没有关于可能的解决方案的经验。另一个缺点是，相比 Angular，资源更少。尽管有关于 Vue.js 的详细文档，尽管有一个不断增长的社区，它仍然没有 Angular 那么发达，因此没有那么多现成的资源。因为社区仍在发展，并非所有的资源都被翻译成用户选择的语言，所以您可能无法访问所有可用的资源，直到它们被翻译或者直到社区为开发人员和同行帮助建立了论坛。

# **结论**

在今天的文章中，我了解了 Angular 和 Vue.js 的区别。我们看到的一些区别是框架类型，MVC 和 MVVM，组成，易用性，可伸缩性，等等。在了解了一些差异之后，我们看了两者的一些优点和缺点。

总的来说，我觉得我对 Angular 和 Vue.js 之间的区别有了更好的理解。希望你也认为这是一篇有趣的文章。下次见，干杯！

***用我的*** [***每周简讯***](https://crafty-leader-2062.ck.page/8f8bcfb181) ***免费阅读我的所有文章，谢谢！***

***想阅读介质上的所有文章？成为中等*** [***成员***](https://miketechgame.medium.com/membership) ***今天！***

*看看我最近的一些文章:*

[](https://medium.com/codex/something-i-learned-this-week-ssh-and-sftp-in-c-33958ebdca50) [## 这周我学到了一些东西:宋承宪和 C#中的 SFTP

### 管理远程文件比你想象的要容易

medium.com](https://medium.com/codex/something-i-learned-this-week-ssh-and-sftp-in-c-33958ebdca50) [](https://python.plainenglish.io/revisiting-flask-vs-fastapi-in-2022-650fb76baf08) [## 2022 年重温 Flask vs FastAPI

### 深入了解 Python 的微 web 框架

python .平原英语. io](https://python.plainenglish.io/revisiting-flask-vs-fastapi-in-2022-650fb76baf08) [](https://medium.com/codex/listing-symbolic-links-in-apache-879477ccfa0c) [## 在 Apache 中列出符号链接

### 创建网络快捷方式的简单方法。

medium.com](https://medium.com/codex/listing-symbolic-links-in-apache-879477ccfa0c) [](/angular-vs-react-c07cc7711423) [## 角度与反应

### web 开发人员的一个有保证的面试问题。

javascript.plainenglish.io](/angular-vs-react-c07cc7711423) [](https://medium.com/codex/how-to-host-your-own-docker-registry-58569f317582) [## 如何托管自己的 Docker 注册表

### 退出 Kubernetes Kubeadm，转而使用 MicroK8s 第二部分

medium.com](https://medium.com/codex/how-to-host-your-own-docker-registry-58569f317582) 

## 参考资料:

[](https://www.techmagic.co/blog/reactjs-vs-angular-vs-vuejs-what-to-choose-in-2020/) [## Angular vs React vs Vue.js:框架对比- TechMagic

### JavaScript 框架正以极快的速度发展，这意味着今天我们有频繁更新的版本…

www.techmagic.co](https://www.techmagic.co/blog/reactjs-vs-angular-vs-vuejs-what-to-choose-in-2020/) [](https://www.monocubed.com/blog/vue-vs-angular/) [## vue Vs Angular:2022 年用哪个框架最好？

### 尽管过去已经发布了大量的 JavaScript 框架，但还没有哪一个能接近神圣的三位一体…

www.monocubed.com](https://www.monocubed.com/blog/vue-vs-angular/) [](https://www.freecodecamp.org/news/angular-vs-vue-which-is-best-for-programming-in-2020/) [## angular vs . Vue——2020 年编程哪个最好？

### Angular 是 Google 先进成熟的 JavaScript 框架。它是实用和有用的，但它需要时间来建立…

www.freecodecamp.org](https://www.freecodecamp.org/news/angular-vs-vue-which-is-best-for-programming-in-2020/) [](https://www.mindinventory.com/blog/angular-vs-vue/) [## Angular Vs Vue:哪个最适合前端开发？

### Angular 与 Vue 的比较:下面是 Angular 和 Vue 之间的区别的详细指南，哪些前端 JavaScript…

www.mindinventory.com](https://www.mindinventory.com/blog/angular-vs-vue/) [](https://stackoverflow.com/questions/59834087/what-does-vuejs-mean-by-calling-themselves-progressive-framework) [## VueJS 自称渐进式框架是什么意思？

### VueJs 的官方文档所指的渐进式框架是什么？进行式的区别是什么…

stackoverflow.com](https://stackoverflow.com/questions/59834087/what-does-vuejs-mean-by-calling-themselves-progressive-framework) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*