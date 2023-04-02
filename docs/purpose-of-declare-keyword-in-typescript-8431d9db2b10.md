# TypeScript 中“declare”关键字的用途

> 原文：<https://javascript.plainenglish.io/purpose-of-declare-keyword-in-typescript-8431d9db2b10?source=collection_archive---------1----------------------->

## 详细介绍了 TypeScript 'declare '的作用，所以你对*.d.ts 文件并不陌生。

![](img/76172436be5c48adbde1f00f0ac81e0c.png)

欢迎来到**掌握打字稿**系列。本系列将以动画的形式介绍 TypeScript 的核心知识和技术。让我们一起学习吧！以前的文章如下:

*   [**TypeScript 泛型中的 K、T、V 是什么？**](https://medium.com/frontend-canteen/what-are-k-t-and-v-in-typescript-generics-9fabe1d0f0f3)
*   [**使用 TypeScript 像 Pro 一样映射类型**](/using-typescript-mapped-types-like-a-pro-be10aef5511a)
*   [**使用 TypeScript 交集类型像亲**](/using-typescript-intersection-types-like-a-pro-a55da6a6a5f7)
*   [**使用 TypeScript 条件类型像亲**](/use-typescript-conditional-types-like-a-pro-7baea0ad05c5)
*   [**使用打字稿推断像亲**](https://levelup.gitconnected.com/using-typescript-infer-like-a-pro-f30ab8ab41c7)
*   [**使用 TypeScript 模板字面类型像亲**](https://medium.com/javascript-in-plain-english/how-to-use-typescript-template-literal-types-like-a-pro-2e02a7db0bac)
*   [**可视化打字稿:15 种最常用的实用类型**](/15-utility-types-that-every-typescript-developer-should-know-6cf121d4047c)

当您在 TypeScript 项目中打开`*.d.ts`声明文件时，您可能会看到`declare`。你知道`declare`是干什么的吗？如果你不知道，看完这篇文章，也许你会。

在 TypeScript 项目中，可能会以脚本标签的形式导入第三方 JS-SDK，比如导入 **Google Maps** 平台的 JS-SDK。

```
<script
   src="[https://maps.googleapis.com/maps/api/js?key=AIzaSyB41DRUbKWJHPxaFjMAwdrzWzbVKartNGg&callback=initMap&v=weekly](https://maps.googleapis.com/maps/api/js?key=AIzaSyB41DRUbKWJHPxaFjMAwdrzWzbVKartNGg&callback=initMap&v=weekly)" defer></script>
```

初始化后，您将调用 JS-SDK 在 TypeScript 文件中公开的 API。

![](img/cebd882e859edf7ebdef71d0292ea3dd.png)

虽然根据 Google Maps 开发文档，你使用的是 JS-SDK 提供的 API，但是对于上面的代码，TypeScript 编译器还是会提示相应的错误信息。这是因为 TypeScript 编译器不识别全局变量`google`。

那么如何解决这个问题呢？答案是使用`declare`关键字声明`google`全局变量，以便 TypeScript 编译器可以识别该全局变量。

```
declare var google: any;
```

![](img/4e6b225677e8ccf48eb7a73874da5b5b.png)

看到这里，你会迷茫吗？为什么可以在 TypeScript 项目中正常使用`JSON`、`Math`或`Object`这样的全局变量？这是因为 TypeScript 在内部为我们做了声明，前面提到的全局变量是在 **lib.es5.d.ts** 声明文件中声明的。

```
// typescript/lib/lib.es5.d.ts
declare var JSON: JSON;
declare var Math: Math;
declare var Object: ObjectConstructor;
```

事实上，除了声明全局变量，declare 关键字还可以用于声明全局函数、全局类或全局枚举类型。您在工作中可能用到的`eval`、`isNaN`、`encodeURI`、`parseInt`等函数也在 **lib.es5.d.ts** 声明文件中声明:

```
declare function eval(x: string): any;
declare function isNaN(number: number): boolean;
declare function encodeURI(uri: string): string;
declare function parseInt(string: string, radix?: number): number;
```

需要注意的是，当声明一个全局函数时，我们并不包括函数的具体实现。通过声明文件，TypeScript 编译器可以识别上述全局 JavaScript 函数。

之前找不到“google”这个名字的解决方法比较暴力。**比较好的解决方法是使用** [**TypeScript 网站**](https://www.typescriptlang.org/dt/search?search=google+map) **或者**[**definitely typed project**](https://github.com/DefinitelyTyped/DefinitelyTyped)上提供的类型声明文件搜索功能，或许可以找到更高质量的第三方库的类型声明文件。

![](img/75768d4f46d1682b16e413b2bb851939.png)

*[*明确类型化项目*](https://github.com/DefinitelyTyped/DefinitelyTyped) *是一个开源项目，维护了很多包的类型声明文件。**

*一旦找到，您就可以通过 npm 安装带有所需类型声明文件的模块。如果你已经阅读了关于使用 TypeScript 和谷歌地图的指南。可以找到 Google Maps 对应的类型声明文件。之后，您可以使用 npm 来安装它:*

```
*npm i -D [@types/google](http://twitter.com/types/google).maps*
```

*对于 npm 包“foo”，其类型位于“@types/foo”。比如大家比较熟悉的 jquery 库，它的包名是— `@types/jquery`。*

*接下来，我们将讨论“声明”的其他用法。当你打开 Vite 项目中的`client.d.ts`声明文件时，你会看到很多声明模块的代码。*

*![](img/f01bcafcd4ba01e32e5b6df03d2aecd7.png)*

*在上面的代码中，我们声明了`css`、`jpg`和`ttf`模块。为什么需要声明这些模块？**因为如果不声明它们，TypeScript 编译器不会识别这些模块，会提示相应的错误信息。***

*![](img/f127901286d1745eac758c3436ae8538.png)*

*在声明模块时，为了避免用对应的模块声明每个资源，TypeScript 2.0 开始支持**通配符(*)形式**来声明模块的名称。*

*![](img/70b97eed67e521635c42d896fc5a6575.png)*

*此外，TypeScript 允许您通过声明模块语法来扩展现有模块中定义的类型。例如，如果您想将`$axios`属性添加到每个 Vue 组件实例中，您可以这样做:*

```
*import { AxiosInstance } from "axios";declare module "[@vue/runtime-core](http://twitter.com/vue/runtime-core)" {
  interface ComponentCustomProperties {
    $axios: AxiosInstance;
  }
}*
```

*然后，使用 config 对象的`globalProperties`属性，您可以有效地将`$axios`属性添加到每个组件实例:*

```
*import { createApp } from "vue";
import axios from "axios";
import App from "./App.vue";const app = createApp(App);
app.config.globalProperties.$axios = axios;
app.mount("#app");*
```

*最后，在组件中，您可以通过组件内部实例的`proxy.$axios`属性访问 **axios** 对象:*

```
*import { getCurrentInstance , ComponentInternalInstance} from "vue"const { proxy } = getCurrentInstance() as ComponentInternalInstance
proxy!.$axios
  .get("[https://jsonplaceholder.typicode.com/todos/1](https://jsonplaceholder.typicode.com/todos/1)")
  .then((response) => response.data)
  .then((json) => console.log(json));*
```

*看完这篇文章，相信你已经了解了`declare`关键字的作用以及一些常见的应用场景。如果你想学习打字稿，那么就不要错过**掌握打字稿**系列。*

*在 [Medium](https://medium.com/@bytefer) 或 [Twitter](https://twitter.com/Tbytefer) 上关注我，阅读更多关于 TS 和 JS 的内容！*

*![Bytefer](img/238cf2afd3c689b50719951ba2fd880d.png)

[拜特弗](https://medium.com/@bytefer?source=post_page-----8431d9db2b10--------------------------------)* 

## *掌握打字稿系列*

*[View list](https://medium.com/@bytefer/list/mastering-typescript-series-688ee7c12807?source=post_page-----8431d9db2b10--------------------------------)**47 stories**![](img/8fba4cad7ae795f6abed5234e33e0356.png)**![](img/373c978fed504a3c38f0fdb5b617fedb.png)**![](img/a8ea3e3ecad1c2d2697107f3ce466e42.png)*

# *资源*

 *[## 搜索类型化的包

### 查找具有类型声明的 npm 包，无论是绑定的还是明确类型的。

www.typescriptlang.org](https://www.typescriptlang.org/dt/search?search=)* *[](https://github.com/DefinitelyTyped/DefinitelyTyped) [## GitHub-definitely typed/definitely typed:高质量类型脚本类型库…

### 高质量类型脚本类型定义的存储库。此部分跟踪存储库的健康状况，并…

github.com](https://github.com/DefinitelyTyped/DefinitelyTyped)* 

**更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*以及*[**T42 不和**](https://discord.gg/GtDtUAvyhW) *上跟随我们。***