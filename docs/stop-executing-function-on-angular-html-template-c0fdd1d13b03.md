# 停止在 Angular HTML 模板上执行函数

> 原文：<https://javascript.plainenglish.io/stop-executing-function-on-angular-html-template-c0fdd1d13b03?source=collection_archive---------4----------------------->

## Angular 允许你在 HTML 模板中执行一个函数或 getter。但是，你想过这是一个好方法吗？

![](img/c087acbd2da917f7b9262e2f5b0ee48e.png)

当你开发一个组件时，你也将编写一个已经支持[绑定](https://angular.io/guide/binding-overview)的 HTML 模板。绑定在从模板(DOM 元素、指令或组件)创建的 UI 的一部分和组件的数据模型之间创建一个活动连接。你可以绑定一个变量，值，甚至是执行一个函数。

# 问题是

当 Angular 运行[变化检测](https://angular.io/guide/change-detection)时，它将从上到下遍历您的组件，寻找绑定值的变化，以便数据模型的变化反映在应用程序的视图中。这种机制允许 Angular 仅在改变的边界值和变量上智能地重新渲染。

相反，在 HTML 中执行一个方法时。Angular 将总是盲目地重新执行一个绑定的函数，因为它不能确定什么条件被认为是函数中的变化。

这里有一个[的密码本](https://codepen.io/sulha199/pen/XWqOKEj)说明了这种情况:

[https://codepen.io/sulha199/pen/XWqOKEj](https://codepen.io/sulha199/pen/XWqOKEj)

如上图 [Codepen](https://codepen.io/sulha199/pen/XWqOKEj) 所示，每次点击一个按钮，那么 Angular 就会一直执行直接传递给 HTML 的方法。然而，使用[纯管道](https://angular.io/guide/pipes#detecting-pure-changes-to-primitives-and-object-references)传递的方法只在输入值改变时执行。

```
"w/ pipe = executed 1x | w/o pipe = executed 4x""w/ pipe = executed 1x | w/o pipe = executed 6x""w/ pipe = executed 1x | w/o pipe = executed 8x""update text""w/ pipe = executed 2x | w/o pipe = executed 12x""w/ pipe = executed 2x | w/o pipe = executed 14x""w/ pipe = executed 2x | w/o pipe = executed 16x"
```

一个简单的函数如果一直被执行，相对来说不会带来什么伤害。然而，具有副作用的函数可能会导致意外的行为，因为副作用会在每次变更检测发生时产生。另一种情况是函数返回图像资源 URL。当检测到变化时，它将重新请求图像。

# 管

[管道](https://angular.io/guide/pipes-overview)是在[模板表达式](https://angular.io/guide/glossary#template-expression)中使用的简单函数，用于接受输入值并返回转换后的值。[纯管道](https://angular.io/guide/pipes#detecting-pure-changes-to-primitives-and-object-references)有智能机制，所以只有当输入值改变时才执行。听起来我们可以通过将它们转换成管道来解决上面的函数重新执行。然而，[创建管道](https://angular.io/guide/pipes-custom-data-trans#using-the-pipetransform-interface)也不是一个有效的解决方案，因为您需要创建管道类本身，然后决定如何将它注入到您的组件中。

# 各行各业的管道

意识到上述问题，我编写了自己的管道，接受一个函数作为参数。令人惊讶的是，在 Typescript 的帮助下，管道还能够建议输入值的类型和额外管道的参数。

在这里，我分享我的代码是什么样子的:

```
import { Pipe, PipeTransform } from '[@angular/core](http://twitter.com/angular/core)'/** Obtain the arguments' types of a function except the first argument */
type RestArgument<T> = T extends (first: unknown, ...args: infer Rest) => any
  ? Rest
  : never[@Pipe](http://twitter.com/Pipe)({ name: 'apply' })
export class ApplyFunctionPipe implements PipeTransform {
  /**
   * [@param](http://twitter.com/param) callbackMethod method that is to be run using `ApplyFunctionPipe`.
   ** If you require access to component's property, please pass an arrow function instead of class method
   */
  transform<Callback extends (value: any, ...extra: any[]) => any>(
    value: Parameters<Callback>[0],
    callbackMethod: Callback,
    ...extra: RestArgument<Callback>
  ): ReturnType<Callback> {
    return callbackMethod(value, ...extra)
  }
}
```

**用法**:

```
{{ someProperties | apply : 'someMethod' }}
```

# 阵列管道

作为奖励，我还将分享一个可以进行各种数组操作的管道

```
type AnyFunction = (...args: any[]) => any
type GetParameters<F> = F extends AnyFunction ? Parameters<F> : never
type GetReturn<F> = F extends AnyFunction ? ReturnType<F> : neverexport type FirstArgs<T, F = any> = T extends [
  first: infer First,
  ...args: any
] ? (First extends F ? First : never)
  : never[@Pipe](http://twitter.com/Pipe)({ name: 'array', pure: false })
export class ArrayPipe implements PipeTransform {
  transform<
    ItemType, 
    ArrayType extends Array<ItemType>, 
    MethodName extends keyof ArrayType, 
    MethodArgs extends GetParameters<ArrayType[MethodName]>
  >(items: ArrayType, arrayMethod: MethodName, ...args: MethodArgs): MethodName extends 'map' ? ReturnType<FirstArgs<MethodArgs, AnyFunction>>[] : GetReturn<ArrayType[MethodName]> {
    return typeof items[arrayMethod] === 'function' ? 
      (items[arrayMethod] as any)(...args as any) : 
      items[arrayMethod]
  }
}
```

**用法**:

```
{{ [ 1, 2] | array : 'join': ' | ' }} <!-- will output "1 | 2" -->
```

# 最后

**感谢阅读。我打算分享更多简单而有效的技巧。我期待着你的关注。**

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。****

****有兴趣规模化你的软件创业*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。**