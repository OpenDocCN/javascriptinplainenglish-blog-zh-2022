# Angular ngTemplateOutlet 指令

> 原文：<https://javascript.plainenglish.io/angular-ngtemplateoutlet-directive-d8c2d3ee1fc9?source=collection_archive---------7----------------------->

## 使用 ngTemplateOutlet 指令，我们可以从准备好的 TemplateRef 中插入一个嵌入式视图。

![](img/494cda86ed2aa0fd7b32698c16b746f4.png)

ngTemplateOutlet directive

ngtemplateeoutlet 被用作可以在多个地方重用的模板的容器。另一个用例，它用于将模板动态地注入到页面中。

# ngTemplateOutlet 的简单用法

首先，我们需要用 ng-template 标签包装我们的内容。默认情况下，ng-template 不呈现任何内容。然后我们需要创建局部变量(使用' # '符号)来创建对模板的引用

```
<ng-template #myTemplate>
 <p>My content</p>
</ng-template>
```

现在我们可以像这样使用我们的内容

```
<ng-container [ngTemplateOutlet]="myTemplate"></ng-container>
```

现在，无论我们在哪里使用 ng-container 代码，我们都会看到*我的内容*输出。但是使用静态内容并不是很有帮助，所以在 ngTemplateOutlet 中，我们也可以通过使用`ngTemplateOutletContext`来传递动态数据

简单的例子

```
<ng-container 
  [ngTemplateOutlet]="myTemplate" 
  [ngTemplateOutletContext]="{text: 'Hello World'}"
></ng-container>
```

现在，要从给定的上下文中访问变量，我们需要使用 **let-*** 关键字。

```
<ng-template #myTemplate let-text="text">
 <p>My content</p>
 <p> Text is: {{ text }} </p>
</ng-template>
```

注意这个语法

```
let-text=”text”
```

这意味着我们创建名为 **text** 的局部变量，该变量的值等于 **context.text** 的值，上下文由**ngTemplateOutletContext**提供

```
let text = context.text
```

我们也可以像这样定义另一个变量名

```
let-dataText="text"
```

在模板内部，我们需要使用`dataText`

```
<ng-template #myTemplate let-dataText="text">
 <p>My content</p>
 <p> Text is: {{ dataText}} </p>
</ng-template>
```

# 缺省值

使用上下文对象中的**$隐式**键会将其值设置为默认值。这意味着我们传递的是整个对象，而不是对象的单独属性。在这个例子中，我们在`ng-template`中创建了`default`变量，它的值等于`component.user`

还有一个将*ngtemplateeutort*与*上下文*一起使用的简短语法:

```
<ng-container 
  *ngTemplateOutlet="myTemplate; context: myData"
></ng-container>
```

# 动态模板

ngTemplateOutlet 的一个好处是我们可以动态地改变模板

```
<button (click)="active = !active">Click</button>
<div 
  [ngTemplateOutlet]="active ? templateRef : templateRef2"
  [ngTemplateOutletContext]="context"
></div>
```

参见[堆栈宽度](https://stackblitz.com/edit/a-ngtemplateoutlet?file=src/app/app.component.html)上的示例

# 内容投影

我们还可以将内容投射到组件中，并通过使用 **TemplateRef 来获取对它的引用。**要在组件中投影内容，我们需要用`ng-template`标签包装内容。

```
<app-menu> // <-- wrapper component
  <ng-template>
    <ul>
      <li>111</li>
      <li>2222</li>
    </ul>
  </ng-template>
</app-menu>
```

在菜单(包装器)组件中，包装在`ng-template`中的代码将显示在`[ngTemplateOutlet]`中。

```
import { TemplateRef, ContentChild} from '[@angular/core](http://twitter.com/angular/core)'
[@Component](http://twitter.com/Component)({
  selector: 'app-menu',
  template: `
    <div>
      <div [ngTemplateOutlet]="templateRef"></div>
    </div>
  `,
})
export class MenuComponent { [@ContentChild](http://twitter.com/ContentChild)(TemplateRef) templateRef: TemplateRef<any>;

}
```

# 调用包装组件函数

为了调用包装组件方法，我们可以创建局部变量(使用`#`符号),该变量将引用组件。示例:

```
<app-list [list]="list" #wrapper (itemAdd)="addNewItem()">
  <ng-template>
    <ul>
      <li *ngFor="let item of list; let i = index">
        {{ item }}
        <button (click)="wrapper.removeItem(i)">x</button>
      </li>
    </ul>
  </ng-template>
</app-list>
```

您可以在 [Stackblitz](https://stackblitz.com/edit/a-ngtemplateoutlet?file=src/app/app.component.html) 上找到示例。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW)**** ***对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。*****