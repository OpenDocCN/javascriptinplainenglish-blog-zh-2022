# Vue 3 GitHub 的简单动作

> 原文：<https://javascript.plainenglish.io/vue-3-github-actions-in-a-nutshell-d207de6f122e?source=collection_archive---------13----------------------->

## GitHub 将 CI/CD 添加到 Vue 3 项目的操作。

![](img/9c73648a48993dce617c37b18e32c307.png)

[GitHub Actions logo with header.](https://itnext.io/github-github-actions-overview-and-argocd-deployment-example-b6cf0cf6f832)

## 在本地测试 GitHub 操作工作流

要为 GitHub 动作工作流启用测试驱动开发，您需要能够在本地测试 GitHub 动作。使你能够做到这一点。

## 阻止提交和推进主分支

在 GitHub 中，可以设置[**分支保护规则**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule) ，该规则提供了一个选项*“限制谁可以推送至匹配分支”*，该选项允许防止有人直接推送至主分支。

但是*“受保护分支”仅在非免费产品中可用。此外，也不妨碍有人误闯当地的`main`分支，搞乱当地的`git`历史。通过`git config branch.master.pushRemote no_push`改变本地`git`配置，可以**禁止推入本地**T3。*

## *类型检查`.vue`文件*

*[](https://github.com/marketplace/actions/vue-tsc-action) [## vue-TSC-行动- GitHub 市场

### Github 动作这个 GitHub 动作运行 vue-tsc。vue 文件并显示在整个代码库中发现的错误…

github.com](https://github.com/marketplace/actions/vue-tsc-action) 

如果将单个文件组件与 TypeScript 一起使用，您需要确保 TypeScript 代码是有效的。要将它构建成一个工作流，你可能想看看 GitHub 的动作***【vue-TSC-Action】***。

## 谷歌灯塔审计

[](https://github.com/marketplace/actions/lighthouse-ci-action) [## 灯塔 CI 行动- GitHub 市场

### 使用 Lighthouse 审计 URL 并使用 Lighthouse CI 测试性能。此动作将灯塔 CI 与 Github 整合…

github.com](https://github.com/marketplace/actions/lighthouse-ci-action) 

[*Lighthouse*](https://developers.google.com/web/tools/lighthouse) 是谷歌的一个工具，它“(……)对性能、可访问性、渐进式网络应用、搜索引擎优化等进行审计”。使用***“light house CI Action”***将其集成到 GitHub Action 工作流中。或者，你也可以看看 [***【灯塔检查】***](https://github.com/marketplace/actions/lighthouse-check) 。

## 用棉绒整理文件

[](https://github.com/marketplace/actions/hadolint-action) [## Hadolint Action - GitHub 市场

### GitHub 操作运行 Hadolint Dockerfile 林挺工具的 GitHub 操作。将以下步骤添加到您的工作流程中…

github.com](https://github.com/marketplace/actions/hadolint-action) 

如果在一个 *Docker* 容器中部署一个 *Vue* 项目，确保当*Docker 文件*被添加和/或修改后 *Docker* 构建(见下面的操作)仍然通过可能会有所帮助。Hadolint 是一个著名的 Dockerfiles 分析器，可以通过 GitHub 动作***【Hadolint 动作】*** 集成到工作流中。

[](https://github.com/marketplace/actions/get-all-changed-files) [## 获取所有更改的文件- GitHub Marketplace

### GitHub 动作在拉请求或推提交中获取所有更改/修改的文件。您可以选择获取所有…

github.com](https://github.com/marketplace/actions/get-all-changed-files) 

要仅在 Dockerfile 已更改时执行该检查，您可能需要使用 GitHub 动作 ***“获取所有已更改的文件”*** 来有条件地执行该动作。BTW: **这个 GitHub 动作也可以在很多其他场景中用于条件动作执行。**

## 构建到 Docker 容器中

[](https://github.com/marketplace/actions/build-and-push-docker-images) [## 构建和推送 Docker 图片- GitHub 市场

### GitHub Action 使用 Buildx 构建和推送 Docker 图像，完全支持莫比 BuildKit 提供的功能…

github.com](https://github.com/marketplace/actions/build-and-push-docker-images) 

您可以将[Vue Cookbook recipe*“Dockerize Vue . js App”*](https://vuejs.org/v2/cookbook/dockerize-vuejs-app.html)与 GitHub 动作 ***“构建并推送 Docker 映像”*** 结合起来，将 *Vue* 项目包装成 Docker 映像，并将其部署到容器(映像)注册表中。支持的注册表有:

*   [本地注册表](https://github.com/docker/build-push-action/blob/master/docs/advanced/local-registry.md)
*   [码头中心](https://github.com/docker/login-action#docker-hub)
*   [GitHub 容器注册表](https://github.com/docker/login-action#github-container-registry)
*   [GitLab 注册表](https://github.com/docker/login-action#gitlab)
*   [Azure 容器注册表](https://github.com/docker/login-action#azure-container-registry-acr)
*   [谷歌容器注册表](https://github.com/docker/login-action#google-container-registry-gcr)
*   [谷歌神器注册表](https://github.com/docker/login-action#google-artifact-registry-gar)
*   [AWS 弹性容器注册(ECR)](https://github.com/docker/login-action#aws-elastic-container-registry-ecr)
*   [AWS 公共弹性集装箱登记处](https://github.com/docker/login-action#aws-public-elastic-container-registry-ecr)
*   [OCI 甲骨文云基础设施注册中心(OCIR)](https://github.com/docker/login-action#oci-oracle-cloud-infrastructure-registry-ocir)
*   [Quay.io](https://github.com/docker/login-action#quayio)

## 将 Vue 项目部署到 GitHub 页面

[](https://github.com/marketplace/actions/vue-to-github-pages) [## Vue 到 Github 页面- GitHub 市场

### 此操作将构建您的 Vue 项目，并将其部署到 Github 页面

github.com](https://github.com/marketplace/actions/vue-to-github-pages) 

动作***“Vue 到 GitHub 页面”*** 用 [npm 或 yarn](https://github.com/xRealNeon/VuePagesAction/blob/main/action.yml#L42) 构建 Vue.js 项目，[将项目部署为 GitHub 页面](https://github.com/xRealNeon/VuePagesAction/blob/main/action.yml#L51)。例如，我如何使用 GitHub 动作将我的 Vue.js 站点自动部署到 GitHub 页面 [*和相应的*](https://dev.to/juniordevforlife/how-i-use-github-actions-to-auto-deploy-my-vue-js-site-to-github-pages-49bf) *[GitHub 库](https://github.com/JasonFritsche/weather-vue)。*

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。**