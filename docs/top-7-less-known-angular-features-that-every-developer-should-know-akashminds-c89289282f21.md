# 每个开发人员都应该知道的 7 个鲜为人知的角度特性

> 原文：<https://javascript.plainenglish.io/top-7-less-known-angular-features-that-every-developer-should-know-akashminds-c89289282f21?source=collection_archive---------0----------------------->

[首页](https://www.akashminds.com/) [JavaScript](https://www.akashminds.com/search/label/JavaScript) 每个开发者都应该知道的 7 大鲜为人知的角度特征| Akashminds

![](img/eab710a357976f4e69144f3a4539e9a9.png)

Angular 是一个 JavaScript 框架，用于构建 web 应用程序。它是最流行的框架之一，被许多大公司使用。Angular 的许多特性使它成为 web 开发的绝佳选择。

然而，有一些鲜为人知的特性是每个开发人员都应该知道的。

它可以通过使我们的代码更易于维护和测试来帮助我们。它还可以帮助我们提高应用程序的性能。Angular 提供了非常酷的特性，我们可以在应用程序中集成这些特性，但是 angular 还有一些我们很多人不知道的特性。

每个开发人员都知道 Angular 是一个强大的框架。但是，Angular 还有一些鲜为人知的特性是每个开发者都应该知道的。

# 1.独立组件

这是 angular 提供的众多 Angular 最新功能之一。[独立组件](https://www.akashminds.com/2022/11/how-to-create-angular-standalone.html)允许您创建一个可用于任何角度应用的独立单元。这是棱角分明的新特征之一

这是一个非常强大的特性，可以用来创建可重用的组件。

独立组件不需要添加任何 ngModule，但它可以在没有模块的情况下工作。这是独立组件的主要特点，这里有完整的独立组件指南供你参考。

除了独立组件，还有独立管道和指令

```
@Component({
  selector: 'app-book-list',
  standalone: true,
  imports: [CommonModule, RouterModule, MatButtonModule],
  template: `
    <section>
      <div class="grid-container">
        <ng-container *ngFor="let book of bookService?.books; let i = index">
          <div class="grid-item" [routerLink]="'/details/' + i">
            <h3>{{ book?.name }}</h3>
            <img width="200" height="200" [src]="book?.imageUrl" [alt]="book?.name"/>
            <div class="">
              <button  mat-raised-button>Add to cart</button>
            </div>
          </div>
        </ng-container>
      </div>
    </section>
  `,
  styles: [
  ],
})
export class BookListComponent implements OnInit {
  constructor(readonly bookService: BooksService) { }

  ngOnInit(): void { }
}
```

# 2.ng 复数

Ngplural 是一个角度指令，可用于根据集合中的项目数量显示不同的内容。

例如，如果集合为空，您可以使用 ngplural 显示类似“没有项目”的消息，如果集合只包含一个项目，则显示“有 1 个项目”。

除了根据集合中项目的数量显示不同的内容之外，ngplural 还可以用于使文本多元化。例如，如果您想显示消息“您有 5 条消息”，您可以使用 ngplural 来表示单词“message”的复数形式。

总的来说，ngplural 是一个有用的指令，可以帮助你的 Angular 应用程序更加用户友好。

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html'
})
export class AppComponent {
  count :number = 5;
}<span [ngPlural]="count">
     <ng-template ngPluralCase="2">there are 2 items.</ng-template>
     <ng-template ngPluralCase="one">there is one item.</ng-template>
     <ng-template ngPluralCase="=4">there are four items.</ng-template>
     <ng-template ngPluralCase="many">there are many items.</ng-template>
     <ng-template ngPluralCase="5">there are five items.</ng-template>
     <ng-template ngPluralCase="no">there are no items.</ng-template>
  </span>
```

# 3.Javascript 的文档属性

如果您正在使用 Angular，您可能需要访问文档对象模型(DOM)。document 属性是一个代表 HTML 文档的全局对象。

您可以使用 document 属性来查询和操作 DOM。

```
import { DOCUMENT } from '@angular/common';
import { Component, Inject } from '@angular/core';

constructor(@Inject(DOCUMENT) documet: Document) {
  console.log(document)
}

renderImageElement() {
  this.document.getElementById("image")
}
```

# 4.角度中的元标签

元标签是 SEO(搜索引擎优化)的重要组成部分，因为它们帮助搜索引擎理解网页的内容。

通过在 meta 标签中包含相关关键字，网站管理员可以提高他们在搜索引擎结果页面(SERPs)中排名靠前的机会。

虽然 meta 标签不能保证高的 SERP 排名，但它们仍然是 angular 中 [SEO 的一个有价值的工具。除了帮助关键字研究，元标签还可以帮助提高来自 SERPs 的点击率(CTR)。](https://www.akashminds.com/2021/05/how-to-set-html-meta-tags-in-angular.html)

一个优化良好的 meta 标签可以吸引用户到你的网站，并鼓励他们点击你的列表。

```
import { Meta } from "@angular/platform-browser"
@Component({
    ...
})
export class TestComponent implements OnInit {
    constructor(private meta: Meta) {}
    ngOnInit() {
        meta.updateTag({name: "title", content: "My title"})
        meta.updateTag({name: "description", content: "My page descripton"})
        meta.updateTag({name: "image", content: "./assets/profile.jpg"})
        meta.updateTag({name: "site", content: "My Site content"})
    }
}
```

# 5.angular 中的 AppInitializer

AppInitializer 是 Angular 提供的一项服务，允许开发人员在应用程序启动后运行初始化代码。这对于确保总是加载某些模块以及在应用程序开始之前设置全局状态特别有用。

AppInitializers 使用 **APP_INITIALIZER** 令牌向 Angular 注册。当执行 AppInitializer 时，它将接收一个注入器作为它的第一个参数。这个注入器可以用来解析初始化代码所需的依赖关系。

一旦执行完所有的 AppInitializers，Angular 将开始运行应用程序的引导进程。

```
function runOnInitilization() {
    ...
}
@NgModule({
    providers: [
        { provide: APP_INITIALIZER, useFactory: runOnInitilization }
    ]
})
```

# 6.严格类型化的表单

```
import { Component } from '@angular/core';
import { FormControl, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css'],
})
export class UserComponent {
  profileForm = new FormGroup({
    firstName: new FormControl('Akash'),
    lastName: new FormControl('chauhan'),
    mobile: new FormControl('099909888'),
    address: new FormGroup({
      street: new FormControl('32 street'),
      city: new FormControl('chandigarh'),
      state: new FormControl('Punjab'),
      zip: new FormControl('160019'),
    }),
  });

  populateName() {
    this.profileForm.controls.firstName.setValue('Akashminds');
  }
```

# 7.模板插值

模板插值是 angular 的一个特性，允许你在 HTML 模板中插入变量。这对于显示数据库中的数据或使模板更加动态非常有用。

要使用模板插值，首先需要在组件类中创建一个变量。

然后，您可以使用双圆括号语法将该变量插入到模板中。((变量))而不是像我们平时用的花括号。{{变量}}。

```
@component({
   selector: "app"
   interpolation: ["((","))"],
   template: '
    <hello name="(( name ))"> </hello>
   ',
   styleUrls: ["./app.component.css"]
})

export class AppComponent {
 name = "Angular " + VERSION.major;
}
```

# 结论

总之，每个 Angular 开发人员都应该利用这个框架鲜为人知的特性来创建更健壮、无错误的应用程序。

利用这些特性将帮助开发人员避免常见错误，并使他们的代码更具可读性和可维护性。

Angular 包含了许多使开发更快更容易的特性。

随着 Angular 14 的发布，关于其功能的讨论已经很多了。该框架包括许多可以帮助我们开发的功能，如独立组件、严格类型的表单和 Angular CLI 自动完成。

【https://www.akashminds.com】最初发表于[](https://www.akashminds.com/2022/11/top-7-less-known-angular-features-that.html)**。**

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。****