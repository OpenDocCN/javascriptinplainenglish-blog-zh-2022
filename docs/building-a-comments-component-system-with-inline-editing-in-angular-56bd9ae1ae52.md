# 使用 Angular 构建带有内嵌编辑的注释组件

> 原文：<https://javascript.plainenglish.io/building-a-comments-component-system-with-inline-editing-in-angular-56bd9ae1ae52?source=collection_archive---------3----------------------->

## 如何在 Angular 中创建注释组件系统的分步指南，该系统具有添加、编辑和删除注释的功能。

![](img/4ee492b7ab8c39e07fe45bee232aa1c8.png)

Photo by [Danial Igdery](https://unsplash.com/@ricaros?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在今天的网络世界中，评论系统是帮助获取用户反馈的最重要的组件之一。通过评论，用户可以对社交媒体帖子做出反应，参与社区讨论，并添加产品或服务评论，这些评论在其他用户购买相同的产品或服务之前可能会对他们有所帮助。

在这篇文章中，我们将一步步来看如何建立一个有效的评论系统。让我们开始吧。

Let’s do this!

首先，我们将创建一个注释接口，我们将使用它来定义特定注释的数据模型。

**comment.model.ts**

Comment model

现在，我们将创建服务来编写所有与评论相关的业务逻辑。

**comment.service.ts**

Comment service

在服务中，我使用预定义的虚拟注释数组。在真实的场景中，这些注释将来自 API。在这种情况下，我们将不得不使用 angular native `HttpClient` API 来使用其不同的 [CRUD 操作](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)方法。

在服务中，我添加了两个方法:一个获取所有评论，另一个发布新评论或更新现有评论。我使用`of` RxJS 操作符将评论数据转换成可观察数据。

> 如果你使用`HttpClient`方法直接从 API 消费数据，你就不必使用`of`操作符，因为默认情况下它们返回一个可观察值。

在方法`postComment`中，我有两个参数。`commentText`是我将作为输入接收的评论，而`commentId`是可选参数，在我编辑现有评论的情况下，我将传递该参数。此外，我正在检查是否定义了`commentId`，添加新的注释或更新现有的注释，最后，返回新的/更新的注释。

现在，让我们开始构建我们的组件。

首先，我们将构建一个显示所有评论列表的组件。

**comments.component.ts**

Commments list component Typescriptfile

在这个组件中，我注入了我们之前创建的`commentService`，这样我们就可以与 API 提供的数据进行通信(在我们的例子中，是虚拟注释列表)。

我创建了一个局部变量`comments$`,它将是一组注释的可观察值。在`ngOnInit()`方法中，我们将使用我们的服务并使用`getAllComments()`方法，然后将返回值赋给`comments$`变量。

现在，让我们为评论列表创建 UI。

**comments.component.html**

Comments list component HTML template

在 HTML 文件中，我们通过使用`async`管道订阅可观察的`comments$`，并将返回值存储在一个名为`comments`的变量中。使用`async`的优点是，当组件被卸载时，它会自动取消对可观察对象的订阅，从而减少内存泄漏的机会。

现在，既然我们有了作为注释数组的`comments`，我们可以使用`ngFor`循环遍历它，并使用`<ul>` HTML 标签创建注释列表。

我在`<li>`标签中使用了`<app-comment>`,这基本上是我们接下来要创建的另一个组件，它将负责显示单个注释以及处理多个操作。

好了，让我们为单个注释创建一个新组件。

**注释.组件. ts**

Single comment component typescript file

这里，我们接受三个输入:单个评论`comment`，所有评论的列表`comments`和特定评论的索引`index`。

此外，我们创建了一个局部变量`isCommentInEditMode`，其默认值为`false`，用于定义当前评论是否处于编辑模式。

首先，有一个方法`editComment()`,它基本上只是将`isCommentInEditMode`的值设置为`true`,因为我们想要编辑我们正在交互的当前评论。

接下来，有一个方法`deleteComment()`基于`index`我们从外部接收到的输入来删除当前的评论，我们相应地调用评论数组列表上的拼接方法来删除选中的评论。

最后，要回到非编辑模式，有一个方法`disableCommentEditMode(isEditMode)`将`isCommentInEditMode`的值设置为我们在方法中作为参数传递的值。

**comment.component.html**

Single comment component HTML template

在注释组件的 HTML 文件中，我们通过作为输入接收到的`<p>`标签中的`comment`对象显示注释文本，以及编辑或删除下面注释的超链接。此外，我们还有另一个组件`app-comment-form`(我们很快就会看到它)，当我们进入编辑模式时，我们将使用它来显示文本框。`isCommentInEditMode`将负责模板中元素的条件渲染。

> **找到窍门了？我们差不多完成了；)**

We are almost there ;)

好吧！我们要做的最后一个组件是`comment-form`,它将负责从用户那里获取评论输入，并将其添加到评论列表中。当我们进入编辑模式时，我们还将使用相同的组件来编辑单个注释。让我们看看它是如何工作的。

**comment-form . component . ts**

Comment form component typescript file

在这个组件中，我们创建了一组输入来接收一个评论列表、一个评论、评论的`index`和`isCommentInEditMode`。我们还注入了`commentsService`来处理发表评论的操作。

在方法`postComment`中，我们有两个参数:`form`和`commentId`(可选)。通过`form`参数，我们将获取用户在文本框中输入的文本。然后，我们将检查表单的有效性和`commentText`的值。

我们还创建了一个类型为`Subscription`的私有变量`postCommentSubscription`，它将存储我们将在组件中使用的所有可观测量及其订阅。它的优点是我们可以退订`postCommentSubscription`而不退订每一个可观察的个体。

**下面我们来详细看看** `postComment()` **的方法**:

我们从`form`值中检索注释文本，然后检查空字符串、`null`或`undefined`的有效性。然后我们在`postCommentSubscription`上使用`add`方法，并在其中调用方法`postComment`，传递两个参数`commentText`和`commentId`，然后订阅它。

在订阅内部，当我们成功接收到刚刚添加的注释时，我们检查是否定义了`index`。它会告诉我们刚刚添加的评论是新评论还是我们正在编辑现有评论，然后我们重置表单。最后，我们还通过将`false`分配给`isCommentInEditMode`来禁用编辑模式。

此外，我们有一个类型为`EventEmitter`的`Output()` `editModeChanged`，它负责与父组件交流关于评论编辑模式的状态。

**comment-form.component.html**

Comment form component HTML template

最后，我们为`comment-form`创建了 HTML 模板，这非常简单。它有一个`form`,在提交时，我们调用`postComment`方法。获取用户输入的`textarea`有一个本地引用`#commentBox`,我们将使用它连接到`ngModel`,并在表单提交时使用它读取文本框值。最后，我们有两个按钮来保存或取消添加/更新评论。

> 对于组件造型，我已经安装了`bootstrap`包。我已经在`styles.css`中导入了`bootstrap.min.css`文件，所以我可以使用 bootstrap 提供的样式类。

# 就是这样！

and we are done! :)

## 试映

Preview of comments component system

我希望这篇文章对你有所帮助，现在你可以在你的应用中轻松创建一个评论系统。

## 谢谢大家！

Thank you!

***更多故事，请在中上*** [***关注我***](https://anishdhingra.medium.com/) ***。***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*