# 如何使用 Node.js 和 TypeScript 与 RabbitMQ 实例对话

> 原文：<https://javascript.plainenglish.io/how-to-talk-to-a-rabbitmq-instance-with-node-js-and-typescript-92dbc514eaf8?source=collection_archive---------0----------------------->

## RabbitMQ、Node.js 和 TypeScript 一起使用

![](img/22168a1e3fd26c4542c699d91fb5ce21.png)

RabbitMQ 是一个**消息队列系统**，它允许您对消息(对您的应用程序有意义的字符串值)进行排队，以供消费者(处理 RabbitMQ 消息的程序片段)使用。

当有大量数据需要处理，但处理不一定是即时的时，可以使用它。

在本文中，我们将建立一个 Node.js 应用程序，它可以使用 RabbitMQ 实例发送和使用消息。

## 先决条件

我们不会花太多时间来设置 RabbitMQ。相反，我们将使用 RabbitMQ 的 **docker 图像。**

为此，您需要在您的机器上安装并运行 Docker。

我们还将使用 Node.js，无论有无 NVM，您都必须安装 npm。14 版或更新版本就够了！

## 使用 docker-compose 的 RabbitMQ

我们不想浪费时间配置 RabbitMQ。相反，我们将使用 Docker 快速部署 RabbitMQ。

在您的项目中，创建一个`docker-compose.yml`文件，并将以下内容粘贴到其中:

```
version: "3.7"
services:
  rabbitmq:
    image: rabbitmq:3.9.13-management-alpine
    container_name: 'rabbitmq'
    restart: always
    environment:
      - "RABBITMQ_DEFAULT_PASS=password"
      - "RABBITMQ_DEFAULT_USER=username"
    ports:
      - 15672:15672
      - 5672:5672
    networks:
      - rabbitmq_go_net

networks:
  rabbitmq_go_net:
    driver: bridge
```

然后在终端中，只需运行命令`docker-compose up -d`
它就会部署一个新的 RabbitMQ 运行实例！

完成后，在浏览器中打开 http://localhost:15672 ，使用 docker-compose 文件中提供的用户名和密码。

你应该看到 RabbitMQ 的管理页面！如果你不熟悉的话，不要犹豫，赶快四处看看。

## 与 RabbitMQ 建立联系

为此，我们将使用一个名为 amqplib 的库，它是 Node.js 的 **RabbitMQ 客户端。**

[](https://www.npmjs.com/package/amqplib) [## amqplib

### npm 安装 amqplib 库，用于为节点制作 AMQP 0-9-1 客户端。JS 和一个 AMQP 0-9-1 节点客户端。JS v10+…

www.npmjs.com](https://www.npmjs.com/package/amqplib) 

安装它并安装它的类型定义(如果您没有使用 TypeScript，您不需要这样做)。

```
npm install amqplib -S
npm install @types/amqplib -D
```

安装完成后，我们将连接到 RabbitMQ 实例。

> 该库支持 2 种方法(异步或回调),我们将在这里使用异步。如果你想启用回调函数，只需在每次导入后添加`/callback_api`即可。

```
import client, {Connection} from 'amqplib'...const connection: Connection = await client.connect(
  'amqp://username:password@localhost:5672'
)
```

这是使用 RabbitMQ 的第一步，即连接到服务。该 URL 使用 docker-compose 文件中定义的相同用户/密码。端口是配置文件中的第二个端口:5672

异步函数`connect`返回连接对象。

## 向 RabbitMQ 发送消息

第二步是向我们的 RabbitMQ 服务发送消息。

我们将不得不访问我们的队列。队列是在第一次访问时自动创建的，不需要担心它们的存在。

我们首先要创建一个通道。通道是一个轻量级 TCP 连接，用于向 RabbitMQ 发送数据或从 rabbit MQ 接收数据。它们与连接共存，如果连接关闭，它们也会关闭。

```
const connection: Connection = await client.connect(
'amqp://username:password@localhost:5672'
)// Create a channel
const channel: Channel = await connection.createChannel()// Makes the queue available to the client
await channel.assertQueue('myQueue')//Send a message to the queue
channel.sendToQueue('myQueue', ***Buffer***.from('message'))
```

将这段代码添加到您的程序后，您应该会看到您的管理页面，尤其是[队列选项卡](http://localhost:15672/#/queues)。

如果一切都按预期运行，您应该会看到一个名为`myQueue`(或者无论您如何称呼它)的队列，如果您打开它，它会有一条空闲模式的消息。此消息正等待使用。这是我们文章的下一步，也是最后一步。

## 消费我们的信息

消费消息相当简单。我们所要做的就是使用通道调用`consume`方法，并给它队列来消费，以及在接收消息时要调用的回调。

> 你应该创建一些小程序来消费，而不是将消费者添加到主应用程序中。原因是 javascript 是单线程的，如果用户需要处理大量的工作，他们可能会降低主应用程序的速度。

```
import client, {Connection, Channel, ConsumeMessage} from 'amqplib'

// Function to send some messages before consuming the queue
const sendMessages = (channel: Channel) => {
  for (let i = 0; i < 10; i++) {
    channel.sendToQueue('myQueue', ***Buffer***.from(`message ${i}`))
  }
}

// consumer for the queue. 
// We use currying to give it the channel required to acknowledge the message
const consumer = (channel: Channel) => (msg: ConsumeMessage | null): void => {
  if (msg) {
    // Display the received message
    ***console***.log(msg.content.toString())
    // Acknowledge the message
    channel.ack(msg)
  }
}const connection: Connection = await client.connect(
'amqp://username:password@localhost:5672'
)
// Create a channel
const channel: Channel = await connection.createChannel()
// Makes the queue available to the client
await channel.assertQueue('myQueue')
// Send some messages to the queue
sendMessages(channel)
// Start the consumer
await channel.consume('myQueue', consumer(channel))
```

这是我们的最终代码！这段代码将创建/访问我们的队列，在上面发送一些消息并使用它。

> Y 您可能会注意到对`channel.ack`的调用，这是为了告诉 RabbitMQ 消息已经成功处理。否则，RabbitMQ 将等待它完成，并最终重新发布它(就像您这样设置它)。

## 结论

现在，Node.js 应用程序上应该有一个正常工作的 RabbitMQ 客户端了。

如果你想了解更多关于 amqplib 的 API，你应该去看看他们的文档。

你可以在[我的 GitHub](https://github.com/psyycker-medium/rabbitmq-nodejs-typescript) 上找到文章的代码。

我希望你喜欢这篇文章！保重！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***