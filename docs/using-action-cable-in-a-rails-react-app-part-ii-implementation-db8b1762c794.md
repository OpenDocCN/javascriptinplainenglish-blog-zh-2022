# 在 Rails/React 应用程序中使用 Action Cable 第二部分:实现

> 原文：<https://javascript.plainenglish.io/using-action-cable-in-a-rails-react-app-part-ii-implementation-db8b1762c794?source=collection_archive---------9----------------------->

![](img/b0436eed017903664a5acf603a6d4879.png)

这篇文章的第一部分讨论了如何配置一个使用 Rails API 后端和 React 前端来处理 Action Cable 的应用程序

第二部分讨论在 Rails/React 应用程序中实际实现 Action Cable

关于 Action Cable 教程，我注意到的一件事是，不管是官方的还是其他的，他们中的许多人试图在某种示例应用程序的上下文中教授 Action Cable，通常是某种聊天应用程序。虽然这对于教程来说是相当标准的做法，但在这种情况下，我觉得有时这只会让事情变得更加混乱。我经常觉得好像有人在教我如何创建一个聊天应用程序，而不是专门教我 Action Cable。有时这意味着我不得不筛选代码行，这些代码不仅与我需要的东西大部分不相关，而且通常是以我不熟悉的方式编写的。将不使用钩子的 React 类组件翻译成使用钩子的函数组件可能是一项需要开发的有用技能，但是当我试图弄清楚 Action Cable 时，这几乎不是我想做的事情。这带来的另一个挑战是，由于所有东西都是作为一个大应用程序的一部分呈现的，所以有时很难将东西分解开来并孤立地识别特定的功能。

如果你喜欢用这种方式学习(我相信很多人都喜欢)，那太好了！有很多很棒的资源，我会在本文的最后将它们链接起来。每个人都是不同的，对一个人有效的方法对另一个人可能更难。如果你像我一样，喜欢把所有的东西都分成小的、独立的部分，那么希望你已经在行动电缆研究中找到了你想要的东西。我将尝试解释每一步，然后也许会为每一步举一个小例子来说明我的意思。我将有意避免过多地解释 Action Cable 到底是什么以及它使用的术语，因为 [Rails Guide](https://guides.rubyonrails.org/action_cable_overview.html) 在不需要我的帮助的情况下做得相当好。如果你对术语不熟悉，我建议你先看看指南，完成后再回来。

# 实施行动电缆:后端

## 建立连接

为了使事情尽可能简单(参考 Rails 指南的[这一节](https://guides.rubyonrails.org/action_cable_overview.html#server-side-components-connections)以获得更深入的解释)，一个连接对象是所有频道订阅的父对象(我们将到达这些，不要惊慌！)用于特定 WebSocket 连接。这使我们能够识别所有订阅的当前消费者。这通常是您对消费者进行身份验证的地方。`Connection`类位于`/app/channels/application_cable/connection.rb`中，看起来像这样:

```
module ApplicationCable
  class Connection < ActionCable::Connection::Base
  end
end
```

设置它以识别当前用户的最简单方法是这样做:

```
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    identified_by :current_user

    def connect
      # I personally used Rails' session hash to identify the current user.
      # There are a number of other ways to do this
      self.current_user = User.find(cookies.encrypted["_session_id"]["user_id"])
    end

  end
end
```

`identified_by :current_user`让您的所有频道都可以访问`:current_user`，这在`connect`中定义。根据您处理 auth 的方式，您可能不需要这样做，所以不要太担心。同样，Rails 指南更详细，请随意探索。

## 频道

在我进入通道之前，快速解释一下什么是流可能是有益的。一个流由一个`string`(或者一个数据库模型的实例，如果您使用的是`stream_for`)表示，它决定了要从特定通道传输的数据。如果我订阅了一个频道，这通常意味着我正在从该频道“流式传输”,并将接收广播到我订阅的流的信息。我们稍后将更多地探索流，包括如何使用`params`个性化流。

不管出于什么原因，我见过的大多数教程都把通道说得比实际更复杂。信道基本上是一种组织你的流和处理它们的订阅者的方法。让一个通道处理多个不相关的流在技术上是可能的，但是这不是一个很好的关注点分离。如果您在一个通道中有一堆不同的流，您的代码将很快变得完全不可读。为了简单起见，我将具体分析一个频道应该包括什么，并让您决定您的应用程序需要多少频道。

创建通道很简单，只需要一个简单的 Rails 生成器:

```
rails g channel example_channel
```

这将在`/app/channels`中创建一个名为`example_channel.rb`的文件，您可能已经猜到了。(出于某种原因，至少对我来说，它还试图重新生成`/app/channels/application_channel`中的默认文件。我不知道它为什么这样做，当提示我决定是否要覆盖原始文件时，我在终端上输入了一个强调的“N”(否)。)这也将在文件本身中生成一些启动代码。它应该是这样的:

```
class ExampleChannel < ApplicationCable::Channel
  def subscribed
    # stream_from "some_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end
```

这些方法实际上做的非常简单。当消费者订阅该频道时，调用`ExampleChannel#subscribed`方法。它应该包括发生这种情况时你想做的任何事情的逻辑。`ExampleChannel#unsubscribed`当消费者退订时调用。就是这样。句号。**这些方法中没有任何东西初始化(或结束)订阅，也不会神奇地向订阅者发送任何信息** *。你让他们做什么，他们就做什么。你可以在`ExampleChannel#subscribed`中输入`puts “Hello World”`，任何时候消费者订阅你的频道，“Hello World”就会被打印到控制台*上，其他什么也不会发生。**

那么这些方法通常包括什么呢？Rails 在自动生成的注释中很好地解释了这一点。当消费者订阅时，您通常会希望通过向他们订阅与该频道相关联的流，来授予他们对将要广播给他们的任何信息的访问权限。这样做很简单:

```
stream_from "example_channel"
```

快速提示:有两种方法可以做到这一点，用`stream_from`和`stream_for`。我将坚持使用`stream_from`，因为我发现它更简单、更容易使用。你可以查看这篇文章来深入探究这种差异。

当用户取消订阅时，您通常想要停止流(通常通过将`stop_all_streams`添加到`ExampleChannel#unsubscribed`)。这是这些方法最基本也是最普遍的用法。根据用户订阅或取消订阅时您需要做的事情，您可能需要向这些方法中添加其他特定于您的应用程序的逻辑，但这取决于您。

您可以在 channel 类中定义的另一个方法是名为`received`的实例方法。每当从订户(前端)发送数据并被服务器接收时，就调用`received`方法。它将该数据作为参数，在方法内部提供对接收数据的访问。让我们用一个例子来说明这一点。假设你有一个聊天应用。您的用户发送一条新消息，您的前端将该消息发送给`ConversationChannel`。您需要将消息保存到数据库中，并在同一个对话中广播给其他人。(通过 POST 请求发送新消息并让您的控制器处理必要的逻辑可能更好(也更传统)，但出于本例的目的，我们将把它发送到通道)。`ConversationChannel#received`最终会变成这样:

```
def received data
  # remember, the data parameter represents whatever is sent from the
  # subscriber, in this case a message object
  message = Message.create(data)
  ActionCable.server.broadcast("conversation_channel", message)
end
```

不要担心最后一行在做什么，我们很快就会开始广播。记住，每次一个新的消息被发送到通道，这个`received`方法将被调用，新的消息作为一个参数被传递。

## 流

当消费者订阅一个频道时，他们从该频道“流式传输”,并将接收广播到该流而不是该频道的信息。这个区别很重要。**信道将订户与流匹配，然而，订户接收的数据取决于流，而不(仅仅)取决于信道。**如果您有个性化的流(通常会有)，同一频道的多个订户可能会收到数据差异很大的广播。

您可以通过在流的名称中插入`params`(从前端发送，我们稍后会讲到)来个性化流。这允许您为每个频道实例创建个性化的流。例如，在聊天应用程序中，一个用户可以与多个用户进行多次对话。所有这些对话都具有相同的基本结构(用户可以发送和接收消息)，因此它们都订阅了相同通道的实例，`ConversationChannel`。然而，对话的实际内容因用户和对话而异。如果用户 A 和用户 B 聊天，用户 C 和用户 D 聊天，他们都会订阅`ConversationChannel`，但是每个用户的流必须是不同的。(如果每个人都能收到其他人的消息，那么祝你好运，让任何人都能使用你的应用！).假设您有一种方法来识别特定的对话(比如有一个`Conversation`模型来跟踪特定对话的实例并将其保存到数据库中)，您可以将其插入到流的名称中:

```
stream_from "conversation_#{params[:conversation_id}"
```

并且对于单个频道的每个实例，以唯一的流结束。这样，每个会话都有自己的流，正确的数据可以广播到正确的会话，从而进入下一步，

## 广播

广播实际上是向用户发送数据的过程。实现起来极其简单。基本代码如下所示:

```
ActionCable.server.broadcast("<name_of_stream>", data)
```

`:broadcast`方法的第一个参数是您要广播到的流的名称。第二个是正在广播的实际数据。在应用程序中的任何地方都可以调用这个函数，只要你能够访问你需要发送的信息，并且能够访问插入到流名称中的任何一个`params`。所以，回到聊天应用的例子。让我们假设您在您的`Message`模型和`Conversation`模型之间建立了一个关系(正如您应该做的那样)。创建了新消息，现在需要将其广播给正确的订户。假设新的消息实例以`message`的形式保存到一个变量中，那么您应该这样传播它:

```
 ActionCable.server.broadcast("conversation_#{message.conversation.id}", message)
```

请注意我是如何将对话的 id(使用活动记录关联)插入到流名称中的，以确保消息被广播到与正确的对话相关联的流中。

关于序列化程序的注意事项:广播数据库模型的实例将不会使用与该模型关联的序列化程序。如果您想要序列化您正在广播的数据，我建议为您的模型定义一个实例方法，该方法将手动序列化您将要广播的任何内容。根据消息示例，将以下代码添加到`/app/models/message.rb`:

```
def serialize
  serialized_message = ActiveModelSerializers::Adapter::Json.new(
  MessageSerializer.new(self)
  ).serializable_hash
  serialized_message[:message]
end
```

现在，在`Message`的任何实例上调用`Message#serialize`将返回一个带有序列化消息的散列。在上面的示例中，要发送序列化的消息，只需添加以下内容:

```
message = message.serialize
ActionCable.server.broadcast(
  "conversation_#{message.conversation.id}", message
)
```

好了，让我们用一个聊天应用程序的例子从头到尾快速演示一下这个过程。我们的模型和关联:

*   `User`:有很多消息，通过消息有很多对话
*   `Conversation`:有很多信息
*   `Message`:属于用户，属于对话。

用户通过在前端创建订阅来加入(预先存在的，让它变得简单)对话(这个过程我们还没有介绍)。这调用了`ConversationChannel#subscribed`，正如我们已经说过的，看起来像这样:

```
def subscribed
    stream_from "conversation_#{params[:conversation_id]}"
end
```

请记住，正确对话的`id`是作为`params`从消费者处发出的。让我们假设这个特定对话的`id`是 3。这意味着这个消费者订阅的流的名称实际上是`"conversation_3"`。现在，任何广播给`"conversation_3"`的东西都会被这个用户接收到。用户现在决定向该对话发送消息。我们将放弃之前向`ConversationChannel#received`发送消息的例子，转而使用更传统的 POST 请求。处理这个 POST 请求的控制器动作必须保存消息，并将其广播给`"conversation_3"`的所有其他订户。它看起来会像这样:

```
def create
  # We are assuming that the conversation_id foreign key is being sent in
  # the params of the request and the user's id is saved to the session hash.
  # There are other ways this can be done
  user = User.find(session[:user_id])
  message = user.messages.create(params)
  # Using the Message#serialize instance method we defined before
  serialized_message = message.serialize
  ActionCable.server.broadcast("conversation_#{message.conversation.id}", serialized_message)
end
```

在这里，我们保存消息并将其广播给`"conversation_3"`的所有订阅者，这将由前端在您认为合适的时候处理(大概是作为对话的一部分呈现在浏览器中)。

这几乎涵盖了 Action Cable 的基本后端设置！还有更多的探索，但这应该足以让它工作。让我们把注意力转向前端，以及如何让我们的 React 应用程序连接到我们的 WebSocket，以便接收和发送数据。

# 实施行动电缆:反应前端

学习使用带有独立 React 前端的 Action Cable(相对于全栈 Rails 应用程序)是一个令人望而生畏的前景。由于没有可用的官方文档，我不得不求助于其他开发人员的博客帖子。没有他们，我永远也不会走到今天，为此我心存感激。然而，在 Action Cable 教程中似乎是一个常见的主题，相对简单的概念经常以一种使它们看起来(至少对我来说)比实际更复杂的方式呈现。为了保持我的目标，使行动电缆容易，我会尽量简单地提出这一点。

以下内容将在假设您的消费者已经按照[第一部分](https://medium.com/@nkulik/using-action-cable-in-a-rails-react-app-part-i-configuration-c87b14f765a9)中的说明使用上下文设置好的情况下呈现。

## 订阅频道

您可以在应用程序中随时订阅频道。一些典型的放置通道订阅的地方是在一个`useEffect`钩子中，当一个组件被挂载时自动订阅，或者在一个由用户事件触发的回调函数中(比如提交一个表单，点击一个按钮，等等)。

订阅频道是通过在您的消费者上调用`.subscriptions.create()`来完成的(不要担心，我一会儿会清楚地演示这一点)。`create()`方法通常有两个参数。第一个是包含相关通道信息的`object`。第一个键`channel`，以字符串形式指向实际的通道名称。第二个可选键将包含需要作为`params`发送到后端的任何内容。比如，通过这个`object`:

```
{
  channel: "ConversationChannel",
  conversation_id: 5
}
```

to `create()`将在后端实例化一个对`ConversationChannel`的订阅，它将能够通过 params 访问对话 id“5”。很有可能`ConversationChannel#subscribed`会是这样的:

```
def subscribed
  # Remember, params[:conversation_id] returns the value of the
  # conversation_id key sent from the frontend, in this case 5
  stream_from "conversation_#{params[:conversation_id}"
end
```

`create()`的第二个参数也需要一个`object`。它有一个键`received`，指向一个回调函数，当通过通道接收到数据时调用这个函数。这个回调可以是你需要的任何东西。这一点很重要，因为这是处理从通道接收的数据的逻辑。此回调的典型用途是以某种方式更新状态，以便在浏览器中呈现实时信息。

订阅频道的完整代码通常如下所示(编写导入时假设组件位于`/src/components`中，CableContext 位于`/src/context/cable.js`):

```
import React, { useContext } from 'react';
import { CableContext } from '../context/cable';

const cableContext = useContext(CableContext)
// If you're unfamiliar with using context, the above code
// has nothing to do with Action Cable specifically, it's how we
// grant access to our CableContext in the component that we're
// working with

const newChannel = cableContext.cable.subscribers.create({
  channel: "ConversationChannel",
  conversation_id: 5
},
{
  received: (data) => console.log(data)
})
```

在这种情况下，我接收到的回调所做的就是将接收到的数据传递给一个`console.log`，这样我就可以在控制台中查看它，并庆祝我已经成功创建了一个频道订阅。

您可能已经注意到，我已经将我的订阅保存到了一个变量中(`newChannel`)。这将允许我们更容易地调用一些`newChannel`自带的内置方法，比如`send()`(我们将会谈到)。

让我们用一个简单但完整的组件来演示订阅过程。假设在后端的某个地方，我们有以下代码:

```
ActionCable.server.broadcast(
  "greeting_#{user.id}", { message: "Greetings, #{user.name}!" }
)
```

据推测，相关通道的`subscribed`实例方法有这样的代码来确保我们的用户订阅了正确的流:

```
stream_from "greeting_#{params[:user_id]}"
```

我们前端的 React 组件负责订阅这个通道，我们称之为我们的`GreetingChannel`，并将广播中接收到的任何消息呈现给 DOM。该组件将类似于以下内容:

```
import React, { useContext, useState, useEffect } from 'react';
import { CableContext } from '../context/cable';

function Greeting({ user }){
  const [greeting, setGreeting] = useState('Hello world!')
  const cableContext = useContext(CableContext)

  useEffect(() => {
    const newChannel = cableContext.cable.subscriptions.create(
    {
      channel: "GreetingChannel",
      user_id: user.id
    },
    {
      // remember, the data being received and passed to the received
      // callback is an object structured like this:
      // { message: "some message" }
      received: (data) => setGreeting(data.message)
    })
  }, [])

  return <h1>{greeting}</h1>
}

export default Greetingt6
```

任何时候从`GreetingChannel`广播一个新消息，`received`回调将被触发，状态将被更新，自动重新呈现组件，从而在浏览器中显示新的`greeting`。

这应该包括订阅频道和处理接收到的数据的基础知识，最终将我们带到最后的演示，将数据从前端发送回服务器。

## 从前端向频道服务器发送数据

正如我前面提到的，创建订阅提供了对几个内置方法的访问。你最常用的两个是`send()`和`unsubscribe()`。我得说这两者都是不言自明的。当您希望您的消费者不再订阅该频道时，会调用`unsubscribe()`。假设您的订阅保存到一个变量中作为`newChannel`，取消订阅就像调用`newChannel.unsubscribe()`一样简单。`send()`接受一个参数，数据被发送到通道(通常以`object`的形式，我认为是惯例)，并且，你猜对了，将数据发送到通道。这将在后端触发`Channel#received`，数据将作为参数传递给它。

所以`newChannel.send({message: "hello world"})`将调用`Channel#received`，传递`{message: "hello world"}`作为参数。做什么取决于你，因为你(开发者)将在`Channel#received`方法中编写代码。

关于`objects`和`hashes`的一个简单说明:JavaScript `object`的键的默认数据类型是`string`，Ruby `hash`的键的默认数据类型是`symbol`。因此，在 JavaScript 中，用键访问一个值通常看起来像是`object['key']`，而在 Ruby 中是`hash[:key]`。我现在提出这个是因为当你从前端发送数据作为一个`object`时，密钥被保存为一个`string`。当编写通道的`received`方法的逻辑时，您可能会本能地尝试通过将键作为符号传递来访问数据的键。这样不行。当处理消费者发送的对象时，您需要将键作为字符串传递，就像在 JavaScript 中一样。

我想就这样吧！我并没有涵盖关于 Action Cable 的所有内容，但是我相信我已经涵盖了您需要的所有内容。谢谢你坚持到最后！

# 资源

[](https://guides.rubyonrails.org/action_cable_overview.html) [## Action Cable 概述- Ruby on Rails 导轨

### Action Cable 概述在本指南中，您将了解 Action Cable 的工作原理以及如何使用 WebSockets 来整合…

guides.rubyonrails.org](https://guides.rubyonrails.org/action_cable_overview.html) [](https://medium.com/nerd-for-tech/using-action-cable-in-your-rails-react-app-showing-online-status-7204c6553d02) [## 在你的 Rails/React 应用中使用 Action Cable:显示“在线”状态

### 我目前正在使用 Action Cable 来实现我的幻想相扑应用程序的现场草稿。有几个…

medium.com](https://medium.com/nerd-for-tech/using-action-cable-in-your-rails-react-app-showing-online-status-7204c6553d02) [](/integrating-actioncable-with-react-9f946b61556e) [## 将 ActionCable 与 React 集成

### Action Cable 是 Ruby on Rails 提供的一个框架，它允许开发人员在他们的…

javascript.plainenglish.io](/integrating-actioncable-with-react-9f946b61556e) [](https://medium.com/@dakota.lillie/using-action-cable-with-react-c37df065f296) [## 使用带 React 的动作电缆

### 在最近的一个项目中，我用 React 前端和 Rails API 后端制作了一个聊天应用程序，目标是熟悉…

medium.com](https://medium.com/@dakota.lillie/using-action-cable-with-react-c37df065f296)  [## action cable-stream _ for vs stream _ from

### ActionCable 是 Ruby on Rails 5+中新的 WebSockets 集成特性。它有几个很棒的特性，其中之一是…

laithazer.com](http://laithazer.com/blog/2017/03/25/rails-actioncable-stream-for-vs-stream-from/) [](https://medium.com/swlh/action-cable-react-hooks-redux-toolkit-yet-another-chat-app-with-unread-messages-feature-93f5f36d4489) [## Action Cable，React Hooks，Redux Toolkit:又一款聊天应用——带有未读消息功能

### Action Cable 是集成 WebSockets 的 Rails 方式，允许以最小的开销进行双向通信…

medium.com](https://medium.com/swlh/action-cable-react-hooks-redux-toolkit-yet-another-chat-app-with-unread-messages-feature-93f5f36d4489) [](https://blog.devgenius.io/integrate-action-cable-with-react-and-ruby-on-rails-to-build-a-one-to-one-chatting-app-4f0feb5479e6) [## 将 Action Cable 与 React 和 Ruby on Rails 集成起来，构建一个一对一的聊天应用程序

### 最近，我正在开发一款带有一对一聊天功能的约会应用。一切都按计划进行，直到…

blog.devgenius.io](https://blog.devgenius.io/integrate-action-cable-with-react-and-ruby-on-rails-to-build-a-one-to-one-chatting-app-4f0feb5479e6) 

*更多内容看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**