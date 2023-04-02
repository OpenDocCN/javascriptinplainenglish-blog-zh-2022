# 使用 Webpack 的模块联邦和 create-react-app 的微前端

> 原文：<https://javascript.plainenglish.io/micro-frontends-using-webpacks-module-federation-with-create-react-app-f6a890600bae?source=collection_archive---------0----------------------->

![](img/4761f2addf03ec4723770c109644483f.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

模块联合使我们能够使用多个独立的构建来形成一个应用程序。

它是在 Webpack 5 中引入的，它确实是前端开发领域的游戏改变者。至少，它支持在同一产品的不同前端之间共享**组件**，例如管理面板、用户网站。但不仅如此，它使我们能够**将前端嵌入到其他前端中**，让我们能够拥有独立的库栈、不同的代码风格、结构等等。

官方文件说得好:

> **用例**
> 
> **每页独立构建**
> 
> 单页应用程序的每一页都从单独版本的容器版本中公开。应用程序外壳也是一个单独的构建，将所有页面作为远程模块引用。这样，每个页面都可以单独部署。当更新路由或添加新路由时，部署应用程序外壳。应用程序外壳将常用的库定义为共享模块，以避免在页面构建中重复使用它们。
> 
> **组件库作为容器**
> 
> 许多应用程序共享一个公共的组件库，该组件库可以构建为一个容器，每个组件都是公开的。每个应用程序都使用组件库容器中的组件。对组件库的更改可以单独部署，而无需重新部署所有应用程序。应用程序自动使用组件库的最新版本。

模块联合给了我们一个真正无痛的体验，将你的代码分布在不同的包中，并且配置的数量是最小的。这使得您的代码在不同的团队之间适应性更强，更易于维护。

# 让我们构建一个示例应用程序

我们将构建一个应用程序，它由三个不同的模块组成:

*   **库** —包含共享组件
*   **app2** —一个独立的应用程序，它使用组件，也可以在其他地方使用(我们将在 app1 中使用它)
*   **app1** —一个使用组件的容器应用，也包括 app2

我们的目标是使用 create-react-app，因为您可能已经在所有 react 项目中使用它了。我们希望模块联合能够补充我们已经很好的设置。当然，我们不希望取消 create-react-app 配置。

由于我们将添加一些 webpack 插件，我们也需要 **craco** 。Craco 是 Create React App 配置覆盖，一个简单易懂的配置层。详见[https://github.com/dilanx/craco](https://github.com/dilanx/craco.)。

有两个 webpack 插件**可以实现这一点:**

*   `craco-mf`**([https://github.com/bfaulk96/craco-mf](https://github.com/bfaulk96/craco-mf))**

**它使我们能够在我们的 CRA 应用程序中使用模块联合。**

*   **`@cloudbeds/webpack-module-federation-types-plugin`([https://github . com/cloudbeds/web pack-module-Federation-types-plugin](https://github.com/cloudbeds/webpack-module-federation-types-plugin))**

**为我们提供了类型安全的开发——这意味着我们的应用程序不会充满 ts 忽略，我们有一个自动系统来在应用程序之间共享类型。这对于任何现实世界的开发场景都是必要的。**

## ****配置****

**涉及的配置非常少。但是，每个模块中都有两个重要的文件:**

*   **`modulefedration.config.js`**
*   **`craco.config.js`**

**`craco.config.js`将成为所有套件的标准配置:**

```
const { join } = require("path");
const cracoModuleFederationPlugin = require("craco-mf");
const { ModuleFederationTypesPlugin } = require( '@cloudbeds/webpack-module-federation-types-plugin' );

module.exports = {
  webpack: {
    plugins: {
      add: [
        new ModuleFederationTypesPlugin({
          downloadTypesWhenIdleIntervalInSeconds: 1,
        }),
      ]
    },
    configure: (webpackConfig) => {
      webpackConfig.devServer = { static: {} };
      webpackConfig.devServer.static.directory = join(process.cwd(), "public");
      return webpackConfig;
    },
  },
  plugins: [
    {
      plugin: cracoModuleFederationPlugin,
    },
  ],
};
```

**在`modulefederation.config.js`中，我们将配置哪些包在不同的应用程序之间共享，哪些组件向其他应用程序公开，以及我们希望在我们的应用程序中访问哪些其他应用程序以及它们驻留在哪里。**

**对于**库**应用程序，我们将使用这个:**

```
module.exports = {
  name: "library",
  exposes: {
    "./NameContextProvider": "./src/components/NameContextProvider.ts",
    "./Button": "./src/components/Button",
    "./Logo": "./src/components/Logo",
  },
  filename: "remoteEntry.js",
  shared: {
    react: {
      singleton: true,
      requiredVersion: deps["react"],
    },
    "react-dom": {
      singleton: true,
      requiredVersion: deps["react-dom"],
    },
  },
};
```

**配置告诉我们，我们将与其他两个应用程序共享一个上下文、一个按钮组件和一个徽标组件。它还告诉我们，我们将在三个模块之间共享`react`和`react-dom`。**

**对于**应用 2** ，我们将使用这个:**

```
module.exports = {
  name: "app2",
  exposes: {
    './App2Index': './src/Homepage',
  },
  filename: "remoteEntry.js",
  remotes: {
    library: `library@http://localhost:3003/remoteEntry.js`,
  },
  shared: {
    react: {
      singleton: true,
      requiredVersion: deps["react"],
    },
    "react-dom": {
      singleton: true,
      requiredVersion: deps["react-dom"],
    },
  },
};
```

**这个配置告诉我们，我们将向其他应用程序公开 app2 的主页(我们将在 app1 中使用它)，并且我们将在这个应用程序中使用 library remote。这将使我们能够使用按钮和标志。**

**对于**应用 1** ，我们将使用以下内容:**

```
module.exports = {
  name: "app1",
  exposes: {
  },
  remotes: {
    app2: `app2@http://localhost:3002/remoteEntry.js`,
    library: `library@http://localhost:3003/remoteEntry.js`,
  },
  filename: "remoteEntry.js",
  shared: {
    ...deps,
    react: {
      singleton: true,
      requiredVersion: deps["react"],
    },
    "react-dom": {
      singleton: true,
      requiredVersion: deps["react-dom"],
    },
  },
};
```

**这个配置使我们能够使用库组件和 app2。**

**本质上，这就是我们需要的所有配置。这个设置的另一个特殊之处是使用路由。如果我们将 app2 作为独立的应用程序使用，我们将需要自己的路由包装器(例如来自 **react-router-dom** 的 **BrowserRouter** )，但是如果我们将 app2 嵌入到 app1 中，我们将使用来自 app1 的路由包装器。**

## **库模块**

**我们将跳过如何创建从库中暴露的按钮和徽标的部分。这都是标准反应。**

**我们还将公开一个简单的上下文:**

```
import React from "react";

export default React.createContext({
  name: "Mr.Noname" as string,
  setName: (name: string) => {},
});
```

**我们将向其他两个应用程序共享一个上下文、一个按钮组件和一个徽标组件。**

## **App2 模块**

**好玩的部分从 **app2** 开始！App2 可以作为一个独立的应用程序运行，也可以包含在另一个应用程序中。让我们看看指数成分:**

**`App.tsx` **:****

```
import NameContextProvider from "library/NameContextProvider";
import { useState } from "react";
import { BrowserRouter } from "react-router-dom";
import Homepage from "./Homepage";

function App2() {
  const [name, setName] = useState("Mojca");

  return (
    <BrowserRouter>
      <NameContextProvider.Provider value={{ name, setName }}>
        <Homepage />
      </NameContextProvider.Provider>
    </BrowserRouter>
  );
}

export default App2;
```

**请注意，我们在这里使用了自己的路由包装器，我们还使用了自己的提供者，这就是为什么我们没有将这个组件公开给 app1，而是公开给下面的 homepage 组件。App1 将有自己的名称提供者，当我们将 app2 嵌入 app1 时，上下文将被共享。神奇！**

**`Homepage.tsx` **:****

```
import Button from "library/Button";

import NameContextProvider from "library/NameContextProvider";
import React from "react";
import { Route, Routes } from "react-router-dom";

function Homepage() {
  const ctx = React.useContext(NameContextProvider);

  return (
    <Routes>
      <Route
        path="/"
        element={
          <div>
            <div style={{ marginBottom: 20 }}>
              Hello again {ctx.name}. This is app2\. The button &amp; context
              used is from components app.
            </div>
            <div>
              <Button
                text="Change name from app2"
                onClick={() => ctx.setName("Jozica")}
              />
            </div>
          </div>
        }
        index
      />
    </Routes>
  );
}

export default Homepage;
```

## **App1**

**App1 是容器应用程序，它将使我们的整个项目变得生动起来。让我们看看指数成分:**

**`App.tsx` **:****

```
import "./App.css";

import App2 from "app2/App2Index";

import { BrowserRouter, Navigate, Route, Routes } from "react-router-dom";
import Homepage from "./Homepage";

const app2RoutingPrefix = "app2";

function App1() {
  return (
    <div className="App">
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Homepage />}>
            <Route index element={<Navigate to={`/${app2RoutingPrefix}`} />} />
            <Route path={`/${app2RoutingPrefix}/*`} element={<App2 />} />
          </Route>
        </Routes>
      </BrowserRouter>
    </div>
  );
}

export default App1;
```

**它包含所有主要路由，并包括 app2。**

**`Homepage.tsx` **:****

```
import React, { useState } from "react";
import "./App.css";

import Logo from "library/Logo";
import NameContextProvider from "library/NameContextProvider";

import Button from "library/Button";
import { Outlet } from "react-router-dom";

function Homepage() {
  const [name, setName] = useState("Mojca");

  return (
    <div>
      <NameContextProvider.Provider value={{ name, setName }}>
        <React.Suspense fallback="loading">
          <div style={{ marginBottom: 20, marginTop: 20 }}>
            <Logo style={{ width: 90 }} />
          </div>
          <div style={{ marginBottom: 20 }}>
            Hello {name}. This is app1 - container app. The button &amp; context
            used is from the components app.
          </div>
          <div style={{ marginBottom: 60 }}>
            <Button
              text="Change name from app1"
              onClick={() => setName("Lojza")}
            />
          </div>
          <Outlet />
        </React.Suspense>
      </NameContextProvider.Provider>
    </div>
  );
}

export default Homepage;
```

**在主页组件中，我们提供了上下文，使用了一些共享库，并为子路由提供了一个出口——app2 是这些子路由中的一个，它将在其位置上呈现。**

**这就是我们所需要的！**

## ****开发中的运行****

**我们有两个选择:**

*   **我们可以使用 **lerna，**它将为我们在每个包中运行`yarn run start`**
*   **每个应用程序也可以通过在各自的 repos 中运行`yarn run start` 来单独运行**

## ****生产用建筑****

**如果我们要将应用程序部署到 S3，我们会将每个模块分别部署到其各自的 S3 存储桶中。**

**唯一需要的配置是在每个包的`modulefederation.config.js`文件中使用正确的远程 URL，这需要指向 S3 URL 而不是本地主机 URL。**

## **完整源代码**

**本例的完整源代码也可以在 github 上的[https://github . com/xtr inch/create-react-app-module-Federation-example](https://github.com/xtrinch/create-react-app-module-federation-example)下找到**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****