# 使用 GitHub 操作将 React 应用程序部署到 AWS S3:分步指南

> 原文：<https://javascript.plainenglish.io/deploy-a-react-app-to-aws-s3-with-github-actions-a-step-by-step-guide-3572265332a3?source=collection_archive---------5----------------------->

## 在这篇初学者友好的文章中，您可以了解如何使用 GitHub Actions 将 React 应用程序部署到 AWS S3。

![](img/3e745a66c52a08c5722d6dbc1cf344e8.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在阅读了不同的文章后，把所有的拼图拼在一起有点困难，所以我决定为初学者创建一个分步指南，这样你就可以在不到 10 分钟的时间内部署你的应用程序。

如果您想跳到某个特定的部分，可以参考以下内容:

1.  创建 React 应用
2.  AWS:创建 IAM 用户
3.  AWS:创建 S3 时段
4.  GitHub 操作

# 1.创建 React 应用

从您最喜欢的终端运行:

```
yarn create react-app test-aws-github-actions --template typescript
```

关于这个脚本的更多信息，你可以[访问 create react app](https://create-react-app.dev/docs/adding-typescript/) 的文档。如果你用`yarn start`运行项目，你应该能看到经典模板。

![](img/d1b35b1334938a445f067248fa208601.png)

Create React App Template

我还想介绍如何使用环境变量，所以我将添加一个`.env`文件并更新主要文本。环境变量是:

```
REACT_APP_MAIN_TEXT="Testing AWS"
```

这是一个非常简单的文本，但它将帮助我们理解这个过程。您可以在图像中看到 git 历史的变化。它只是在主屏幕上显示文本。

![](img/6e6bf5985fe22803cd598a5c0dadaa79.png)

如您所见，来自环境变量的文本显示在 React 图标下面的主页上。

![](img/35553090078af320fe40cfc88fbf96d1.png)

React with environment variable

现在您可以将代码推送到 Github 仓库，让我们开始看看 AWS 方面的事情。

# 2.AWS:创建 IAM 用户

您首先需要的是 AWS 中的用户。从 IAM 控制台中，添加用户。创建过程有 5 个步骤

## 创建用户步骤 1

根据需要命名用户。我正在为这个项目创建一个用户，所以我用同样的方式命名它。在 GitHub actions 中，我们需要一个键，这样你就可以在初始屏幕中选择它。

![](img/110e164d1caeb28072c4ccc390838976.png)

IAM create user 1

## 创建用户步骤 2

第二步是向用户提供权限。您可以选择`AdminsitratorAccess`

![](img/6e35c95f0aae5a1a1db2d9a05dbc2d2f.png)

IAM create user 2

## 创建用户步骤 3

这一步允许您添加标签。请随意添加任何对您的管理员有用的相关内容。

![](img/cda03b5b164a6292c9c860b7eecfca83.png)

IAM create user 3

## 创建用户步骤 4

现在，您可以查看前面步骤中提供的信息。这将为您创建用户，因此请检查详细信息以确保所有信息都是正确的。

![](img/bec83a11998ea6f418cd85ef940e966e.png)

IAM create user 4

## 创建用户步骤 5

这是用户的总结。您将看到一个访问密钥和一个需要保存的密码，因为 GitHub 操作将使用它。

![](img/67525c1f7944ffa3c0789b23f7afc502.png)

IAM create user 5

# 3.AWS:创建 S3 时段

在 AWS 中，创建一个 S3 桶:[https://s3.console.aws.amazon.com/s3/bucket/create](https://s3.console.aws.amazon.com/s3/bucket/create)

这里，启用 ACL 很重要；否则，GitHub 操作会出错。

![](img/b7e72ce89b5202fa98a37c8e14f68969.png)

Create AWS S3

并解除对公众访问的封锁。

![](img/92731ee73d300130216c72cc68004c04.png)

Create AWS S3

在属性区，你可以找到一个静态网站托管的部分。启用静态网站托管，并将索引文档和错误文档更新到 index.html。

![](img/953b142734e15c003072f94cb2eff5bc.png)

保存更改后，您将看到主机的 URL。

![](img/875b683e3b268e315b33b4ff566ea61d.png)

Static Website Hosting AWS S3

这就是 AWS 的全部内容。

# 4.GitHub 操作

在 repo 中，创建一个新文件。

```
name: Deploy AWS
on:
  push:
    branches:
      - mainenv:
  REACT_APP_MAIN_TEXT: "Successfully deployed in AWS"
  AWS_S3_BUCKET: ${{ secrets.AWS_BUCKET_NAME }}
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  AWS_REGION: ${{ secrets.AWS_REGION }}
  SOURCE_DIR: "build"jobs:
  build:
    runs-on: ubuntu-lateststrategy:
      matrix:
        node-version: [16.x]steps:
    - uses: actions/checkout@v1
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}- name: Yarn Install
      run: yarn install- name: Staging Build
      run: yarn build- name: Deploy to S3
      uses: jakejarvis/s3-sync-action@master
      with:
        args: --acl public-read --follow-symlinks --delete
```

在 GitHub 中，更新[动作秘密](https://docs.github.com/en/actions/security-guides/encrypted-secrets)包括:

*   AWS_BUCKET_NAME
*   AWS_ACCESS_KEY_ID
*   AWS_SECRET_ACCESS_KEY
*   AWS_REGION

![](img/d9ef0a947eba01e8cc2d13076e4872d0.png)

GitHub secrets

一旦你提交和推动，你会看到行动运行:

![](img/537e3c8851e793358b790859dc7e07be.png)

GitHub Action

如果您检查您的 S3 桶，您将看到来自构建文件夹的所有文件:

![](img/b58bf732a00498438f8575c15ac72eae.png)

AWS S3 Files deployed from GitHub Actions

您将能够看到您的 React 应用程序正在工作:

![](img/7c8123a8d9b400e41a8b661a0676c139.png)

React App Deployed in AWS

# 解决纷争

## 路径问题

如果你还没有设置主机，你会看到一些路径的问题。这是因为 bucket 将管理 URL，而 React 是一个单页应用程序，它需要所有指向 index.html 的路由，因此 React 可以自己管理路由。

```
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<Error>
<Code>AccessDenied</Code>
<Message>Access Denied</Message>
</Error>
```

![](img/1d92994932eb5d3499233899b2583c8d.png)

要修复它，你需要在网站托管领域的 S3 配置中做一个小的更新。看台阶。

## ACL 的问题

如果您在 GitHub 操作中遇到与 ACL 相关的错误，那是因为 ACL 被禁用了。您需要在 AWS S3 配置中启用它们。

```
upload failed: build/asset-manifest.json to s3://***/asset-manifest.json An error occurred (AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs
upload failed: build/robots.txt to s3://***/robots.txt An error occurred (AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs
upload failed: build/logo512.png to s3://***/logo512.png An error occurred (AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs
upload failed: build/static/js/787.e67aebaf.chunk.js.map to s3://***/static/js/787.e67aebaf.chunk.js.map An error occurred (AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs
upload failed: build/static/css/main.e6c13ad2.css to s3://***/static/css/main.e6c13ad2.css An error occurred (AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs
```

![](img/e1709faee80ff6651eed405982bc6d6a.png)

要解决这个问题，您需要对 AWS S3 配置进行小的更新，以启用 ACL。

就这些，谢谢。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。******