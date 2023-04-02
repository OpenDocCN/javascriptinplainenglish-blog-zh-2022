# 如何使用 Web 客户端存储

> 原文：<https://javascript.plainenglish.io/a-better-way-to-work-with-web-client-storage-70387443b4cb?source=collection_archive---------15----------------------->

## 使用 web 客户端存储的更好方式

![](img/af0cef0d9eae9a53f409240d3190ff6d.png)

Photo by [Artem Maltsev](https://unsplash.com/@art_maltsev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览器配备了存储选项，可以帮助您管理客户端上的数据，以最大限度地减少对服务器的调用，甚至在您的应用程序中提供离线体验。有些应用程序甚至会先从服务器加载数据，然后不需要调用服务器就可以运行。

问题不在于您是否需要处理客户端存储选项，而在于何时处理。然而，当你跳入这个世界时，一些问题出现了:

*   每个都有自己的 API，有些很冗长；
*   每一种都有其数据类型限制，这意味着不是所有的数据类型都可以存储；
*   您可能需要使用不同的选项，因为并非所有的浏览器类型和版本都支持所有的存储选项；
*   您可能需要管理数据格式、验证和类型，以确保数据以一致的方式存储，从而防止应用程序级别的数据检查。
*   你很可能需要一个库来帮助你，但是找到一个能解决你所有或大部分问题的库可能是一项艰巨的任务。

## 进入“客户端-网络-存储”包

“ [*客户端-网络-存储*](https://github.com/beforesemicolon/client-web-storage) ”是一个很有前途的解决方案，因为:

*   它提供了一个简单的 API 来处理所有的客户端存储选项: *IndexedDb、WebSQL、LocalStorage，以及 in Memory*；
*   它自动回退到不同的选项，保证您的数据将被正确地存储在客户端；
*   支持一长串数据类型:`Date, Number, String, Boolean, Array, **ArrayBuffer**, **Blob**, Float32Array, Float64Array, Int8Array, Int16Array, Int32Array, Uint8Array, Uint8ClampedArray, Uint16Array, Uint32Array`；
*   它为你做基本的数据验证；
*   提供模式支持，保证数据格式。它会自动为您创建具有默认值的字段；
*   为您的服务器 API 通信提供挂钩，以便您只与数据存储进行交互，而所有 API 通信都在后台进行；
*   它提供了一个难以置信的简单的 API 来做所有的事情；
*   允许架构嵌套创建复杂的存储区；

## 它是如何工作的？

它允许您通过模式定义来定义具有特定数据格式的小文档。这是你告诉它数据是什么样子的，以及它应该如何进行验证的方式。让我展示给你看:

假设我有一个 TypeScript 项目，所以我需要为我的数据定义类型:

```
interface User extends **Schema.DefaultValue** {
    name: string;
}

interface ToDo extends **Schema.DefaultValue** {
    name: string;
    description: string;
    complete: boolean;
    user: User;
}
```

上面我定义了一个`User`和一个`ToDo`，它们扩展了定义字段`id`、`createdDate`和`lastUpdatedDate`的`Schema.DefaultValue`，这些字段是自动为您处理的重要数据字段。它将为您生成`uuid`,并在您做出更改时更新`lastUpdatedDate`字段。

## 定义模式

由此我可以定义我的模式，我还可以向它添加类型:

```
const **userSchema** = new **Schema**<**User**>("user", {
   name: new **SchemaValue**(String, true),
});const **todoShema** = new **Schema**<**ToDo**>("todo", {
   name: new **SchemaValue**(String, true),
   description: new **SchemaValue**(String, false, "No Description"),
   complete: new **SchemaValue**(Boolean),
})
```

上面我定义了一个带有必填名称字段的用户模式:

```
**new SchemaValue(type, isRequired, defaultValue)**
```

然后，我定义了一个 todo 模式，其中还包含一个必需的 name 字段和一个可选的 description 字段，当没有提供值时，description 字段将具有默认值`No Description`，最后是一个 boolean `complete`字段，用于指示 todo 项是否已完成。

我可以用模式做的一件很酷的事情是自动生成一个带有默认值的基本数据对象:

```
**const todo1 = todoShema.toValue();***/** **todo1** *{
  id: "123e4567-e89b-12d3-a456-426614174000",
  name: "",
  description: "No Description",
  complete: false,
  createdDate: "January, 4th 2022",
  lastUpdatedDate: "January, 4th 2022",
}
 */*
```

它将创建一个`uuid`，为我在模式中定义的字段添加日期并使用默认值。

## 创建数据存储

当你创建自己的商店时，奇迹就发生了。

```
const **todoStore** = new **ClientStore**<ToDo>("todos", **todoSchema**)
```

这是创建接受所有默认值的商店的最简单形式。这意味着它处理版本控制、存储类型、回退、创建、优化等。

我也可以选择提供我的配置，有 4 个选项:

```
const **todoStore** = new **ClientStore**<ToDo>("todos", **todoSchema**, {
    **appName**: "My Todo App",
    **version**: 1, *// changes when configuration or schema changes*
    **type**: **ClientStore.Type.LOCALSTORAGE**,
    **description**: "manages user todos"
})
```

上面我正在创建我的 todo 存储的第一个版本，我将它定义为一个`LOCALSTORAGE` 类型。

我还可以提供一个类型列表，作为它的备用类型:

```
**type**: [
  **ClientStore.Type.**INDEXEDDB**,
  ClientStore.Type.**LOCALSTORAGE**,
  ClientStore.Type.**MEMORY_STORAGE],
```

以上意思是，根据浏览器支持从`INDEXEDDB`到`MEMORY_STORAGE`开始尝试这些存储选项。

商店为你做了很多。它将在加载时读取客户端存储(如果它们存在)，填充所有内容并准备好供您与之交互。该存储是 100%异步的，这很有帮助。

## 弄脏商店

创建一个项目非常简单。我不必提供所有的值。我可以只提供默认值，其余的是自动填充的:

```
const **todo1** = await **todoStore**.**createItem**({
    name: "Go Shopping", // name is required
});

*/* Will create item
{
  id: "123e4567-e89b-12d3-a456-426614174000",
  name: "Go shopping",
  description: "No Description",
  complete: false,
  createdDate: "January, 4th 2022",
  lastUpdatedDate: "January, 4th 2022",
}
 */*
```

它还将根据我定义的类型和模式数据类型来验证数据。例如，执行以下操作将会失败:

```
**todoStore**.**createItem**({});
**todoStore**.**createItem**({name: 12});
**todoStore**.**createItem**({*complete*: "yes"});
```

它为我做类型检查和字段需求检查。它还尽可能地为我过滤和映射数据。

```
const todo = fetchSingleTodo("984728374834");**todoStore**.**createItem**(todo);
```

如果从 API 返回的数据有更多或更少它需要的字段，它将总是只添加它需要的字段，当字段名在您提供的数据中不存在时，将返回默认值。

更新商店是一个类似的过程:

```
const **todo1** = await **todoStore**.**createItem**({
    name: "Go Shopping",
});await **todoStore**.**updateItem(todo1.id, {
  complete: true
})**
```

一般来说，它只支持下面的 CRUD 和搜索**异步**动作:`createItem, updateItem, getItem, getItems, loadItems, removeItem, clear, findItem, findItems`。

## 商店挂钩

有可能知道并拦截对商店所做的一切。

您可以向商店订阅更新:

```
const **unsub** = **todoStore**.**subscribe**((eventType, details) => {
    switch (eventType) {
      case **ClientStore.EventType.READY**: 
        // handle event type here
        break;
      case **ClientStore.EventType.CREATED**: 
        // handle event type here
        break;
      case **ClientStore.EventType.UPDATED**: 
        // handle event type here
        break;
      case **ClientStore.EventType.ABORTED**: 
        // handle event type here
        break;
      case **ClientStore.EventType.CLEARED**: 
        // handle event type here
        break;
      case **ClientStore.EventType.DELETED**: 
        // handle event type here
        break;
      case **ClientStore.EventType.ERROR**: 
        // handle event type here
        break;
      default:
    }
})

**unsub()** // call to unsubscribe from the store
```

您提供的订阅处理程序是用事件类型和该操作类型产生的数据调用的。

您还可以在存储发生之前拦截操作，甚至中止它们，使它们不会发生。对于您的服务器 API 处理来说，这是一个完美的钩子。

```
const **unsub** = **todoStore**.**beforeChange**(async (eventType, data) => {
    switch (eventType) {
        case **ClientStore.EventType.CREATED**:
            *await todoService.****createTodo****(data);*
            break;
        case **ClientStore.EventType.UPDATED**:
            *await todoService.****updateTodo****(data.id, data);*
            break;
        case **ClientStore.EventType.DELETED**:
            *await todoService.****updateTodo****(data);*
            break;
        case **ClientStore.EventType.CLEARED**:
            *await todoService.****deleteAllByIds****(data);*
            break;
        default:
    };

    **return true;**
});

**unsub**();
```

您可以返回 true 或 false 来决定是否更新存储，这将发送一个可以在订阅处理程序中捕获的`ABORT`事件。

您也可以抛出错误或者让您的 API 失败，商店将捕获并广播一个`ERROR`事件，您也可以在订阅处理程序中捕获该事件。

## 更复杂的数据

该模式的一个优点是，您可以嵌套它们以形成复杂的存储。

例如，我们可以将用户模式嵌套到 todo 模式中。

```
// Schema TS type
interface **User** extends Schema.DefaultValue {
    name: string;
}

interface **ToDo** extends Schema.DefaultValue {
    name: string;
    description: string;
    complete: boolean;
    **user: User;**
}

// denife schemas
const userSchema = new Schema<User>("user");
const todoSchema = new Schema<ToDo>("todo");

userSchema.defineField("name", String, {required: true});

todoShema.defineField("name", String, {required: true});
todoShema.defineField("description", String);
todoShema.defineField("complete", Boolean);
**todoShema.defineField("user", userSchema, {required: true});**

// create stores
const userStore = new ClientStore<User>("users", userSchema);
const todoStore = new ClientStore<ToDo>("todos", todoSchema);
```

那么创建一个项目看起来应该是这样的:

```
// you can create a new on or get it from the store
const **AdminUser** = await userStore.createItem({
    name: "John Doe"
});

const todo1 = await todoStore.createItem({
    name: "Go Shopping",
    **user: AdminUser**
});

*/* Will create item
{
  id: "123e4567-e89b-12d3-a456-426614174000",
  name: "Go shopping",
  description: "No Description",
  complete: false,* ***user: {
    id: 3483748929e82382,
    name: "John Doe",
    createdDate: "January, 4th 2022",
    lastUpdatedDate: "January, 4th 2022",
  }* ***
  createdDate: "January, 4th 2022",
  lastUpdatedDate: "January, 4th 2022",
}
 */*
```

存储将根据架构定义对数据进行深度评估，因此以下操作将失败:

```
*// missing* ***required*** *user*
**await todoStore.createItem({name: "Buy shoes"});***// missing* ***required*** *user name* **await todoStore.createItem({name: "Buy shoes", user: {}});**
```

## 减去

这个解决方案省去了您在客户端处理数据的所有麻烦。它用相同的 API 接口处理许多存储选项，这是一个巨大的优势。在数据之上，它支持从简单到复杂的数据类型、数据格式，并通过惊人的挂钩进行验证，以真正做到最好。

[看看吧](https://github.com/beforesemicolon/client-web-storage)，在评论中告诉我你的想法:

[](https://github.com/beforesemicolon/client-web-storage) [## GitHub-before 分号/client-we B- storage:indexed db、WebSQL 的浏览器存储接口…

### 用于 IndexedDB、WebSQL、LocalStorage 的浏览器存储接口，以及带有模式和数据验证器的内存数据。…

github.com](https://github.com/beforesemicolon/client-web-storage) ![](img/79122679204c8ac0aa65ca22857737ab.png)

**YouTube 频道** : [分号前](https://www.youtube.com/channel/UCrU33aw1k9BqTIq2yKXrmBw)
**网站**:[beforesemicolon.com](https://beforesemicolon.com/)