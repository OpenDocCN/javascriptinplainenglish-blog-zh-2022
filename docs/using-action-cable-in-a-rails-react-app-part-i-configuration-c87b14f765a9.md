# 在 Rails/React 应用程序中使用 Action Cable 第一部分:配置

> 原文：<https://javascript.plainenglish.io/using-action-cable-in-a-rails-react-app-part-i-configuration-c87b14f765a9?source=collection_archive---------11----------------------->

![](img/a38ab762328af10d7fac8770ddb9199b.png)

本文的第一部分讨论了如何配置一个使用 Rails API 后端和 React 前端与 Action Cable 协同工作的应用程序

第二部分讨论在 Rails/React 应用中实际实现 Action Cable

当我在做我最近的项目，一个[琐事游戏](https://backward-jeopardy.herokuapp.com/)时，我决定离开我的舒适区，尝试一些新的东西。这将是我在熨斗学校的最后一个主要项目，我希望它是一个好项目。我发现了 Rails 的一个内置特性，Action Cable，这引起了我的兴趣。进一步的调查让我陷入了一个研究和实验的兔子洞，这比我预期的要困难得多，有时令人难以置信地沮丧，以至于我几乎放弃了，但最终非常值得，因为我最终到达了我需要的地方。如果没有其他遇到类似问题的开发人员撰写的许多其他博客帖子(大多数都在这个平台上),并且好心地与世界分享他们的解决方案，我永远也不会走到这一步。我已经决定加入我的声音，有几个原因，这些原因加起来就是一个主要原因:**我的目标不仅是给出一个循序渐进的教程，而且让行动电缆变得容易**。这是一个崇高的目标，最终将由读者来决定我是否成功。我还将包括我认为最有用的资源的链接。

那么什么是行动电缆呢？简单解释一下(因为这不是本文的重点)，Action Cable 是一种将 WebSockets 集成到 Rails 应用程序中的方法。WebSockets 是一种通信协议，在这种协议中，客户端和服务器之间的持久连接保持打开，因此信息可以自由地来回流动，这与 HTTP 协议相反，HTTP 协议只在响应请求时发送或接收信息。使用 WebSockets 的应用程序的一个经典实例是聊天应用程序。消息传递应用程序依赖于能够向用户提供实时信息，例如在线状态、输入指示器，当然还有新消息，最好不要求客户端不断发出请求(如果您好奇，可以称为轮询)

Action Cable 像所有其他 Rails 特性一样，有一个非常全面的 [Rails Guide](https://guides.rubyonrails.org/action_cable_overview.html) 。如果是这样的话，有什么困难呢？好吧，如果你一直试图在你自己的项目中实现 Action Cable，也许同样的问题把你带到了这里。那样的话，我也去过，真心希望能帮到你。如果没有，我希望你能从我要说的话中找到价值，并从这里走出来，比以前多一点见识。

我(和其他人)面临的第一个也可能是最重要的挑战是，Rails 指南假设您正在使用全栈 Rails 应用程序。这意味着实现带有独立 React 前端的 Action Cable 的官方文档很少(也就是说，没有)。如果不是遇到同样问题的人写的许多博客帖子，我的行动电缆愿望永远不会实现(我相信 [NASA](https://blogs.nasa.gov/artemis/2022/09/03/artemis-i-launch-attempt-scrubbed/) 会认同这一点)。我将列出三个主要步骤以及我在每个步骤中遇到的一些挑战，之后我将演示如何用 React 以一种简单明了的方式设置 Action Cable。

*   配置:Rails 指南并不清楚如何设置你的应用程序来使用 Action Cable。即使你用实际代码做了所有正确的事情，如果没有正确设置，它也不会工作。
*   在应用程序中实际使用 Action Cable:我发现的许多讨论在 React 中使用 Action Cable 的博客都有点过时，代码示例中包含了使用的类组件。作为一个学会使用 React 函数组件和 React 钩子的人，这意味着我必须破译所有代码并“翻译”它们。这增加了一层额外的混乱，有时使相对简单的代码看起来比实际更复杂。这将在第二部分讨论。
*   为生产/部署进行配置:为了使 Action Cable 能够在生产中工作，需要进行一些额外的配置。不幸的是，在写这篇文章的时候，自由的 Heroku 正处于垂死挣扎之中。我希望找到一个替代方案，但在此之前，我将不得不坚持使用 Heroku，这就是我将在这里报道的内容。

# 开发配置

我会尽可能地保持简短。如果你想了解更多，我会在最后链接一些资源。您要做的第一件事(实际上不一定是第一步，但可能是最基本的一步)是为您的 WebSocket 定义一个路由。将此添加到`/config/routes.rb`:

```
mount ActionCable.server => '/cable'
```

端点不一定是`/cable`，但这是传统的做法。

接下来，您必须将新创建的 Action Cable URL 添加到`/config/environments/development.rb`中。您还想禁用可能令人讨厌的安全特性(当然，只是在开发阶段！).将以下几行添加到`/config/environments/development.rb`:

```
config.action_cable.url = 'ws://localhost:3000/cable'
config.action_cable.disable_request_forgery_protection = true
```

注意`ws`前缀，而不是普通的`http`。正如我提到的，WebSockets 不使用 HTTP 协议。此外，如果您的 Rails 应用程序运行在 3000 以外的端口上，请确保在上面的代码中替换了正确的端口！接下来，如果您的前端和后端在不同的存储库中(如果它们都在一个域中，您可以跳过这一步)，您可能需要注意潜在的 CORS 问题。在 gem 文件中取消对`gem ‘rack-cors’`的注释，并在终端中运行`bundle install`。然后转到`/config/initializers/cors.rb`并取消注释(或者添加，如果还没有的话)下面的代码:

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins "*"

    resource "*",
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

部署应用程序后，您可能希望更改允许的来源，以仅包括您的前端应用程序。

这应该足以让 Action Cable 投入开发。我见过那些推荐在开发中使用 redis 服务器的人，但是我觉得没有必要。

# 生产配置

如果您将应用程序部署到 Heroku，您将需要使用 Redis 附加组件的 Heroku 数据，Redis 附加组件是另一个即将不再免费的免费附加组件😢。Heroku 关于如何设置它的文章相对简单，所以按照这里的说明[直到你创建了一个实例。一旦有了 Redis URL(可以通过`REDIS_URL`配置变量访问)，就转到`/config/cable.yml`。在这里，您应该会看到类似如下的代码:](https://devcenter.heroku.com/articles/heroku-redis)

```
development:
  adapter: async

test:
  adapter: test

production:
  adapter: redis
  url: <%= ENV.fetch("REDIS_URL") { "redis://localhost:6379/1" } %>
  channel_prefix: <your_app_name>_production
```

在`production`下，粘贴以下代码，而不是第 9 行`url:`后的内容:`<%= ENV["REDIS_URL"] %>`。请不要做我看到的一些博客帖子(包括这篇，直到我艰难地认识到我的错误)说要做的事情，即复制并粘贴实际的 Redis URL 到这个文件中。我的应用程序在正常工作几周后莫名其妙地在生产中崩溃，之后我发现 Heroku 偶尔会更改 Redis 的 URL。如果您的应用程序通过`REDIS_URL`配置变量访问 URL，这不是问题，因为配置变量将总是指向正确的 URL。如果您手动添加 URL 本身，当您的 WebSocket 突然停止工作时，您可能会发现自己疯狂地搜索无用的错误消息。

接下来，转到`/config/environments/production.rb`，在这里您会看到注释掉了下面的代码:

```
# Mount Action Cable outside main process or domain.
# config.action_cable.mount_path = nil
# config.action_cable.url = 'wss://example.com/cable'
# config.action_cable.allowed_request_origins = [ 'http://example.com', /http:\/\/example.*/ ]
```

取消所有内容的注释(当然除了第一行),并更新它，使其看起来像这样:

```
config.action_cable.mount_path = "/cable"
config.action_cable.url = "wss://<your-rails-app-domain>.com/cable"
config.action_cable.allowed_request_origins = [ 
"http://<your-rails-app-domain>.com",
/http:\/\/<your-rails-app-domain>.com.*/
]
```

Regex 位是一个附加的安全东西，不要太担心它，只要把你的后端 Rails 应用的 URL 粘贴到它应该在的地方就可以了。还要注意`'wss'`中额外的‘s ’,用于 Heroku 将使用的安全 WebSocket 协议。

## 配置 React 前端

有一些潜在的方法来设置事物的反应面。我个人更喜欢`useContext`。如果你不熟悉它是如何工作的，你可以复制并粘贴我将在这里包括的大部分代码，它应该工作得很好。

首先，您必须安装 npm actioncable 包。这就像在终端中从你的 React 应用的根目录运行`npm install actioncable --save`一样简单。(如果你的 React 应用在 Rails 应用的客户端目录中，只需从你的项目根目录运行命令并添加`--prefix client`。)

现在，在 React 应用程序的`src`目录中，创建一个名为`context`的文件夹，并在该文件夹中创建一个名为`cable.js`的文件。我将首先提供这个文件的代码，然后分解一些重要的部分:

```
import React from "react";
import ActionCable from "actioncable";

const CableContext = React.createContext();

function CableProvider({ children }) {
    const actionCableUrl = process.env.NODE_ENV === 'production' ? 'wss://<your-deployed-app-domain>.com/cable' : 'ws://localhost:3000/cable'

    const CableApp = {}
    CableApp.cable = ActionCable.createConsumer(actionCableUrl)

    return <CableContext.Provider value={CableApp}>{children}</CableContext.Provider>;
}

export { CableContext, CableProvider };
```

让我们看看这是怎么回事。我们正在创建一个名为`CableApp`的`object`，并给它一个键`cable`，它指向一个新创建的 Action Cable 消费者。这将通过使用上下文对我们的`CableProvider`组件的所有子组件(在本例中，是整个应用程序)可用。

`createConsumer()`函数将 Action Cable URL 作为参数，所以让我们看看我们的`actionCableUrl`变量。它的值是使用第 7 行上看起来有点吓人的三元表达式来赋值的。我们在这里试图解决的问题是，你的 Rails 应用在开发和生产中不会有相同的域。我见过一些克服这种情况的方法，对我来说这是最简单的。我们利用内置的环境变量`NODE_ENV`，来检查应用程序当前运行的环境，并相应地调整 URL。如果您的 React 应用程序与 Rails 应用程序位于完全不同的目录中，并且是单独部署的，这不一定行得通。在这种情况下，您必须根据您的 Rails 后端当前所在的位置手动更改链接，并将其传递给`createConsumer()`。

现在我们的`cable.js`文件已经设置好了，让我们让应用程序的其余部分访问我们的`CableContext`。导航到你的 React 应用的入口点(可能是`/src/index.js`)。默认情况下，它看起来像这样:

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

导入您的`CableProvider`:

```
import { CableProvider } from './context/cable';
```

并将其包裹在顶层组件周围，`<App />`:

```
root.render(
  <React.StrictMode>
    <CableProvider>
      <App />
    </CableProvider>
  </React.StrictMode>
);
```

整个文件应该是这样的:

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { CableProvider } from './context/cable'; 

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <CableProvider>
      <App />
    </CableProvider>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

现在我们的`CableContext`应该可以在整个应用程序中使用。

我相信我们已经完成了配置我们的应用程序来使用动作电缆，来到[第二部分](https://medium.com/@nkulik/using-action-cable-in-a-rails-react-app-part-ii-implementation-db8b1762c794)的有趣部分，实际上在我们的应用程序中使用动作电缆！

# 用于配置的资源

[](https://devcenter.heroku.com/articles/heroku-redis) [## Redis 的 Heroku 数据

### 从 2022 年 11 月 28 日开始，Redis 计划的免费 Heroku Dynos、免费 Heroku Postgres 和免费 Heroku 数据将不再…

devcenter.heroku.com](https://devcenter.heroku.com/articles/heroku-redis) [](https://medium.com/swlh/deploying-a-rails-react-app-with-actioncable-to-heroku-cb5d42f41a2a) [## 将带有 ActionCable 的 Rails/React 应用程序部署到 Heroku

### 本文假设您已经在开发环境中成功实现了 ActionCable。如果你有…

medium.com](https://medium.com/swlh/deploying-a-rails-react-app-with-actioncable-to-heroku-cb5d42f41a2a) [](https://medium.com/@the.asantiagojr/how-to-setup-actioncable-with-a-rails-api-backend-1f1807c2d908) [## 如何用 Rails API 后端设置 ActionCable

### 当我开始和我的同事一起做一个项目时，我们并没有花太多时间来决定我们想要做什么…

medium.com](https://medium.com/@the.asantiagojr/how-to-setup-actioncable-with-a-rails-api-backend-1f1807c2d908) [](https://medium.com/swlh/action-cable-react-hooks-redux-toolkit-yet-another-chat-app-with-unread-messages-feature-93f5f36d4489) [## Action Cable，React Hooks，Redux Toolkit:又一款聊天应用——带有未读消息功能

### Action Cable 是集成 WebSockets 的 Rails 方式，允许以最小的开销进行双向通信…

medium.com](https://medium.com/swlh/action-cable-react-hooks-redux-toolkit-yet-another-chat-app-with-unread-messages-feature-93f5f36d4489) 

*更多内容看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**