# 如何用 Prisma ORM 编写高效的单元测试

> 原文：<https://javascript.plainenglish.io/how-to-write-efficient-unit-tests-with-prisma-orm-e9d8fdf43f5f?source=collection_archive---------5----------------------->

## Express & Prisma 的一个例子

在我的全栈开发生涯中，我尝试了很多 ORM、ODM 和查询构建器。有些太棒了，而有些仍然让我做噩梦(我们看到你[](https://sequelize.org/)*)。*

*![](img/daec96a3512ba923e78ebc3cd9bef10a.png)*

*Photo by [Roman Mager](https://unsplash.com/fr/@roman_lazygeek) on [Unsplash](https://unsplash.com/fr/s/photos/test)*

# *初速电流状态*

*在这些神奇的工具中，有 [Prisma](https://www.prisma.io/) 。它工作完美，有一个伟大的 DX，文件，等等。我在使用它的时候遇到了一个问题，单元测试。*

*虽然他们有一个关于单元测试的文档页面，有一个很好的介绍，但是他们嘲笑的方法并不令人满意。*

*[](https://www.prisma.io/docs/guides/testing/unit-testing) [## 使用 Prisma 进行单元测试

### 将 Jest 添加到您的项目 Prisma 使用 TypeScript，Jest 可以在软件包的帮助下设置为使用 TypeScript…

www.prisma.io](https://www.prisma.io/docs/guides/testing/unit-testing) 

最好的情况是，这允许您一个接一个地模拟您认为将被调用的请求的响应。我认为这是低效的，原因如下:

*   每次测试都需要太多的设置。
*   在您定义的模拟中，信任度非常低，因为您不确定 Prisma 是否会返回相同的数据。
*   通过自己定义这些模拟，您可以远离测试您的应用程序行为，而更接近测试实现细节。
*   有了 Prisma 的新版本，你有可能看到你的测试被淘汰。

[](https://kentcdodds.com/blog/testing-implementation-details) [## 测试实施细节

### 回到我使用 enzyme 的时候(就像当时的其他人一样)，我小心翼翼地绕开 enzyme 中的某些 API。我…

kentcdodds.com](https://kentcdodds.com/blog/testing-implementation-details) 

让我们看看我们要测试什么应用程序，要写哪些测试，然后定义如何写单元测试。

# 应用程序结构

我的后端应用程序通常分为几层。如果我们以一个基本的 ExpressJS 应用程序为例，它至少有 3 层:模块、控制器和服务。

每组功能被分成一个专用的**模块**，它处理路由、验证，并将请求传递给控制器。

**控制器**是发现业务逻辑的地方，并且经常使用服务。

一个**服务**提供向数据库发出请求的高级功能。这就是我使用 ORM 比如 **Prisma** 的地方。

# 应该测试什么

当我在后端应用程序上工作时，我通常有两种主要的测试类型(根据上下文，还有更多类型！).它们是**单元**和**端到端**测试。

[](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing) [## 软件测试的不同类型

### 区分手动测试和自动测试是很重要的。手动测试由…亲自完成

www.atlassian.com](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing) 

我尽可能避免编写 e2e 测试，因为它们有一些限制，比如速度慢、成本高、反馈晚。我通常为中间件等低级功能编写**单元**测试。

另一方面，我不会完全孤立地测试我的服务或控制器。在那些情况下，我觉得它没有给我足够的时间来写测试。相反，我想从整体上测试我的端点行为。

为此，我使用我的后端应用程序的**测试版本**来编写我的测试。像 Prisma 这样的外部依赖被模拟(以一种有效的方式),这允许我使用像 [SuperTest](https://www.npmjs.com/package/supertest) 这样的工具单独模拟查询。

在这种情况下，我为大多数用例编写单元测试。它包括验证(如参数)、授权(确保您有正确的访问权限)，但我也使用 Prisma 的模拟版本验证我收到了正确的响应。根据我的应用程序，甚至有更多的用例。

最后，我还要编写 e2e 测试，以确保在真实环境中，我的成功响应和与数据库相关的错误是意料之中的。

这些测试可能与我的单元测试部分重叠，但是这次使用的是真实的数据库。它给了我单元测试的快速和早期的反馈，同时具有 e2e 测试的高可信度。

# 如何编写那些测试

在下面的例子中，我希望你理解测试的基础。这包括 Jest，它被用作示例的一部分。

[](/testing-with-node-js-understand-and-choose-the-right-tools-98c0a33fb59a) [## 用 Node.js 测试:理解并选择正确的工具

### 用 Node.js 测试需要哪些工具，根据自己的目的选择哪些？

javascript.plainenglish.io](/testing-with-node-js-understand-and-choose-the-right-tools-98c0a33fb59a) 

## 中间件

中间件不需要特殊的测试环境，它们可以像其他功能一样被考虑。

唯一的问题是，他们有一个明确的格式。对于 Express，它们必须返回一个接受**请求**、**响应**和**下一个函数**的函数。让我们来看看下面的片段:

Validator 接受一个函数，该函数通过基于接收到的请求返回一个布尔值来确定请求是否有效。它返回一个中间件，如果接收到的请求被确定为无效，该中间件将抛出一个错误。

有了 Jest，这个中间件可以很容易地通过用不同的参数调用它来测试，并验证 next 是用正确的元素调用的。

## 端点(单位)

我已经解释过我使用 [SuperTest](https://www.npmjs.com/package/supertest) 作为我的端点。我还谈到了使用我的后端应用程序的测试版本。更准确地说，我有几个助手函数，专门用于在测试期间引导我的后端和管理模拟数据。

下面的代码片段是单元测试的一个很好的例子。我们演示了如何测试一个致力于创建文章的端点。

我们使用助手来引导我们的应用程序，生成用例所需的令牌，并使用 SuperTest 发送请求。

## 和 Prisma 一起嘲笑

但是我们仍然没有解决 Prisma 带来的问题。在上面的片段中，看起来没有什么是嘲笑。

如果我们想编写不依赖于数据库或[大量模仿](https://www.prisma.io/docs/guides/testing/unit-testing)的测试，有一个简单的解决方案:使用 Prisma 的内存实现。

介绍[普里莫克](https://www.npmjs.com/package/prismock)。*声明:我的确是它的创造者*。

[](https://www.npmjs.com/package/prismock) [## 普里莫克

### 这是对 PrismaClient 的嘲弄。它完美地模拟了 Prisma 的 API，并将所有内容存储在内存中，以便快速、隔离地…

www.npmjs.com](https://www.npmjs.com/package/prismock) 

由于没有令人满意的解决方案来有效地用 Prisma 编写单元测试，我决定编写自己的解决方案。

它实际上会读取你的`schema.prisma`，并基于它生成模型。它完美地模拟了 Prisma 的 API，并将所有内容存储在内存中，以便进行快速、隔离和可重试的单元测试。

还记得我如何使用助手来构建我的后端应用程序的测试版本吗？

在生产中，我使用真正的 **PrismaClient** 构建我的应用程序，然后进行引导。在我的测试中，我使用[依赖注入](https://www.npmjs.com/package/prismock#dependency-injection)替换 **PrismaClient** 。

在上面的代码片段中，它是作为`ServerMock.createApp()`的一部分完成的，这使得它在我编写测试时几乎不可见。

## 端点(E2E)

在我们的文章端点和授权过程已经过测试的情况下，我们可以说，在 e2e 测试期间，在每个端点上测试认证并不是强制性的。

例如，我们可以以下面的测试结束:

这个测试必须在一个不同的环境中编写，在这个环境中，我们可以访问一个种子数据库，并且我们的端点已经在一个接近生产的环境中构建和运行。

# 结论

在这种情况下，我们应该用单元测试覆盖我们的整个代码库，给我们快速和早期的反馈，对我们的测试结果有强烈的信任。

使用 Prisma 的内存实现代替[手动模拟](https://www.prisma.io/docs/guides/testing/unit-testing)进一步增加了我们的信心。连同我们的测试策略(定义在**什么应该被测试**中)，我们也以惊人的生产力结束。

最后，我们专门为向我们的数据库发出请求的用例编写 E2E 测试。它确实与一些单元测试重叠，速度较慢，后期反馈更昂贵，但是它消除了剩余的灰色区域。

然后我们能够回答:

> 您有信心将您的应用交付生产吗？

**寻找使用 Node 创建后端应用程序的完整课程。JS？**

[](https://www.scalablebackend.com) [## 使用 NodeJS 的企业级后端开发

### 采取正确的技术选择是必要的，但还不够。实施应该是最高质量的，并且…

www.scalablebackend.com](https://www.scalablebackend.com) 

*更多内容看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****想扩大你的软件创业规模*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***