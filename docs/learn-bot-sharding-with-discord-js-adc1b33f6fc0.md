# 用 Discord.js 学习 Bot Sharding

> 原文：<https://javascript.plainenglish.io/learn-bot-sharding-with-discord-js-adc1b33f6fc0?source=collection_archive---------10----------------------->

![](img/a74a22842aff170b99334c003aa5ace4.png)

Photo of The Shard by [Jamie Street](https://unsplash.com/@jamie452?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当一个不和谐机器人发展到一定规模时，通常大约有 2000 个加入的服务器，机器人的单个实例将开始与所有这些计算斗争。这就是分片的用武之地。分片是在 [Discord 开发者文档](https://discord.com/developers/docs/topics/gateway#sharding)中定义的一种方法，它允许你运行同一个 bot 的多个实例，在所有实例之间分割服务器的份额。

假设你已经创造了下一个大的不和谐机器人。事情进展得非常顺利，您的机器人已经被添加到近 2000 台服务器上。但是你的机器人在挣扎，事实上，它已经崩溃过几次了。因此，为了处理这个带宽，您设置了 bot 的第二个实例，每个实例需要大约 1000 台服务器。这就是实际应用中的分片。现在，你不能只运行机器人的两个实例，你必须定义一个分片管理器来在两者之间分配工作。

今天，您将学习如何使用 Discord.js 和一些技巧来设置分片，以保持 bot 的所有功能正常工作，即使在通过分片管理器运行两个实例时也是如此。

# **创建一个机器人(可选)**

如果你已经有了一个用 Discord.js 编写的 Discord bot，你可以放心地跳过这一步。对于那些还没有，让我们创建一个简单的 NPM 项目，并添加一个简单的机器人。

```
mkdir pingbot
cd pingbot
npm init -y
npm i discord.js
```

在创建了 NPM 项目并安装了 Discord.js 之后，在该目录下创建一个`index.js`文件并添加以下 bot 代码。然后添加您的 bot 令牌，并使用`node .`运行项目，以测试它是否正常工作。

```
const { Client, Intents } = require('discord.js')const BOT_TOKEN = 'BOT_TOKEN_HERE'let client = new Client({
  intents: [Intents.FLAGS.GUILDS, Intents.FLAGS.GUILD_MESSAGES]
})client.on('messageCreate', message => {
  if (message.content === 'ping') message.reply('Pong!')
})client.login(BOT_TOKEN)
```

# 实现分片

那么我们如何分割我们的机器人呢？嗯，Discord.js 有一个内置的分片管理器来管理同一台机器上的多个 bot 实例。创建一个名为`shard.js`的新文件并导入`ShardingManager`。然后创建一个`manager`，给它一个 bot 条目文件(`index.js`)和 bot 令牌。注意，您需要在碎片管理器和 bot 本身中传递令牌。对于经理来说，还有更多选项，你可以在 [Discord.js 文档](https://discord.js.org/#/docs/main/stable/class/ShardingManager)中找到。

```
const { ShardingManager } = require('discord.js')const BOT_TOKEN = 'BOT_TOKEN_HERE'const manager = new ShardingManager(`${__dirname}/index.js`, { token: BOT_TOKEN })
```

然后我们可以监听`shardCreate`事件，并在启动时记录碎片的 id。然后，我们准备用`.spawn()`产生我们的碎片。

```
manager.on('shardCreate', shard => console.log(`Launched shard ${shard.id}`))
manager.spawn()
```

# **清点服务器**

你在分片时可能会遇到的一个问题是试图显示你的机器人已经加入的服务器数量。这是机器人状态或`/status`命令的一个常见特征。如果您尝试用`client.guilds.cache.size`获取您的 bot 所在的服务器数量，您可能会惊讶地看到它返回一个远低于实际数量的数字。这只是为这个单独的碎片提供服务的服务器数量。为了获得总数，我们可以使用下面的代码片段来获得每个分片中的服务器数量，然后将它们相加，然后在 promise 中返回该值。

```
function totalGuilds() {
  return client.shard.fetchClientValues('guilds.cache.size')
    .then(shards => {
      return shards.reduce((acc, guilds) => acc + guilds, 0)
    })
}
```

您可以使用类似的技巧来获取总成员数。这一次使用了`broadcastEval`方法，该方法将代码发送给所有碎片进行评估，并返回包含响应数组的 promise。

```
function totalMembers() {
  return client.shard
   .broadcastEval(c => c.guilds.cache.reduce((acc, guild) => acc + guild.memberCount, 0))
   .then(shards => shards.reduce((acc, memberCount) => acc + memberCount, 0))
}
```

# **结论**

超过一定规模的机器人需要分片，一旦达到该规模，将机器人分成多个实例将有助于提高性能。Discord.js 使设置分片变得很容易，所以如果你有一个增长很快的机器人，记住这一点，也许现在就开始实现它。如果您想提前计划好事情，也可以运行单个 shard 实例。

您只能纵向扩展这么多，所以很快我将在本文的第二部分解释如何在多个物理机器上共享您的 discord bot。

[](/technologies-i-plan-to-learn-in-2022-a9f44e9c3162) [## 我计划在 2022 年学习的技术

### 我 2022 年的学习目标。

javascript.plainenglish.io](/technologies-i-plan-to-learn-in-2022-a9f44e9c3162) [](https://medium.com/@otterlord/5-awesome-discord-bot-ideas-c5c6f550e307) [## 5 个绝妙的不和谐机器人创意

### 不和谐机器人非常受欢迎，而且比以往任何时候都更容易上手。每个专业都有图书馆…

medium.com](https://medium.com/@otterlord/5-awesome-discord-bot-ideas-c5c6f550e307) [](/learn-jest-javascript-unit-testing-5ca104b564ce) [## 学习 Jest——JavaScript 单元测试

### 单元测试是指测试单个的代码单元，甚至是多个代码单元，以确保它们能正常工作…

javascript.plainenglish.io](/learn-jest-javascript-unit-testing-5ca104b564ce) 

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*