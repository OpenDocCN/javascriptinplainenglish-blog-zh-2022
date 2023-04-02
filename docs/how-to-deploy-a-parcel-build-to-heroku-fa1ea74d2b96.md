# 如何将包构建部署到 Heroku

> 原文：<https://javascript.plainenglish.io/how-to-deploy-a-parcel-build-to-heroku-fa1ea74d2b96?source=collection_archive---------1----------------------->

## 关于将包构建部署到 Heroku 的教程。

![](img/0d36edfc53f3f509a89cab16480ef3d5.png)

Photo by [Chris Ried](https://unsplash.com/@cdr6934?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇文章讲述了如何将一个[包](https://parceljs.org/)构建部署到 [Heroku](https://www.heroku.com/) 。

![](img/6d50c71238341daeff9d5efc60ea59c5.png)

Parcel and Heroku

# 包裹

假设您有一个包裹应用程序:

*   包裹-示例

[](https://github.com/remarkablemark/parcel-example) [## GitHub-remarble mark/Parcel-example:Parcel web app 示例

### 受教程“用 Parcel 构建 web app”启发。克隆存储库:git 克隆…

github.com](https://github.com/remarkablemark/parcel-example) 

*   宗地类型脚本示例

[](https://github.com/remarkablemark/parcel-typescript-example) [## GitHub-remarble mark/Parcel-TypeScript-example:Parcel TypeScript 示例

### 宗地类型脚本示例。克隆存储库:git 克隆…

github.com](https://github.com/remarkablemark/parcel-typescript-example) 

*   react-type script-parcel-template

[](https://github.com/remarkablemark/react-typescript-parcel-template) [## GitHub-remarkable mark/React-type script-Parcel-template:React type script Parcel 模板

### React TypeScript 宗地模板。克隆存储库:git 克隆…

github.com](https://github.com/remarkablemark/react-typescript-parcel-template) 

在您的`[package.json](https://docs.npmjs.com/cli/v8/configuring-npm/package-json)`中，确保有一个`build`脚本:

Heroku 运行`[build](https://devcenter.heroku.com/articles/nodejs-support#customizing-the-build-process)`脚本，如果它在部署期间存在的话。

# 服务

安装[伺服](https://www.npmjs.com/package/serve)为静态站点服务；

```
npm install serve
```

在`package.json`中创建一个[启动脚本](https://devcenter.heroku.com/articles/deploying-nodejs#specifying-a-start-script):

或者创建一个 [Procfile](https://devcenter.heroku.com/articles/procfile) 来服务您的项目目录:

```
echo 'web: npx serve' > Procfile
```

> Heroku 通过查找 Procfile 或启动脚本来确定如何启动您的应用程序。

然后创建 [serve.json](https://github.com/vercel/serve-handler#options) 以便静态站点和路由被正确服务:

```
touch serve.json
```

提交并推送您的存储库。

# 反对

按顺序添加 [Heroku buildpacks](https://devcenter.heroku.com/articles/buildpacks) :

1.  [heroku/nodejs](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-nodejs)
2.  [heroku-build pack-static](https://elements.heroku.com/buildpacks/heroku/heroku-buildpack-static)([弃用](https://github.com/heroku/heroku-buildpack-static#warning-heroku-buildpack-static-is-deprecated))

Node.js buildpack 必须在 static buildpack 之前，因为必须先构建站点，然后才能提供服务。

可以通过 Heroku CLI 添加构建包:

将`<MY_APP_NAME>`替换为您的 Heroku 应用名称。

也可以加上`[app.json](https://devcenter.heroku.com/articles/app-json-schema#buildpacks)`:

创造一个`[static.json](https://github.com/heroku/heroku-buildpack-static#deploying)`:

```
touch static.json
```

并且[为您的静态应用程序配置](https://github.com/heroku/heroku-buildpack-static#configuration)选项:

推送部署 Heroku app。构建日志应该如下所示:

```
-----> Building on the Heroku-20 stack
-----> Using buildpacks:
       1\. heroku/nodejs
       2\. https://github.com/heroku/heroku-buildpack-static
-----> Node.js app detected
-----> Creating runtime environment
-----> Installing binaries
-----> Restoring cache
-----> Installing dependencies
-----> Build
-----> Pruning devDependencies
-----> Caching build
-----> Build succeeded!
-----> Static HTML app detected
-----> Installed nginx 1.19.0 to /app/bin
-----> Discovering process types
       Procfile declares types     -> (none)
       Default types for buildpack -> web
-----> Compressing...
-----> Launching...
       Released v1
       https://myappname.herokuapp.com/ deployed to Heroku
```

由于 Heroku 会自动为您的静态应用程序创建一个 dyno，因此无需使用 [Procfile](https://devcenter.heroku.com/articles/procfile) :

```
web bin/boot
```

*本文原载于 2022 年 3 月 16 日*[*remarkablemark.org*](https://remarkablemark.org/blog/2022/03/16/deploy-parcel-build-to-heroku/)*。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**