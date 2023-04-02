# fire base 9:angular fire 应用程序的一股新鲜空气

> 原文：<https://javascript.plainenglish.io/firebase-9-a-breath-of-fresh-air-for-the-angularfire-app-c6d80c1260b2?source=collection_archive---------1----------------------->

## 新的树抖动 API 的迁移指南。

![](img/f2dd9206c049afde700dcbe0bb5e3595.png)

AngularFire migration guide to Firebase 9 Modular API

> 💡我做这个指南是为了分享我把复杂的 Firebase app 从 Firebase 8 升级到 Firebase 9 模块化 API 后的个人经验。它将该应用在移动设备上的性能提高了 35%，在桌面上的性能提高了 10%。

Firebase JS SDK 的开发人员做了大量的工作，完全重写了在我们的 web 应用程序中集成和使用 Firebase 库的方式。现在它已经变得不可动摇，更小，并允许我们在需要时动态导入 Firebase 模块。

多亏了这些变化，我们的网络应用程序变得更加轻量级，运行速度也更快。由 AngularFire 支持的 Angular 应用程序也不例外。但是这一次，我们必须处理巨大的重构，以利用树摇摇模块的所有好处。

在本教程中，我们将涵盖:

*   在兼容模式下从 AngularFire 6 迁移到 Angular 7
*   从兼容模式到模块化的迁移策略
*   认证模块:匿名认证、账户链接、电子邮件和社交登录/注册
*   实时数据库:对象、列表、高级查询、在线/离线状态
*   云 Firestore:文档、集合、高级查询

从第一个角度来看，这似乎很难，但是在回顾了几个例子之后，你会发现它是多么的符合逻辑和简单明了。重构将会是一个没有陷阱的单调例行程序。

## 从 AngularFire 6 迁移到 Angular 7

首先，我们需要确保你使用最新的 Firebase 和 AngularFire。检查`package.json`，如果包含 AngularFire 6 或以下，我们需要运行:`ng update @angular/fire`。还有，一定要用 Angular 12+。

现在我们需要替换项目中从`@angular/fire/`到`@angular/fire/compat/`以及从`firebase/`到`firebase/compat/`的所有导入路径。

另外，在`app.module.ts`中提供 Firebase 配置。

```
providers: [
  {
    provide: FIREBASE_OPTIONS,
    useValue: environment.firebase
  }
]
```

在这一步，我们的应用程序应该像以前一样工作。我们可以合并这些更改，甚至在这种模式下部署到 prod，因为它允许我们在切换到 Firebase 9 模块化导入时，缓慢、部分、逐步地迁移，而不会破坏整个应用程序。

# 模块导入

首先，我们要做的是导入 AngularFire 模块:

它是怎样的:

它如何变成:

这是一个最简单的例子。提供这种回调的好处并不明显。但是这是我们可以控制应该装载什么的地方。

例如，你还记得我之前提到的为移动设备加载的`iframe.js`吗？它符合移动社交认证的要求。但是我们可以控制何时加载这个解析器。所以我们可以将它从 app.module.ts 中移除，并在调用`signInWithPopup()`时将其作为参数传递。

*By the way, we can also do better ways to store authentication data later.*

然后我们需要在调用社交登录时提供一个解析器。这里有一个例子:

> 注意，目前由于一些 AngularFire 问题，我们需要从 firebase/auth 导入 signInWithPopup 和 browserPopupRedirectResolver，而不是`@angular/fire/auth`。

# 证明

这是你需要改变的第一件事，因为在兼容模式下， **Firebase 会在应用加载期间在移动设备上加载** `iframe.js`。这将大大降低你在 PageSpeed Insights 上的移动设备性能得分，甚至可能影响你在谷歌搜索结果中的位置。在移动设备上使用 social auth 需要这个 iframe.js。

但是不要担心，在迁移到 Firebase 9 之后，性能会比以前更好，因为只有当用户单击登录按钮时，我们才能加载我们需要的所有内容。

现在我们需要重写使用 AgnularFire auth 方法的逻辑。

情况如何:

```
import { AngularFireAuth } from '@angular/fire/compat/auth';constructor(public afAuth: AngularFireAuth) {}
```

它如何变成:

```
import {Auth} from '@angular/fire/auth';constructor(@Optional() private auth: Auth) {}
```

但在更早的时候，它是 AngularFire 中所有 Auth 方法的类实例。现在，这是一个链接到 Firebase 应用程序的 Auth 模块实例。没有任何方法，它不会加载你不用的东西。

对于新的方法，我们需要单独导入所需的方法。

## 用电子邮件登录

情况如何:

它如何变成:

这是主要的想法。我们导入我们需要的功能，仅此而已。

## 登录社交网络

情况如何:

它如何变成:

> 我非常推荐在调用 signInWithPopup 时提供 browserPopupRedirectResolver，而不是在主线程的 app.module.ts 中加载。

## 匿名登录

就更简单了。它不需要任何重定向解析器。

## 将现有个人资料与社交网站链接

由于重定向解析器的问题(我希望是暂时的)，我们需要从 firebase 而不是 AngularFire 导入它。

> 提醒:如果在 app.module.ts 中简单提供了 auth 模块而没有定制`provideAuth(() => getAuth())`，则不需要提供 browserPopupRedirectResolver。

## 获取用户配置文件

情况如何:

它如何变成:

在授权迁移之后，您可以发现显著的性能改进，尤其是对于移动设备。

# 实时数据库

对于数据库，变化是相同的。之前，我们在数据库实例中有所有的方法。现在，我们应该导入我们需要在应用程序中使用的方法。

情况如何:

```
import { AngularFireDatabase } from '@angular/fire/compat/database';constructor(public db: AngularFireDatabase) {}
```

它如何变成:

```
import { Database } from '@angular/fire/database';constructor(public db: Database) {}
```

和 Auth 实例一样，数据库实例不包含任何查询数据的方法。我们需要分别导入它们。

## 实时数据库获取对象

它是怎样的:

```
this.db.object(`path/to/your/object`)
    .valueChanges()
    .subscribe((data) => {
      // your code
    });
```

它如何变成:

```
import { Database, ref, objectVal } from '@angular/fire/database';objectVal(ref(this.db, `path/to/your/object`))
  .subscribe( data => {
    // Your code
  });
```

如您所见，我们现在需要构建对我们想要获取或编辑的数据库对象的引用。更多的例子在下面。

## 实时数据库获取列表

它是怎样的:

我用了`snapshotChanges`而不是`valueChanges`不是弄错了。早些时候，为了获得能够编辑每个项目的对象列表，我们必须使用`snapshotChages`来获得带有键的快照。然后，我们总是必须将快照映射到带有键的项目数组，就像当前的例子一样。

有了新的 API，它变成了一个内置特性！

它如何变成:

> 新的论点`{ keyField: ‘key’ }`成功了！您可以定义将包含对象键的属性。相同的配置可以用于`objectVal()`。

## 实时数据库查询列表

如你所见，`objectVal`和`listVal`可以接受`ref(this.db, `path/to/your/list`)`作为第一个参数，但是如何对数据进行过滤或排序呢？

还有一个功能——查询。下面是我们如何使用它。

以前是什么样子:

它如何变成:

```
const listRef = ref(this.db, `path/to/your/list`);
const qry = query(listRef, orderByChild('date'));listVal(qry, { keyField: 'key' }).subscribe((onlineList) => {});
```

query()可以接受多个参数，因此我们可以进行更高级的查询:

```
const listRef = ref(this.db, `chats/${this.chatId}`);
const qry = query(listRef, orderByChild('date'), limitToLast(30));listVal<IMessage>(qry).subscribe((chatLog) => {
  // Your code
});
```

## 实时数据库在线/离线状态

为了获得用户的在线状态，我们可以订阅一个. info/connected 对象。

它是怎样的:

它如何变成:

但是当 connected 为 false 时，表示用户已经离线。所以我们不能改变用户的状态。为了处理这个问题，我们使用了`onDisconnect()`函数。

它是怎样的:

```
const ref = this.db.object(`online/${newUser.key}`);
ref.query.ref.onDisconnect().remove();
```

它如何变成:

我只是想说明我们之前使用的所有高级 API 都是可用的，但是应该单独导入。

# Firebase Cloud Firestore

这里的变化与实时数据库相同。首先，这里是对 app.module.ts 的更改。

情况如何:

```
@NgModule({
  imports: [
    AngularFireModule.initializeApp(environment.firebase),
    AngularFirestoreModule.enablePersistence(),
  ]
})
```

它如何变成:

```
@NgModule({
    imports: [
        ...
      provideFirebaseApp(() => initializeApp(environment.firebase)),
        provideFirestore(() => getFirestore()),
    ],
})
```

然后在组件中，我们对所有方法使用单个实例，现在类似于实时数据库，我们使用带有连接细节和单独导入功能的 Firestore 实例。

情况如何:

它如何变成:

要获得带有文档键和元数据的快照，有一个方法`onSnapshot`。

动态加载 Firestore 模块是可能的，但在我的情况下，我在角度特征模块中加载它，对我来说，这是如何加载它的最有角度的方式。但是这里有一个如何实现的官方例子。

## 摘要

您可以通过 project `/compat/` word 进行搜索，以检查迁移是否完全完成。不应该提及旧的进口货。

迁移之后，我的 Angular 项目开始获得比移动版高 35%的 PageSpeed insight 分数。

嗨！非常感谢您阅读我的文章！如果你不是一个媒体成员，想要支持我，你可以通过[点击这个链接](https://golosay.medium.com/membership)来支持我。中型会员将允许你阅读我的帖子和其他人的帖子。再次感谢大家的支持！

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*