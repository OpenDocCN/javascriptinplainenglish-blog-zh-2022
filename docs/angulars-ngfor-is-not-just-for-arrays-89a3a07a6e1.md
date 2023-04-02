# Angular 的 ngFor 不仅仅用于数组

> 原文：<https://javascript.plainenglish.io/angulars-ngfor-is-not-just-for-arrays-89a3a07a6e1?source=collection_archive---------0----------------------->

## 关于`ngFor`指令及其所有特性(如`trackBy`等)的指南。

![](img/90933ee22e64d951b8f3c3fb7d092020.png)

Photo by [Tomáš Malík](https://unsplash.com/@malcoo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用`*ngFor`指令，一个 HTML 模板的一部分为一个可迭代列表(集合)中的每一项重复一次。与 AngularJS 中的`ngRepeat`类似，`ngFor`是 Angular 的结构指令。`ngFor`指令导出一些局部变量，如 Index、First、Last、odd 和 even。

修改 DOM 的结构，因为它是一个结构指令。

它的目的是为数组中的每个值重复运行一个预定的 HTML 模板，每次发送数组值作为任何字符串插值或绑定的上下文。

## 我们可以用`ngFor`做什么？

我们可以使用基本指令`ngFor`在 HTML 模板中创建数据表示列表和表格。让我们以下面的信息为例:

```
const HEROES= [
    {id: 1, name:'Superman'},
    {id: 2, name:'Batman'},
    {id: 5, name:'BatGirl'},
    {id: 3, name:'Robin'},
    {id: 4, name:'Flash'}
];
```

通过创建类似这样的 HTML，我们可以使用`ngFor`在屏幕上以数据表的形式打印这些数据:

```
<table>
    <thead>
        <th>Name</th>
    </thead>
    <tbody>
      <tr>
           <td>Superman</td>
       </tr>
       <tr>
           <td>Batman</td>
       </tr>
       ...
       </tbody>
</table>
```

## `ngFor`的语法是什么？

让我们构建一个与`ngFor`一起使用的组件，这样我们就可以有一个功能性的 HTML 模板:

```
@Component({
    selector:'heroes',
    template: `
    <table>
        <thead>
            <th>Name</th>
            <th>Index</th>
        </thead>
        <tbody>
            <tr *ngFor="let hero of heroes">
                <td>{{hero.name}}</td>
            </tr>
        </tbody>
    </table>
`
})
export class Heroes {

    heroes = HEROES;

}
```

## 对扩展您的软件启动感兴趣吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们刚刚显示的 HTML 表将由这个模板生成。这个例子显示了使用`ngFor`的(最典型的)语法:

*   我们正在为`ngFor`提供一个迭代表达式
*   Javascript 语法后面是使用关键字`let`来定义循环变量`hero`
*   该表达式遵循 Javascript `of`迭代功能，并采用`var i of items`的形式

## 可变能见度

请记住，循环变量`hero`只能在循环中访问；在`ngFor`部分之外是不可访问的。

## 要注意的常见`ngFor`错误

如果您来自 AngularJs 背景，在您习惯新的 Angular 语法之前，以下错误会出现几次:

```
Can't bind to 'ngFor' since it isn't a known property of 'tr'
```

您可能无意中键入了`item in items`而不是`item of items`，或者忘记在语句的开头包含`let`关键字，这就是发生这种情况的原因:

```
<tr *ngFor=" hero in heroes">
    <td>{{hero.name}}</td>
</tr>
```

## 查找列表元素的索引

添加列表元素的数字索引位置是一个非常典型的需求。使用`index`变量，我们可以确定元素的当前索引:

```
 <tr *ngFor="let hero of heroes; let i = index">
    <td>{{hero.name}}</td>
    <td>{{i}}</td>
</tr>
```

要获得索引的值，注意必须使用`let`关键字；否则，您将收到类似以下内容的错误:

```
Parser Error: Unexpected token = at column ...
```

经过这一修改，现在生成的 HTML 如下所示:

```
<table>
    <thead>
        <th>Name</th>
        <th>Index</th>
    </thead>
    <tbody>
      <tr>
           <td>Superman</td>
           <td>0</td>
       </tr>
       <tr>
           <td>Batman</td>
            <td>1</td>
       </tr>
       ...
       </tbody>
</table>
```

## 如何使用`even`和`odd`对表格进行分条

通过向偶数或奇数行添加不同的 CSS 类来对表进行条带化的能力是创建表时另一个经常需要的特性。

假设我们想在上表中添加一个 CSS 类`even`，如果是偶数行，添加一个 CSS 类`odd`。

我们有两个变量——`even`和`odd`——可以在使用`ngClass`的下列组合中使用，以实现这一点:

```
<tr *ngFor="let hero of heroes; let even = even; let odd = odd" 
    [ngClass]="{ odd: odd, even: even }">
    <td>{{hero.name}}</td>
</tr>
```

让我们看看这个模板生成的 HTML:

```
<table>
        <thead>
            <th>Name</th>
        </thead>
        <tbody>
            <tr class="even">
                <td>Superman</td>
            </tr>
            <tr class="odd">
                <td>Batman</td>
            </tr>
            ...
        </tbody>
    </table>
```

我们可以看到，正如预期的那样，`ngClass`将 CSS 类添加到了右边的行中。

## 识别列表的`first`和`last`元素

除了偶数和奇数功能之外，还有两个附加变量可用于确定列表的第一个和最后一个元素:

```
<tr *ngFor="let hero of heroes; let first = first; let last = last" 
    [ngClass]="{ first: first, last: last }">
    <td>{{hero.name}}</td>
</tr>
```

这会将名为`first`的 CSS 类添加到列表的第一个元素中，并将名为`last`的 CSS 类添加到列表的最后一个元素中:

```
<table>
    <thead>
        <th>Name</th>
    </thead>
    <tbody>
      <tr class='first'>
           <td>Superman</td>
       </tr>
       ...
      <tr class='last'>
           <td>Flash</td>
       </tr>      
       </tbody>
</table>
```

## 当我们在列表中添加或删除元素时`ngFor`是如何工作的？

随着输入列表的改变，`ngFor`将努力避免重复创建和销毁列表的 DOM 元素，因为这样做是一个昂贵的过程。此外，传递给`ngFor`的新列表不一定需要完全重建列表的 DOM。

对列表中的每个元素独立地做出决定。许多现有的 DOM 元素将被重用，只有其中的一些值将被覆盖。

因为，例如，如果我们以不同的顺序传入一个新的列表，Angular 将尝试识别元素并重新排序列表中的 DOM 元素，而不删除和重新创建它们，所以 Angular 有必要唯一地识别每个列表元素，以便做出决定。

## 默认情况下如何跟踪列表项？

默认情况下，`ngFor`使用对象标识来跟踪列表项。这意味着，如果您从与前一个列表完全相同的值开始创建一个全新的对象列表，并将这个新创建的列表提供给`ngFor`，Angular 将无法检测特定的列表项目是否已经存在。

从对象标识的角度来看，新列表中的元素与旧列表中的元素完全不同。例如，如果我们从后端重新查询数据，就会出现这种情况。

由于 Angular 缺乏关于对象的知识，默认情况下最好通过对象标识进行跟踪，因为它无法确定使用哪个属性进行跟踪。

## 为什么这对性能很重要？

正如我们所见，`ngFor`已经默认执行了许多优化，试图尽可能多地重用现有的 DOM 元素，但是它将这些优化基于对象标识。

即使进行了这些更改，我们仍然会遇到性能问题，并且会注意到，对于包含巨大列表的模板，或者由于大量 DOM 元素被创建和销毁而占据了屏幕很大一部分的列表，UI 会很慢。

如果是这种情况，我们可以设置`ngFor`使用不同于对象识别的方法来跟踪对象。

## 如何使用`trackBy`？

使用`trackBy`，我们可以创建自己的系统来跟踪列表中的项目。必须向`trackBy`传递一个将索引和当前选择的项目作为参数的方法:

```
@Component({
    selector:'heroes',
    template: `
    <table>
        <thead>
            <th>Name</th>
        </thead>
        <tbody>
            <tr *ngFor="let hero of heroes; trackBy: trackHero" >
                <td>{{hero.name}}</td>
            </tr>
        </tbody>
    </table>
`
})
export class Heroes {

    heroes = HEROES;

    trackHero(index, hero) {
        console.log(hero);
        return hero ? hero.id : undefined;

    }

}
```

跟踪将使用这个实现的`id`属性来执行。

## 何时使用 trackBy？

利用`trackBy`是因为它是一种性能优化，默认情况下通常不需要，理论上，只有出现性能问题时才需要。

如果您使用过时的移动浏览器，考虑在较大的表格中使用`trackBy`作为预防措施，但这实际上取决于您的系统和用例。

## `ngFor`只针对数组吗？

在这个例子中，我们已经向`ngFor`发送了一个 Javascript 对象数组，但是这并不是它运行所必需的；我们可以只传递一个对象给`ngFor`。

任何类型的 Javascript Iterable 都可以传递给它，包括框架本身产生的那些。我们将为名为`hero`的配置元素定义一个指令来演示这一点。

```
import {Directive, Input} from "@angular/core";

@Directive({
    selector: 'hero',
})
export class Hero {

    @Input()
    id: number;

    @Input()
    name:string;
}
```

这个配置元素现在可以在我们的模板中以下列方式使用:

```
<heroes>
    <hero id="1" name="Superman"></hero>
    <hero id="2" name="Batman"></hero>
    <hero id="3" name="Batgirl"></hero>
    <hero id="3" name="Robin"></hero>
    <hero id="4" name="Flash"></hero>
    <hero id="5" name="Green Lantern"></hero>
</heroes>
```

现在让我们使用`@ContentChildren`从配置元素中查询该信息:

```
export class Heroes {

     @ContentChildren(Hero)
     heroes: QueryList<Hero>;

}
```

你知道这里发生了什么吗？原来`QueryList`是 Angular 中的一个类，它本身是可迭代的！因此，除了在组件类中以编程方式使用它之外，我们还可以选择将它直接传递给`ngFor`并在那里迭代。

我们程序中的任何其他 iterable 也可以以同样的方式使用。

## 结论

我们已经了解了`ngFor`和它在 Angular 中的特性，以及我们如何在需要的地方改进它的性能。希望对你有用。

```
Want to Connect?

Connect with me on [LinkedIn](https://www.linkedin.com/in/gouravkajal/).
```

感谢阅读！

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*