# 如何在非根 Docker 容器中使用 NGINX 为 React 应用提供服务

> 原文：<https://javascript.plainenglish.io/how-to-serve-a-react-app-with-nginx-in-a-non-root-docker-container-cbc4c6acc177?source=collection_archive---------3----------------------->

![](img/4b3aa8e47ef4aec4e3b84e68202b6b7f.png)

Photo by [Joshua Sortino](https://unsplash.com/fr/@sortino?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/data?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

喔，这个标题有点拗口。但是我想就此写一篇短文，因为这是我最近遇到的一个问题。这比我想象的要复杂得多！

我在网上找到了不少文章，但仍有不少问题需要解决。

因此，这是我的 docker 文件看起来像这样:

这使用一个多阶段构建来首先捆绑 react 应用程序的生产构建。一旦完成，在构建的第二阶段，nginx 配置文件——`nginx.conf`——将与应用程序的产品捆绑包一起复制到容器中。

然后，需要做一些事情来授予 NGINX 以非 root 用户身份运行的权限:

1.  它需要一个新的进程 id 文件
2.  我们将用来运行应用程序的用户需要对该文件和其他必要文件(缓存、日志、我们的 react 应用程序)的权限。

然后，您可以更改运行 Docker 容器的用户，这样就非常容易了！

当然，你还需要一个 NGINX 配置文件…下面是 React 应用程序的基本配置文件:

完成这些后，您可以使用以下命令运行您的应用程序:

`docker build -t react-app .`

`docker run -d -p 8080:8080 react-app`

然后，导航到 [http://localhost:8080](http://localhost:8080) 查看！

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣规模化你的软件创业*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*