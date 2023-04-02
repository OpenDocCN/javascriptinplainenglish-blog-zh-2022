# 为什么不用 Shape 作为 TypeScript 接口的后缀？

> 原文：<https://javascript.plainenglish.io/why-not-suffix-typescript-interfaces-with-shape-c251e1d0d878?source=collection_archive---------8----------------------->

## 都是关于描述物体的形状

![](img/60e4fbf1cca99bb072b9bac12c851c31.png)

Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/shapes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

嘿，web devs，再次欢迎来到使用现代语言的面向对象编程的世界。我们正在讨论顶尖的软件设计模式和开发技术，它们肯定会让你得到一份理想的工作。请记住，我们正在从头开始构建 OOP 国际象棋代码库。

如果你想了解更多，请点击下面的链接。

[](https://medium.com/geekculture/why-typescript-and-php-are-good-friends-964360fb75f6) [## 为什么 TypeScript 和 PHP 是好朋友

### 完整指南

medium.com](https://medium.com/geekculture/why-typescript-and-php-are-good-friends-964360fb75f6) 

PHP 和 TypeScript 之间的另一个显著区别是，当涉及到函数和类方法中的类型提示对象时，前者没有那么严格。在 PHP 中，在访问对象的属性之前，不需要显式定义对象的形状，而在 TypeScript 中则不是这样。

我想说 TypeScript 比 PHP 的类型更强是公平的。

[](https://medium.com/codex/php-became-strongly-typed-66f2b2ae917) [## PHP 变成了强类型

### 随着时间的推移逐渐更新

medium.com](https://medium.com/codex/php-became-strongly-typed-66f2b2ae917) 

下面的例子是一个非常有效的 PHP 代码。

在给定一个`$move`对象的情况下，`Chess\Board`类中的`pickPiece()`方法旨在从棋盘上选取一个棋子。棋步将由`Chess\PGN\Move`类中的`toObj()`方法返回，然后作为参数传递给`pickPiece()`。请注意，对象的属性(`color`、`id`、`sq`)是在`pickPiece()`方法中访问的。

为了进一步说明，让我们看一个 PGN 运动如何转换成物体的例子。

```
$move = \Chess\PGN\Move::toObj('w', 'e4');var_dump($move);
```

下面描述的是 PHP `stdClass`格式的*白棋 e4* 。

```
object(stdClass)#6 (7) {
  ["pgn"]=>
  string(2) "e4"
  ["isCapture"]=>
  bool(false)
  ["isCheck"]=>
  bool(false)
  ["type"]=>
  string(27) "[a-h]{1}[1-8]{1}[\+\#]{0,1}"
  ["color"]=>
  string(1) "w"
  ["id"]=>
  string(1) "P"
  ["sq"]=>
  object(stdClass)#5 (2) {
    ["current"]=>
    string(1) "e"
    ["next"]=>
    string(2) "e4"
  }
}
```

这是打字稿的风格。

如你所见，在 TypeScript 版本中，`move`参数必须被类型提示为`MoveShape`，否则如果类型提示为`object`，编译器将报错`TS2339`和`TS2345`。

为了修复错误，人们可能会尝试将类型提示`move`输入为`any`，这并不方便。根据 [TypeScript 的注意事项](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html) , `any`不应该作为类型使用，除非您正在将 JavaScript 项目迁移到 TypeScript。

# 最好描述得更详细些

在 TypeScript 中，像`MoveShape`这样的自定义类型可以用类型别名或接口来创建。问题是，如果你决定采用基于接口的解决方案，你将面临一个两难的境地。

根据微软的编码[准则，TypeScript](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines) `I`不应该用作接口名称的前缀。同样， [Google 建议](https://google.github.io/styleguide/tsguide.html#naming-style)不要特别标记界面，如`IMove`或`MoveInterface`，而是更具描述性，使用一个描述界面内容的后缀。

# 那么如何命名一个接口呢？

TypeScript 的接口命名约定听起来可能令人困惑。

其他编程语言可以在接口名称前加前缀或后缀一个通用名称，PHP 就是这种情况，接口应该总是以`Interface`作为后缀。

[](https://www.php-fig.org/bylaws/psr-naming-conventions/) [## PSR 命名惯例- PHP-FIG

### 我们是一群已经建立的 PHP 项目，他们的目标是谈论我们项目之间的共性，并找到方法…

www.php-fig.org](https://www.php-fig.org/bylaws/psr-naming-conventions/) 

但是一切都比看起来简单！我决定在 TypeScript Chess 中引入一个新的命名约定。

[](https://github.com/chesslablab/ts-chess) [## GitHub-chess lab/ts-chess:一个用于 TypeScript 的国际象棋库。

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/chesslablab/ts-chess) 

在这里。描述对象形状的界面现在以单词`Shape`作为后缀。顺便说一下，这是一件很常见的事情。因此，如果您找到一个以`Shape`后缀结尾的文件名，那只不过是对域数据的描述。

毕竟，数据形状代表模型中的数据。同样的事情也适用于`PieceShape`。如果你读了我以前的帖子，你可能知道`Board.ts`基本上是一个对象存储(一个类型脚本映射),包含以前用面向对象方法设计的棋子。

[](https://blog.devgenius.io/how-to-iterate-over-a-typescript-map-c62ca11cc69c) [## 如何迭代 TypeScript 映射

### 并在不使用 forEach 循环的情况下返回值

blog.devgenius.io](https://blog.devgenius.io/how-to-iterate-over-a-typescript-map-c62ca11cc69c) 

再说一次，编写像`getPieceBySq()`这样的方法是很常见的，它用代数符号给出一个特定的正方形，返回占据这个正方形的棋子。

如果找到一个棋子——一个地图元素——将返回一个类型为`PieceShape`的对象，如下图所示。

我希望这是不言自明的，对任何从事代码库工作的开发人员都有意义。

那么，当涉及到描述对象的形状时，你对用单词`Shape`作为 TypeScript 接口的后缀有什么看法？你觉得这种命名约定比用`Interface`作为后缀更具描述性吗？

请在下面的评论区告诉我。

非常感谢您的阅读！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***