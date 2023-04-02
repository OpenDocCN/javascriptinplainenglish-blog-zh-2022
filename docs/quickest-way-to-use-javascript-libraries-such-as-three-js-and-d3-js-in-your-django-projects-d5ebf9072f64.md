# 在 Django 项目中使用 JavaScript 库，比如 Three.js 和 D3.js:最快的方法

> 原文：<https://javascript.plainenglish.io/quickest-way-to-use-javascript-libraries-such-as-three-js-and-d3-js-in-your-django-projects-d5ebf9072f64?source=collection_archive---------9----------------------->

本文将向您展示如何在 Django 项目中快速整合强大的 JavaScript 库，如 Three.js 和 D3.js。

![](img/1cb95de8982267b3717c0fbdbde74cd5.png)

先决条件:一个 Django 项目，参见 Django [文档](https://docs.djangoproject.com/en/3.2/intro/tutorial01/)来建立一个简单的 Django 项目。

库或相应的模块应该以一种不包含任何导出或导入的格式(即普通 JavaScript 格式)可用，Django 无需使用捆绑器即可访问。

许多被广泛使用和维护的 JavaScript 库，包括 Three.js 和 D3.js，在云服务器(如 Cloudflare)上有不同版本的普通 JavaScript。这些库的其他模块通常可以通过项目的 GitHub 资源库以普通 JavaScript 的形式获得(三个. js 模块见这个[文件夹](https://github.com/mrdoob/three.js/tree/dev/examples/js))。

**选项 1:** 在 Django 模板 HTML 文件中，包含一个指向托管的普通 JavaScript 文本文件的链接:

```
// Django template html file 
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script><script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script><script src="//cdnjs.cloudflare.com/ajax/libs/lodash.js/0.10.0/lodash.min.js"></script>
```

**选项 2:** 将普通的 JavaScript 文本复制到本地脚本中(位于 Django 静态文件夹中)。使用框架中的其他模块(如 Three.js 的 OrbitControls 和对象加载器)需要此选项。模板 HTML 文件中的脚本标记源将引用静态文件夹和 JavaScript 文件的特定路径，请参见下面的示例:

```
// Django template html file
<script src="{% static 'myApp/js/threejs/OrbitControls.js' %}"></script><script src="{% static 'myApp/js/threejs/GLTFLoader.js' %}"></script><script src="{% static 'myApp/js/threejs/CSS2DRenderer.js' %}"></script>
```

这种方法的替代方法(超出了本文的范围):

I .使用 bundler 如 bundle.js 或 webpack 将前端文件转换成普通的 JavaScript。

二。在服务器上托管库。

编码快乐！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***