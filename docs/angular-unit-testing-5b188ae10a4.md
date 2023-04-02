# 角度单位测试

> 原文：<https://javascript.plainenglish.io/angular-unit-testing-5b188ae10a4?source=collection_archive---------5----------------------->

在这个角度单元测试教程中，我们将演示如何构建一个简单的角度应用程序，然后通过例子一步一步地完成单元测试过程。

我们将详细介绍以下内容:

*   **什么是角度测试？**
*   **什么是角度单元测试？**
*   **为什么你应该对 Angular apps 进行单元测试**
*   **角度测试怎么写？**
*   **什么是羯磨有角？**
*   **如何用 Angular 编写单元测试**
*   **如何测试角度服务**
*   **如何测试角度组件**
*   **如何测试角度异步运行**

按照本教程，你应该对如何使用 [Angular](https://angular.io/guide/testing-services) 有一个基本的了解。

# 什么是角度测试？

[角度测试](https://angular.io/guide/testing)是使用[角度 CLI](https://angular.io/cli) 设置的每个项目的核心功能。

为了与 JavaScript 生态系统保持同步，Angular 团队每年都会发布两个主要的 Angular 版本。从一开始到最近的版本， [Angular 11](https://blog.angular.io/version-11-of-angular-now-available-74721b7952f7) ，Angular 的设计就考虑到了可测试性。

有两种角度测试:

1.  单元测试是测试小的、孤立的代码片段的过程。也称为隔离测试，单元测试不使用外部资源，如网络或数据库
2.  **功能测试**是指从用户体验的角度测试 Angular 应用的功能，也就是说，当应用在浏览器中运行时，就像用户一样与应用进行交互

# 什么是角度单位测试？

[角度单元测试](https://docs.angularjs.org/guide/unit-testing)是指测试单个代码单元的过程。

角度单元测试旨在发现诸如不正确的逻辑、行为不当的函数等问题。通过分离代码片段。这有时比听起来更困难，尤其是对于关注点分离不良的复杂项目。Angular 旨在帮助你以这样一种方式编写代码，使你能够单独测试你的应用程序的功能。

# 为什么应该对 Angular 应用进行单元测试

角度单元测试使你能够基于用户行为测试你的应用。虽然测试每一种可能的行为是乏味、低效和无效的，但是为应用程序中的每一个耦合块编写测试有助于演示这些块的行为。

测试这些块的强度的最简单的方法之一是为每个块编写一个测试。您不必等到用户抱怨单击按钮时输入字段的行为。通过为你的模块(组件、服务等)编写单元测试。)，可以很容易的察觉到什么时候有断档。

我们的示例 Angular 应用程序有一个服务、一个组件和一个异步任务来模拟从服务器获取的数据。

# 角度测试怎么写？

当您使用 Angular CLI ( `ng new appName`)创建新项目时，会添加一个默认组件和测试文件。另外——如果你像我一样，总是在寻找捷径——测试脚本总是与你使用 Angular CLI 创建的任何组件模块(服务、组件)一起创建。

这个以`.spec.ts`结尾的测试脚本总是被添加。让我们来看看最初的测试脚本文件，它是`app.component.spec.ts`:

```
import { TestBed, async } from '@angular/core/testing';
import { AppComponent } from './app.component';
describe('AppComponent', () => {
  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [
        AppComponent
      ],
    }).compileComponents();
  }));
  it('should create the app', async(() => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.debugElement.componentInstance;
    expect(app).toBeTruthy();
  }));
  it(`should have as title 'angular-unit-test'`, async(() => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.debugElement.componentInstance;
    expect(app.title).toEqual('angular-unit-test');
  }));
  it('should render title in a h1 tag', async(() => {
    const fixture = TestBed.createComponent(AppComponent);
    fixture.detectChanges();
    const compiled = fixture.debugElement.nativeElement;
    expect(compiled.querySelector('h1').textContent).toContain('Welcome to angular-unit-test!');
  }));
});
```

让我们运行第一个测试，以确保没有任何问题发生:

```
ng test
```

您可能想知道，即使项目在浏览器中呈现，我们如何通过简单地编写测试来模拟用户行为？随着我们的继续，我将演示如何模拟和 Angular 应用程序在浏览器上运行。

# 《角》中的业力是什么？

[Karma](https://karma-runner.github.io/latest/index.html) 是一个 JavaScript 测试运行器，它在 Angular 中运行单元测试片段。Karma 还确保测试结果在控制台或文件日志中打印出来。

默认情况下，Angular 运行在 Karma 上。其他试跑者还包括[摩卡](https://blog.logrocket.com/a-quick-and-complete-guide-to-mocha-testing-d0e0ea09f09d/)和[茉莉](https://jasmine.github.io/)。Karma 提供了一些工具，使得在用 Angular 编写代码时调用 Jasmine 测试变得更加容易。

# 如何用 Angular 编写单元测试

角度测试包包括两个名为`TestBed`和`async`的工具。`TestBed`是主要的角度实用套件。

![](img/a7130f4b9f1a20e556443479ba07eb93.png)

`describe`容器包含不同的块(`it`、`beforeEach`、`xit`等)。).`beforeEach`在任何其他程序块之前运行。其他块的运行互不依赖。

从`app.component.spec.ts`文件开始，第一个块是容器内的`beforeEach`(`describe`)。这是唯一一个在任何其他程序块之前运行的程序块(`it`)。`app.module.ts`文件中 app 模块的声明在`beforeEach`块中模拟(声明)。在`beforeEach`块中声明的组件(`AppComponent`)是我们希望在这个测试环境中拥有的主要组件。同样的逻辑也适用于其他测试声明。

调用`compileComponents`对象来编译组件的资源，如模板、样式等。如果使用 webpack，您可能不一定要编译组件:

```
beforeEach(async(() => {
   TestBed.configureTestingModule({
      declarations: [
         AppComponent
      ],
   }).compileComponents();
}));
```

现在组件已经在`beforeEach`块中声明，让我们检查组件是否被创建。

`fixture.debugElement.componentInstance`创建该类的一个实例(`AppComponent`)。我们将使用`toBeTruthy`测试该类的实例是否真正被创建:

```
it('should create the app', async(() => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.debugElement.componentInstance;
    expect(app).toBeTruthy();
}));
```

第三块演示了如何访问已创建组件的属性(`AppComponent`)。默认情况下添加的唯一属性是标题。您可以从创建的组件实例(`AppComponent`)中轻松检查您设置的标题是否已更改:

```
it(`should have as title 'angular-unit-test'`, async(() => {
     const fixture = TestBed.createComponent(AppComponent);
     const app = fixture.debugElement.componentInstance;
     expect(app.title).toEqual('angular-unit-test');
}));
```

第四块演示了测试在浏览器环境中的行为。在创建组件之后，调用所创建组件的实例(`detectChanges`)来模拟在浏览器环境中运行。现在组件已经呈现，您可以通过访问呈现组件的`nativeElelment`对象(`fixture.debugElement.nativeElement`)来访问它的子元素:

```
it('should render title in a h1 tag', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   fixture.detectChanges();
   const compiled = fixture.debugElement.nativeElement;
 expect(compiled.querySelector('h1').textContent).toContain('Welcome to angular-unit-test!');
}));
```

现在，您已经熟悉了测试组件的基础知识，让我们测试我们的 Angular 示例应用程序。

![](img/9e0e83ba1aaddf3bd4f9f8e7492919c3.png)

# 如何测试角度服务

服务通常依赖于 Angular 注入到构造函数中的其他服务。在许多情况下，通过将`providedIn: root`添加到可注入对象，可以很容易地创建和注入这些依赖关系，这使得任何组件或服务都可以访问它:

```
import { Injectable } from "@angular/core";
import { QuoteModel } from "../model/QuoteModel";@Injectable({
  providedIn: "root"
})
export class QuoteService {
  public quoteList: QuoteModel[] = []; private daysOfTheWeeks = ["Sun", "Mon", "Tue", "Wed", "Thurs", "Fri", "Sat"]; constructor() {} addNewQuote(quote: String) {
    const date = new Date();
    const dayOfTheWeek = this.daysOfTheWeeks[date.getDate()];
    const day = date.getDay();
    const year = date.getFullYear();
    this.quoteList.push(
      new QuoteModel(quote, `${dayOfTheWeek} ${day}, ${year}`)
    );
  } getQuote() {
    return this.quoteList;
  } removeQuote(index) {
    this.quoteList.splice(index, 1);
  }
}
```

这里有一些测试`QuoteService`类的方法:

```
/* tslint:disable:no-unused-variable */
import { QuoteService } from "./Quote.service";describe("QuoteService", () => {
  let service: QuoteService; beforeEach(() => {
    service = new QuoteService();
  }); it("should create a post in an array", () => {
    const qouteText = "This is my first post";
    service.addNewQuote(qouteText);
    expect(service.quoteList.length).toBeGreaterThanOrEqual(1);
  }); it("should remove a created post from the array of posts", () => {
    service.addNewQuote("This is my first post");
    service.removeQuote(0);
    expect(service.quoteList.length).toBeLessThan(1);
  });
});
```

在第一个块`beforeEach`中，创建了一个`QuoteService`的实例，以确保它只被创建一次，并避免在其他块中重复，除了一些例外情况:

```
it("should create a post in an array", () => {
    const qouteText = "This is my first post";
    service.addNewQuote(qouteText);
    expect(service.quoteList.length).toBeGreaterThanOrEqual(1);
  });
```

第一个块通过检查数组的长度来测试 post 模型`QuoteModel(text, date)`是否被创建到一个数组中。`quoteList`的长度预计为`1`:

```
it("should remove a created post from the array of posts", () => {
    service.addNewQuote("This is my first post");
    service.removeQuote(0);
    expect(service.quoteList.length).toBeLessThan(1);
  });
```

第二个块在数组中创建一个 post，并通过调用服务对象中的`removeQuote`立即删除它。`quoteList`的长度预计为`0`。

# 如何测试角度组件

在我们的角度单元测试示例应用程序中，`service`被注入到`QuoteComponent`中以访问其属性，这是视图所需要的:

```
import { Component, OnInit } from '@angular/core';
import { QuoteService } from '../service/Quote.service';
import { QuoteModel } from '../model/QuoteModel';@Component({
  selector: 'app-Quotes',
  templateUrl: './Quotes.component.html',
  styleUrls: ['./Quotes.component.css']
})
export class QuotesComponent implements OnInit { public quoteList: QuoteModel[];
  public quoteText: String = null; constructor(private service: QuoteService) { } ngOnInit() {
    this.quoteList = this.service.getQuote();
  } createNewQuote() {
    this.service.addNewQuote(this.quoteText);
    this.quoteText = null;
  } removeQuote(index) {
    this.service.removeQuote(index);
  }
}<div class="container-fluid">
  <div class="row">
    <div class="col-8 col-sm-8 mb-3 offset-2">
      <div class="card">
        <div class="card-header">
          <h5>What Quote is on your mind ?</h5>
        </div>
        <div class="card-body">
          <div role="form">
            <div class="form-group col-8 offset-2">
              <textarea #quote class="form-control" rows="3" cols="8" [(ngModel)]="quoteText" name="quoteText"></textarea>
            </div>
            <div class="form-group text-center">
              <button class="btn btn-primary" (click)="createNewQuote()" [disabled]="quoteText == null">Create a new
                quote</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div> <div class="row">
    <div class="card mb-3 col-5 list-card" id="quote-cards" style="max-width: 18rem;" *ngFor="let quote of quoteList; let i = index"
      (click)="removeQuote(i)">
      <div class="card-body">
        <h6>{{ quote.text }}</h6>
      </div>
      <div class="card-footer text-muted">
        <small>Created on {{ quote.timeCreated }}</small>
      </div>
    </div>
  </div>
</div>
```

`describe`容器中的前两个程序块连续运行。在第一个块中，`FormsModule`被导入到配置测试中。这确保了可以使用表单的相关指令，如`ngModel`。

同样，`QuotesComponent`在`configTestMod`中声明，类似于组件在`appModule`文件中的`ngModule`中声明。第二块`creates` a `QuoteComponent`及其`instance`，将被其他块使用:

```
let component: QuotesComponent;
  let fixture: ComponentFixture<QuotesComponent>; beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [FormsModule],
      declarations: [QuotesComponent]
    });
  }); beforeEach(() => {
    fixture = TestBed.createComponent(QuotesComponent);
    component = fixture.debugElement.componentInstance;
  });
```

此块测试所创建的组件实例是否已定义:

```
it("should create Quote component", () => {
    expect(component).toBeTruthy();
  });
```

注入的服务处理所有操作的操作(`add`、`remove`、`fetch`)。`quoteService`变量保存注入的服务(`QuoteService`)。此时，在调用`detectChanges`方法之前，组件尚未呈现:

```
it("should use the quoteList from the service", () => {
    const quoteService = fixture.debugElement.injector.get(QuoteService);
    fixture.detectChanges();
    expect(quoteService.getQuote()).toEqual(component.quoteList);
  });
```

现在让我们测试一下我们是否能成功创建帖子。组件的属性可以在实例化时访问，所以当一个值被传递到`quoteText`模型时，呈现的组件检测到新的变化。`nativeElement`对象提供了对呈现的 HTML 元素的访问，这使得检查添加的`quote`是否是呈现文本的一部分变得更加容易:

```
it("should create a new post", () => {
    component.quoteText = "I love this test";
    fixture.detectChanges();
    const compiled = fixture.debugElement.nativeElement;
    expect(compiled.innerHTML).toContain("I love this test");
  });
```

除了可以访问 HTML 内容之外，您还可以通过元素的 CSS 属性来获取元素。当`quoteText`模型为空或 null 时，按钮将被禁用:

```
it("should disable the button when textArea is empty", () => {
    fixture.detectChanges();
    const button = fixture.debugElement.query(By.css("button"));
    expect(button.nativeElement.disabled).toBeTruthy();
  });it("should enable button when textArea is not empty", () => {
    component.quoteText = "I love this test";
    fixture.detectChanges();
    const button = fixture.debugElement.query(By.css("button"));
    expect(button.nativeElement.disabled).toBeFalsy();
  });
```

就像我们用 CSS 属性访问元素一样，我们也可以通过类名访问元素。使用`By e.g By.css(‘.className.className’)`可以同时访问多个类。

通过调用`triggerEventHandler`来模拟按钮点击。必须指定`event`类型，在本例中是 click。点击时，显示的报价将从`quoteList`中删除:

```
it("should remove post upon card click", () => {
    component.quoteText = "This is a fresh post";
    fixture.detectChanges(); fixture.debugElement
      .query(By.css(".row"))
      .query(By.css(".card"))
      .triggerEventHandler("click", null);
    const compiled = fixture.debugElement.nativeElement;
    expect(compiled.innerHTML).toContain("This is a fresh post");
  });
```

# 如何在 Angular 中测试异步操作

不可避免的是，你最终需要远程获取数据。此操作最好被视为异步任务。

`fetchQoutesFromServer`表示一个异步任务，它在两秒钟后返回一组引号:

```
fetchQuotesFromServer() {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve([new QuoteModel("I love unit testing", "Mon 4, 2018")]);
      }, 2000);
    });
  }
```

`spyOn`对象模拟`fetchQuotesFromServer`方法如何工作。它接受注入组件的两个参数`quoteService`和`fetchQuotesFromServer`方法。`fetchQuotesFromServer`有望回报承诺。`spyOn`将使用`and`的方法与使用`returnValue`返回的假承诺调用链接起来。因为我们想要模拟`fetchQuotesFromServer`的工作方式，所以我们需要传递一个`promise`来解析一个报价列表。

正如我们之前所做的，我们将调用`detectChanges`方法来获取更新的更改。`whenStable`允许访问所有`async` 任务完成后的结果:

```
it("should fetch data asynchronously", async () => {
    const fakedFetchedList = [
      new QuoteModel("I love unit testing", "Mon 4, 2018")
    ];
    const quoteService = fixture.debugElement.injector.get(QuoteService);
    let spy = spyOn(quoteService, "fetchQuotesFromServer").and.returnValue(
      Promise.resolve(fakedFetchedList)
    );
    fixture.detectChanges();
    fixture.whenStable().then(() => {
      expect(component.fetchedList).toBe(fakedFetchedList);
    });
  });
```

# 使用 [LogRocket](https://www2.logrocket.com/angular-performance-monitoring) 确保角度异步操作在生产中成功。

调试 Angular 应用程序可能很困难，尤其是当用户遇到难以重现的问题时。如果你对监控和跟踪生产中所有用户的角度状态和动作感兴趣，[试试 LogRocket](https://www2.logrocket.com/angular-performance-monitoring) 。

![](img/2175f50cbf2bbebcca019fbb29f0e0c0.png)

[https://logrocket.com/signup/](https://www2.logrocket.com/angular-performance-monitoring)

LogRocket 就像是网络应用程序的 DVR，记录你网站上发生的一切，包括网络请求、JavaScript 错误等等。您可以汇总并报告问题发生时应用程序的状态，而不是猜测问题发生的原因。

LogRocket NgRx 插件将角度状态和动作记录到 LogRocket 控制台，为您提供导致错误的环境，以及出现问题时应用程序的状态。

# 结论

Angular 确保在浏览器中查看测试结果。这将更好地显示测试结果。

![](img/e18a9cdb89f1b050106566a9b1c19ae4.png)

Test Result

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*******

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***