# 利用角分量通信实现效率最大化

> 原文：<https://javascript.plainenglish.io/maximizing-efficiency-with-angular-component-communication-388941ec2dda?source=collection_archive---------21----------------------->

![](img/9d7eed9324d945bc46bec7665363fc74.png)

Photo by [Etienne Boulanger](https://unsplash.com/@etienneblg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/photos/erCPgyXNlto?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Angular 中的组件是控制用户界面特定元素的可重用代码。它们让开发人员编写易于管理和维护的模块化、可重用的代码。

使用组件的一个最显著的优势是它们的**能力，可以将**与另一个连接起来，允许开发者设计复杂的、交互式的程序。

角度组件可以通过多种方式相互通信，包括:

1.  **@输入和@输出装饰器**:这些装饰器通过使用属性绑定和事件绑定让组件交换数据。@Input decorator 用于将数据发送到组件中，而@Output decorator 用于从父组件可能管理的组件中发出事件。
2.  服务:角度服务是组件交流数据和功能的一种极好的方式。它们可以被注入到任何需要它们的组件中，让组件访问共享的数据或功能，而不必在它们之间直接传输。
3.  **本地引用:**组件可以使用本地引用来相互通信。局部引用是一种将引用分配给组件模板中的元素的方法，然后可以从组件的类中检索该元素。这使得组件可以通过它们的模板相互通信。
4.  **共享** **模块**:共享模块是一种将相关组件、指令和管道聚集在一起，并使它们对应用程序的其他区域可用的方法。这使得组件能够通过共享服务和其他公共资源间接地相互通信。

通过采用这些组件间的通信机制，开发人员可以设计出高效且有效的 Angular 应用程序，这些应用程序易于维护和扩展。

为每个用例选择合适的通信模式至关重要，因为每个用例都有优点和缺点，并且可能不适合所有情况。

这里有一个关于如何使用 **@Input** 和 **@Output** 装饰器在角度组件之间进行通信的例子:

考虑一个名为 **ProductListComponent** 的父组件，它显示一个商品列表，还有一个名为 **ProductItemComponent** 的子组件，它显示一个商品。ProductListComponent 必须向 ProductItemComponent 提供产品列表，以便可以显示每个产品。

我们可以使用 ProductListComponent 中的产品数组将项目列表连接到 ProductItemComponent 中的属性:

```
// product-list.component.ts

import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-product-list',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
export class ProductListComponent implements OnInit {
  public products: any[];

  constructor() { }

  ngOnInit(): void {
  }
}
```

然后，在 ProductItemComponent 中，我们可以使用 **@Input** decorator 将产品列表链接到一个组件属性:

```
// product-item.component.ts

import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-product-item',
  templateUrl: './product-item.component.html',
  styleUrls: ['./product-item.component.css']
})
export class ProductItemComponent implements OnInit {
  @Input() product: any;

  constructor() { }

  ngOnInit(): void {
  }
}
```

然后，我们可以利用 ProductListComponent 模板中的属性绑定向 ProductItemComponent 提供产品列表:

```
<!-- product-list.component.html -->

<app-product-item *ngFor="let product of products" [product]="product"></app-product-item>
```

这使 ProductListComponent 可以向 ProductItemComponent 提供产品列表，后者随后可能会单独显示每个产品。

这只是如何使用**@输入**和**@输出**装饰器来跨角度组件通信的一个例子。Angular 中组件间通信的其他方法包括服务、本地引用和共享模块。

为每个用例选择合适的通信模式至关重要，因为每个用例都有优点和缺点，并且可能不适合所有情况。

我希望这篇文章对你有所帮助。 ***感谢阅读。***

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*