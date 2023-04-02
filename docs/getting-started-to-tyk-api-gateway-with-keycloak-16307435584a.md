# 使用 Keycloak 开始使用 Tyk API 网关

> 原文：<https://javascript.plainenglish.io/getting-started-to-tyk-api-gateway-with-keycloak-16307435584a?source=collection_archive---------3----------------------->

## 如何使用 Tyk Gateway(开源)保护 Node.js API，在没有来自 Keycloak 实例的 OIDC 令牌的情况下拒绝对它的访问。

![](img/fbd736e36027940e17539b819f5d0045.png)

Basic Architecture — TYK with Keycloak

# 介绍

在本文中，我们的目的是理解如何使用 [Tyk](https://tyk.io/) 来保护我们自己的 [Node.js API](https://github.com/santoshshinde2012/node-boilerplate) 。Tyk 将阻止请求，除非它们带有由 [Keycloak](https://www.keycloak.org/) 提供的 ID 令牌或有效签名的密钥。

那些不熟悉 Tyk 网关并希望了解该网关的基本特性的人可以参考我以前的文章，请参见下面的链接。

[](/getting-started-with-tyk-open-source-on-your-local-machine-6468d1c4f7b) [## 在本地机器上开始使用 Tyk API Gateway

### 用 Node.js 和 Express 创建一个简单的 API 端点，然后创建一个本地 TYK 网关(开源)。

javascript.plainenglish.io](/getting-started-with-tyk-open-source-on-your-local-machine-6468d1c4f7b) 

# 开始安装

我们将使用 docker-compose 在本地安装 TYK & Keycloak，这是最快的方法。

**步骤 1 —克隆 docker-compose 存储库**

[](https://github.com/santoshshinde2012/tyk-keycloak-demo) [## GitHub-Santosh shinde 2012/tyk-key cloak-demo:Basic demo 将 tyk gateway 开源与…

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/santoshshinde2012/tyk-keycloak-demo) 

```
git clone [https://github.com/santoshshinde2012/tyk-keycloak-demo.git](https://github.com/santoshshinde2012/tyk-keycloak-demo.git)
```

**步骤 2—更新本地机器中的主机条目**

请将以下几行添加到您的`/etc/hosts`:

```
127.0.0.1       oidc
127.0.0.1       tyk
```

![](img/09e6962fd9f18f0890d5c742ca24a1e2.png)

`/etc/hosts`

**第 3 步—转到新目录**

```
cd [tyk-keycloak-demo](https://github.com/santoshshinde2012/tyk-keycloak-demo.git)
```

**步骤 4—部署 Tyk 网关、Redis 和 Keycloak**

[https://raw . githubusercontent . com/Santosh shinde 2012/tyk-key cloak-demo/master/docker-compose . yml](https://raw.githubusercontent.com/santoshshinde2012/tyk-keycloak-demo/master/docker-compose.yml)

```
docker-compose up -dORdocker-compose up
```

![](img/22ecaf94b261dbb99c384ce8a708a57c.png)

Deploy Tyk Gateway, Redis and Keycloak

**步骤 5—测试网关& Keycloak 是否正在运行**

tyk gateway API 的 Swagger 文档可在此处获得[https://tyk.io/docs/tyk-gateway-api](https://tyk.io/docs/tyk-gateway-api/)。下一步，我们将使用 TYK 网关 API，Keycloak 用户界面，我们将使用 p [ostman](https://www.postman.com/) 客户端进行 API 调用。

```
API - http://localhost:8000/hello
METHOD - GET
```

![](img/bb680b36ec7217205213e0237138d303.png)

**Test the Gateway is running or not**

![](img/cfcaf8c8aba7a790e91ec3df2f826553.png)

**Test the Keyclaok is running or not**

**步骤 6—创建演示 Node.js 应用程序**

对于本文，我们将使用已经使用 TypeScript 和 Express 创建的 [Node.js 样板代码](https://github.com/santoshshinde2012/node-boilerplate)。

[](https://github.com/santoshshinde2012/node-boilerplate) [## GitHub-Santosh shinde 2012/Node-Boilerplate:用于微服务的节点类型脚本样板…

### 微服务的节点类型脚本样板。用 TypeScript 编写的 Node.js 应用程序的框架(带有安装说明…

github.com](https://github.com/santoshshinde2012/node-boilerplate) 

```
// clone the application
git clone [https://github.com/santoshshinde2012/node-boilerplate.git](https://github.com/santoshshinde2012/node-boilerplate.git)// change to the new directory
cd node-boilerplate// Run the application using docker-compose
docker-compose up
```

![](img/c2d7fc2750aa5418dd016b23e231b071.png)

Run the node js application

有关更多信息，请参考以下文章:

[](/skeleton-for-node-js-apps-written-in-typescript-444fa1695b30) [## 用 TypeScript 编写的 Node.js 应用程序的框架

### 包含 ESLint、Prettier 和 Husky 的设置说明。

javascript.plainenglish.io](/skeleton-for-node-js-apps-written-in-typescript-444fa1695b30) 

**第七步——设置钥匙锁领域和客户端**

如果你是第一次接触[键盘锁](https://www.keycloak.org/documentation)，那么请浏览下面的文章了解更多细节。

[](/introduction-to-building-an-effective-identity-and-access-management-architecture-with-keycloak-4c1645124d83) [## 使用 Keycloak 构建有效的身份和访问管理架构简介

### Keycloak 是一个开源软件产品，允许使用身份和访问管理进行单点登录，旨在为现代…

javascript.plainenglish.io](/introduction-to-building-an-effective-identity-and-access-management-architecture-with-keycloak-4c1645124d83) 

1.登录到 Keycloak —要登录，我们将使用下面的凭据，这些凭据已经添加到 docker-compose 中。

```
KEYCLOAK_USER: kcadmin
KEYCLOAK_PASSWORD: admin
```

![](img/24b35cadae78ccf651fa299fe1f12a0d.png)

Keycloak Login

2.创建领域—领域管理一组用户、凭据、角色和组。用户属于并登录到一个领域。领域相互隔离，只能管理和验证它们控制的用户。

```
Name : tyk
```

![](img/c89a4a43bb76cdd6e840e61087110fef.png)

Create Realm

3.添加用户——一旦我们创建了一个新领域，我们就可以添加一个新用户

![](img/f1f992f022780de31cc0ccfe157009a9.png)

create new user

4.更新密码—确保更新该用户的默认密码

![](img/2e8f4b23b88eddecb8cd5ab4fab5e7a9.png)

update password

5.创建客户端—客户端是可以请求 Keycloak 对用户进行身份验证的实体。大多数情况下，客户端是希望使用 Keycloak 来保护自己并提供单点登录解决方案的应用程序和服务。

这里我们将创建两个客户端，一个用于 API 认证流，另一个用于网关。我们的网关客户端已经被映射到资源客户端，因此该条目被添加到我们的 JWT 令牌中。

```
Gateway Client Name : tyk-gateway
Resource Client Name : tyk-client
```

![](img/1239f36ab75e66682d8d844db7e507dc.png)

tyk-gateway

![](img/a6b19fdb1296071bc81e85dfc893e580.png)

tyk-client

![](img/3032600f6d07db119c4e1f6d3f4176d1.png)

create protocol mapper from Mappers tab

**第 8 步—添加/创建新的 API**

确保我们知道我们的 API secret，我们的 Tyk 网关 API secret 存储在您的 tyk.conf 文件中，该属性称为 secret，您将需要使用它作为名为 **x-tyk-authorization** 的头来调用网关 API。如果您正在使用 Docker-compose，那么默认的 secrete 是`**foo**`，它可以在 Docker compose 文件的环境部分找到。

```
environment:
      - TYK_GW_SECRET=foo
```

我们将使用 POST API `{{baseUrl}}/tyk/apis`创建一个 API，这里的基本 URL 是`http://localhost:8080`。头`x-tyk-authorization: foo`和正文如下。

*   `proxy.listen_path`:监听的路径，如`/api`或`/`。在 Tyk 被配置为运行的端口上，任何进入主机的请求都将应用 API 定义中定义的规则。我们的演示将基于我们系统的状态 API 端点`[/w](http://21b1-103-109-12-32.ngrok.io/api/status/system)eb.`
*   `proxy.target_url`:这定义了如果请求通过了 Tyk 中的所有检查，它应该被代理到的目标 URL。示例— `[http://host.docker.internal:3146/w](http://host.docker.internal:3146/web)eb.`

**设置 OIDC**

要设置 API 定义以使用 OIDC，请将以下块添加到定义中，并确保没有启用其他访问方法:

```
"use_openid": true,
"openid_options": {
  "providers": [
    {
      "issuer": "http://oidc:8080/auth/realms/tyk",
      "client_ids": {
        "dHlrLWdhdGV3YXk=": "admin"
      }
    }
  ],
    "segregate_by_client": false
}
```

*   `use_openid`:设置为 true 以启用 OpenID 连接检查。
*   `openid_options.providers`:授权提供商及其客户端 id/匹配策略的列表。
*   `openid_options.providers.client_ids`:应用于其用户的客户端 id 和策略 id 列表。
*   **注意:**客户端 id 是 Base64 编码的，所以映射是`base64(clientid):policy_id`。当匹配的 idP/客户端 ID 中出现有效用户时，此条目中列出的策略将跨 OIDC ID 令牌应用于其令牌。
*   `openid_options.segregate_by_client`:启用此项可将策略应用于用户 ID 和客户端 ID 的组合。例如:
*   **如果禁用**:当 Alice 使用移动应用程序登录 API 时，Tyk 会应用与她通过 web 应用程序或桌面客户端登录时相同的速率限制和访问规则。
*   **如果启用**:当 Alice 使用移动应用程序登录 API 时，Tyk 会应用与她通过 web 应用程序或桌面客户端登录时不同的速率限制和访问规则。事实上，每个客户端和用户组合都有自己的内部表示。

[](https://tyk.io/docs/advanced-configuration/integrate/api-auth-mode/open-id-connect/) [## 与 OIDC 融合

### Tyk 支持任何符合标准的 OIDC 提供商提供的 OpenID Connect (OIDC)身份令牌…

tyk.io](https://tyk.io/docs/advanced-configuration/integrate/api-auth-mode/open-id-connect/) 

请在下面找到我们将要使用的示例

```
{
 "name": "web",
 "slug": "web",
 "api_id": "web",
 "org_id": "gateway_demo",
 "active": true,
 "use_openid": true,
 "openid_options": {
   "providers": [
        {
           "issuer": "http://oidc:8080/auth/realms/tyk",
           "client_ids": {
               "dHlrLWdhdGV3YXk=": "admin"
            }
        }
    ],
    "segregate_by_client": false
 },
 "version_data": {
 "not_versioned": true,
 "versions": {
     "Default": {
        "name": "Default"
     }
  }
 },
 "proxy": {
   "listen_path": "/web",
    "target_url": "http://host.docker.internal:3146/web",
    "strip_listen_path": true
  }
}
```

![](img/fa317f92d134a9ae22d9b97631bd4217.png)

create new api

**第 9 步——重启或热重装**

一旦我们创建了 API 文件，我们将需要重新启动 Tyk 网关或发出热重新加载命令:

```
API - [http://localhost:8080/tyk/reload/group](http://localhost:8080/tyk/reload/group)
HEADER - `x-tyk-authorization: foo`
METHOD - GET
```

![](img/47d113b2d8bfd8ccadedd324adfe7117.png)

reload the API

**步骤 10—尝试通过网关访问 API**

我们在这里仅用一个 API `[http://tyk:8000/w](http://tyk:8000/test-api)eb`配置了 Tyk，它只是将我们定向到我们的节点 js 应用程序。如果我们试图在没有授权头的情况下访问 API，那么它将返回带有 **401** 状态码的**未授权**。

![](img/25385565ab4a9862ae40ebe7b8d568f8.png)

**Try to access API via the gateway**

**步骤 11—创建访问令牌**

在 Keycloak 中，我们可以为网关使用仅承载客户端—它仅用于匹配 JWT 中的观众。这就是为什么有两个客户端——一个用于登录，一个用于网关。

```
API - [http://oidc:8080/auth/realms/tyk/protocol/openid-connect/token](http://oidc:8080/auth/realms/tyk/protocol/openid-connect/token)Authorization - 
    username - tyk-client
    password - client secret of tyk-client Content-Type - application/x-www-form-urlencodedMETHOD - POSTBody -grant_type:password
username:santosh
password:pass1
redirect_uri:[http://tyk:3000/auth/oidc](http://tyk:3000/auth/oidc)
```

![](img/922a76513e492f31490c9125525f2244.png)

**Create Access Token**

![](img/b3435f6730b11a1b296d402ef93d577b.png)

**Create Access Token**

**步骤 12 —通过网关访问 API**

我们现在可以通过 Tyk 网关访问 REST API 端点。这里我们需要从上一个 API 接收到的密钥。

```
API - http://localhost:8080/web
METHOD - GET
Header - Authorization: Bearer 1d1e45a4ffae843d39833a4412ce80a97
```

![](img/23980c9b2ac151c121f31f9c22a99781.png)

API via gateway with Authorization header

感谢阅读，请分享你的评论，如果这个博客增加了你的学习价值，请鼓掌。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***