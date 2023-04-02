# Redis 如何让用户的身份验证变得简单 10 倍

> 原文：<https://javascript.plainenglish.io/how-redis-can-make-authentication-10x-easoer-for-your-users-cd8c0601d38?source=collection_archive---------1----------------------->

![](img/7f64c1651cf0fad0be1c6f3b684e6f3d.png)

您是一名开发人员，可能已经为一些用户构建了一些应用程序。您的用户需要注册才能访问您的应用程序上的一些资源。要完成注册，他们还必须验证他们的电子邮件。虽然有些用户完全可以接受这一额外的步骤，但大多数人并不觉得愉快，即使他们知道他们不得不这样做。为什么？太手动了。

如果有一种更好的方法来验证用户的电子邮件，而不使其过于露骨，会怎么样？那么，让我向您介绍一下 Magic Link 认证模型。你可能已经听说过它，甚至以前在什么地方用过它。注册时，从用户的角度来看是这样的:

*   他们输入自己的电子邮件地址
*   一个链接被发送到该电子邮件地址
*   他们进入收件箱并打开链接(这是验证被巧妙应用的地方)
*   他们将被重定向到一个注册页面，在这里他们将输入自己的其他详细信息，如姓名、密码、电话等。
*   他们注册并立即被登录

很简单！没有人需要知道他们必须验证他们的电子邮件——他们只是在没有注意到的情况下这么做了。这就是为什么魔链模型在现代认证系统中被直观地接受的原因。但是在这个过程中，幕后发生了很多事情。这就是本教程的重点。

有一些方法可以在后端实现这个概念，选择权在你。但是不一定要选择效率较低的。想想吧。如果你想用 Express 实现这个，你会怎么做？也许您会创建一个端点(端点 1 ),实现以下算法:

1.  从请求主体收集电子邮件
2.  使用 Node.js 内置加密包生成令牌
3.  将电子邮件和令牌以及过期时间存储在数据库中的一个单独的(来自您的用户)表中
4.  将令牌注入一个 URL(匹配前端的一个页面),并将其发送到给定的电子邮件地址

然后，另一个端点(端点 2，通常是注册路由)执行以下操作:

1.  检查请求对象中是否提供了令牌
2.  收集用户的详细信息，尤其是电子邮件地址
3.  尝试从数据库的“特殊”表中提取带有给定标记的记录
4.  如果记录不存在，返回一个禁止的错误
5.  如果记录存在，但过期时间已到，则返回一个错误请求错误
6.  如果记录存在并且到期时间仍然有效，则使用给定的详细信息创建一个新用户

让我们考虑一下这种方法。你觉得有效吗？嗯，除了端点 1 的第 3 步，一切看起来都很理想。我这么想的原因如下:

*   将令牌存储在数据库中是没有意义的，因为它只是初步数据，以后将变得无用。
*   你的数据库会被瘾君子的数据塞满。您可能会争辩说，您可以应用 endpoint 2 中的第 7 步来删除记录，但在我看来，使用数据库来删除记录效率较低，而且对生产来说也不理想。我相信你能想到这种方法的其他缺点。

更好的方法是使用 JWT。使用 JWT 将处理端点 1 的步骤 2 和 3。然后，端点 2 的步骤 3 将适合于用 JWT 而不是数据库来验证令牌。尽管如此，这并不是最好的解决方案。原因是，对于这个简单的问题，使用 JWT 是多余的。

更好的解决方案是使用 RedisJSON。

RedisJSON 是一个高性能的 NoSQL 文档存储库，它提供本机 API 来接收、索引、查询和运行 JSON 文档的全文搜索，既可以在本地进行，也可以作为云中的托管服务。这意味着您可以使用 RedisJSON 内存[键-值]数据结构存储作为数据库和缓存。你可以在这里了解更多信息。让我向您展示 [Redis](https://www.linkedin.com/company/redisinc/) 如何根除端点 1 的步骤 3 的低效。

# 该项目

对于本教程，我创建了一个项目，我们将使用整个。这是一个非常简单的 Express 应用程序，它公开了三个 RESTful API 端点— /users、/users/magic_link 和/users/signup。你可以在这里克隆或下载源代码。这是一个文档化的应用程序。

# 先决条件

*   我假设您已经了解了容器的基本知识，并且在您的机器上安装了 docker。如果您没有安装它，请遵循本指南并从支持的平台中选择一个。你根本不知道容器的概念？没问题。只要按照教程一步一步来，并确保安装所有必要的依赖关系。
*   在这里安装 docker-compose。使用这两个命令在 Linux 上安装要容易得多:

1.

```
sudo curl -L “https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)” -o /usr/local/bin/docker-compose
```

2.

```
sudo chmod +x /usr/local/bin/docker-compose
```

*   当然，还要确保安装了 Node.js 和 NPM。

# 项目之旅

让我给你介绍一下这个项目。在您喜欢的代码编辑器中打开项目文件夹。请注意，项目文件夹包含两个文件夹— starter 和 final。starter 文件夹包含我们需要开始的不完整的代码和文件。最后一个文件夹包含完整的源代码。

![](img/975aaacc47c79fe90b9ae53127aec58f.png)

如果您希望快速浏览一下我们将要构建的内容，首先确保 docker 已经启动并正在运行，然后打开您的终端并运行以下命令:

```
❯ cd finalfinal ❯ docker-compose up -d --build
```

Docker-compose 将执行 docker-compose.yml 文件中的所有指令。如果你对 docker-compose 一无所知，也不用担心。毕竟这不是 docker 教程😊。

之后，你应该访问[http://localhost:4000/users](http://localhost:4000/users)。如果一切正常运行，您应该会看到如下成功响应:

![](img/edaeea31efae9357be507baa174516fe.png)

要停止所有正在运行的容器，请执行:

```
final ❯ docker-compose down
```

# 现在，让我们开始吧！

将目录改回起始文件夹。在这个文件夹中，您应该看到包含两个 env 文件的 env 文件夹—一个用于 MongoDB，另一个用于 app。starter 文件夹中的另一个文件夹是 utils 文件夹，目前只包含邮件程序模块。我们将使用这个模块发送电子邮件。

![](img/89002fdcbd1544569862af89e46c422f.png)

其余的是:

*   。dockerignore 文件
*   包含一组可执行指令的 docker-compose.yml 文件，使用它们各自的容器名来启动 mongodb、redis 和我们的 magiclinkredis 应用程序映像
*   一个 docker 文件，具有 docker 识别的语法，用于创建我们的应用程序映像
*   一个空的 index.mjs 文件，它将很快包含我们的应用程序逻辑
*   以及描述我们的应用程序依赖关系的 package.json 文件

所以，让我们启动所有的容器。运行:

```
starter ❯ docker-compose up -d --build
```

这将查看 docker-compose 文件，并按照文件中的描述逐行执行指令。它将尝试提取为每个服务规定的图像，并旋转它们各自的容器。下面我们来分析一下 Redis 服务:

![](img/623292650e9f31cbd9f54574bf4ef000.png)

我们将从 docker hub 中调出标签为 7.0.2-alpine 的官方 Redis docker 图片。然后，我们为用这个映像创建的容器提供名称“redis”。或者，我们可以在发生意外时“重启”容器。最后，我们执行命令来启动 Redis 服务器。你可以在[官方 Redis docker hub 页面](https://hub.docker.com/_/redis)上找到这个配置和更多信息。

因为我们应用了一个[绑定挂载](https://docs.docker.com/storage/bind-mounts/)，每当我们在 index.mjs 文件中做了更改，服务器就会重新加载，这些更改会立即反映出来，这在开发中非常有用。

我们可以通过运行以下命令来跟踪应用程序的日志:

```
starter ❯ docker logs magic-link-redis -f
```

在 index.mjs 文件中，让我们导入 express、mongoose、morgan 和 dotenv 模块。然后初始化我们的 express 服务器，并将其连接到 MongoDB 数据库:

```
 import express from "express" import mongoose from "mongoose"; import morgan from "morgan"; import { config } from "dotenv"; config({ path: "./env/.env" }); const app = express(); app.use(morgan("combined")); app.use(express.json()); app.use((req, res, next) => { res.setHeader("Access-Control-Allow-Origin", "*"); res.setHeader("Access-Control-Allow-Methods", "GET, POST, DELETE,  OPTIONS"); res.setHeader("Access-Control-Allow-Headers", "Content-Type"); next(); }); mongoose.connect( `mongodb://${process.env.MONGODB_USERNAME}:${process.env.MONGODB_PASSWORD}@mongodb:27017/migic-link-redis?authSource=admin`, { useNewUrlParser: true, useUnifiedTopology: true, }, (err) => { if (err) { console.error("FAILED TO CONNECT TO MONGODB"); console.error(err); } else { console.log("CONNECTED TO MONGODB!!"); app.listen(4000, () => console.log( `App listening on port 4000 in ${process.env.NODE_ENV} mode.` ) ); } });
;
```

您应该会在日志中看到这样的消息:

![](img/b144aae2094c225bad455ac022ce2b2e.png)

这是一个好迹象😉。深呼吸…你做得很好。

让我们创建用户模式。从相对于“starter”文件夹的根文件夹中，创建一个新文件夹，并将其命名为“models”。在这个新文件夹中，创建一个“user.mjs”文件。

![](img/447ea55e01a655c052bb40ecddc253eb.png)

将以下代码放入 user.mjs 文件中:

```
import mongoose from "mongoose"; import bcrypt from "bcryptjs"; import validator from "validator"; const Schema = mongoose.Schema;
  const userSchema = new Schema( { name: { type: String, trim: true, }, email: { type: String, required: true, unique: true, lowercase: true, validate: [validator.isEmail, "Email is invalid."], }, password: { type: String, required: true, select: false, }, }, {
    timestamps: true,
  } );

 userSchema.pre("save", async function (next) { if (!this.isModified("password")) return next(); // Hash password with a cost of 12 this.password = await bcrypt.hash(this.password, 12); next(); }); const UserModel = mongoose.model("User", userSchema); export default UserModel;
```

将用户模式模块导入 index.mjs 文件:

```
import User from "./models/user.mjs";
```

现在让我们创建一个 GET /users 端点来获取所有用户文档。

```
app.get("/users", async (req, res) => { try { const users = await User.find(); res.status(200).json({ status: "SUCCESS", users, }); } catch (err) { console.error(err.message); res.status(500).json({ status: "FAIL", message: "Failed to fetch  users." }); } });
```

打开您的 Postman(可能)并尝试在 GET[http://localhost:4000/users](http://localhost:4000/users)处调用端点。您应该得到以下响应(否则，请跟我唱二重唱😜):

![](img/edaeea31efae9357be507baa174516fe.png)

# 开始有趣的部分

这是更有趣的地方。我们将创建另一个端点来处理神奇链接逻辑。这个端点将执行开头提到的“端点 1”的逻辑。这一次，我们将利用 RedisJSON 的特性。

在创建此端点之前，我们需要首先创建两个模块:tokenGenerator.mjs 和 cacheHandler.mjs。因此，在 utils 文件夹中，创建上述文件并将以下代码放入 tokenGenerator.mjs 文件中:

```
import crypto from "crypto";export default () => crypto.randomBytes(32).toString("hex");
```

这个模块将用于生成一个随机哈希值，该值被转换成一个字符串并用于注册令牌。

现在，更重要的是，缓存处理程序。这个文件是我们实现和连接 Redis 到我们的应用程序的地方。它处理三个函数:getCache 用于查询 RedisJSON API 以通过给定的键获取数据，setCache 用于存储具有给定的键、数据和过期时间(以秒为单位)的新缓存，deleteCache 用于从内存中删除缓存。如果你想了解更多关于这个概念的内容，请看我之前关于如何使用 Redis [创建活跃用户指标的文章。](/how-to-implement-daily-active-users-metric-using-redis-4a7d7c4aca8f)

该模块的代码如下:

```
import { createClient } from "redis"; let client; if (process.env.NODE_ENV === "production") { client = createClient({ url: `redis://${process.env.REDIS_USER}:${process.env.REDIS_PASSWORD}@${process.env.REDIS_HOSTNAME}:${process.env.REDIS_PORT}`, }); } else { client = createClient({ url: "redis://redis:6379", }); } client.on("error", (err) => console.log("Redis Client Error", err)); async function connectRedis() { await client.connect(); } connectRedis(); const defaultExpirationTime = 60 * 10; // 60 seconds times 10 -> 10 minutes const handleCache = (cb) => cb(); export const getCache = (key) => new Promise((resolve, reject) => { try { handleCache(async () => { const data = await client.get(key); if (data) { console.log("DATA FOUND! 🥳"); } resolve(JSON.parse(data)); }); } catch (error) { reject(error); } }); export const setCache = (key, data, expTime) => { if (typeof expTime === "undefined") { expTime = defaultExpirationTime; } return new Promise((resolve, reject) => { try { handleCache(async () => { const isOk = await client.set(key, JSON.stringify(data), { EX: expTime, }); if (isOk) {
          console.log("CACHED! ✅");
        } resolve(); }); } catch (error) { reject(error); } }); }; export const deleteCache = (key) => new Promise((resolve, reject) => { try { handleCache(async () => { const response = await client.del(key); if (response === 1) { console.log("CACHE DELETED!"); } resolve(JSON.parse(response)); }); } catch (error) { reject(error); } });
```

注意，初始化 Redis 客户机的实现受到两个条件的限制:如果应用程序运行在开发环境上，则连接到本地 Redis 服务(运行在 docker 容器的 6379 端口上)。否则，使用“您的”凭证连接到 redis 云服务。这一点至关重要，因为您应该在生产中使用云服务。如果你想了解更多关于 Redis Cloud 的信息，请访问[官方页面](https://redis.com/try-free/?utm_campaign=write_for_redis)。最棒的是你可以从免费计划开始。

好吧！现在，让我们将模块导入 index.mjs 文件:

```
import tokenGenerator from "./utils/tokenGenerator.mjs"; import { setCache, getCache, deleteCache } from  "./utils/cacheHandler.mjs"; import { sendMagicLink } from "./utils/mailer.mjs";
```

注意，我们还导入了邮件模块。

因此，让我们创建神奇链接端点(端点 1):

```
app.post("/users/magic_link", async (req, res) => { const { email } = req.body; if (!email) return res.status(400).json({ status: "FAIL", message: "Email required." }); try { // 1) check if user exists already const userExists = await User.findOne({ email }); if (userExists) return res .status(400) .json({ status: "FAIL", message: "Email already in use." }); // 2) generate token const token = tokenGenerator(); // 3) store email and token in redisJSON for 24 hours const hours24 = 60 * 60 * 24; await setCache(token, { email, token }, hours24); // 4) send token to user's email address sendMagicLink(email, token); res.status(200).json({ status: "SUCCESS", message: "Link sent to your email!", }); } catch (err) { console.error(err.message); res .status(500) .json({ status: "FAIL", message: "Something went terribly wrong."       }); } });
```

这里，我们在端点 1 中实现了开始时提到的逻辑，但是增加了一个额外的验证步骤，检查给定电子邮件地址的帐户是否已经存在。然后，我们用 RedisJSON 缓存时态文档，并将到期时间设置为 24 小时，而不是将它存储在数据库中。简单的👌🏾。

我能感觉到你想测试这个终点的冲动，但是不要这么快😜。注意，邮件模块实现了 nodemailer transporter，它需要一些 Zoho 邮件凭证。这意味着你应该在这里创建一个 Zoho 账户[。然后，替换。env 文件分别与您的 Zoho 电子邮件和密码。现在我们可以走了。](https://www.zoho.com/signup.html)

使用以下有效负载向[http://localhost:4000/users/magic _ link](http://localhost:4000/users/magic_link)发出 POST 请求:

![](img/4032030a71900242ed1c8cd8b786844f.png)

上面的邮件应该是你的邮件，否则我会吃掉你的邮件😁。

如果一切正常，您应该会在您的应用程序日志中看到如下消息:

![](img/4ae0fe88be804623fedfca5acffb2b08.png)

这意味着电子邮件已经发送到您的电子邮件地址。

最后，让我们创建注册端点(端点 2):

```
app.post("/users/signup", async (req, res) => { const { email, name, password } = req.body; const { token } = req.query; // 1) check if user exists already const userExists = await User.findOne({ email }); if (userExists) return res .status(400) .json({ status: "FAIL", message: "Email already in use." }); // 2) require token if (!token) return res.status(400).json({ status: "FAIL", message: "Token required." }); // 3) validate body if (!email || !name || !password) return res .status(400) .json({ status: "FAIL", message: "Invalid request." }); // 4) check if data exists on redisJSON and client email matches data email. if  NOT, return "Access denied" const data = await getCache(token); if (!data || data.email !== email) return res.status(403).json({ status: "FAIL", message: "Access denied." }); // 5) if exists, create new user account let user; try { user = await User.create({ name, email, password }); await deleteCache(email); res.status(201).json({ status: "SUCCESS", message: "User saved!", user, }); } catch (err) { console.error(err.message); res.status(500).json({ status: "FAIL", message: "Failed to save user." }); }});
```

在这里，我们还要确保不要用已经存在的电子邮件地址创建帐户。我们确保将令牌和所需的主体细节传递给请求对象。然后，我们检查 Redis 上的令牌是否存在。如果令牌存在，并且提供的电子邮件与 Redis 上存储的数据电子邮件相匹配，那么我们继续创建用户文档。此后，出于安全考虑，我们会删除缓存，即使它无论如何都会过期。

多酷啊。使用 Redis 简单而有效地解决了这个问题。现在，让我们测试这个端点。转到您的收件箱，复制 URL 字符串中的令牌。将令牌附加到请求查询对象，并将请求发送到[http://localhost:4000/users/sign up？token=YOUR_TOKEN](http://localhost:4000/users/signup?token=YOUR_TOKEN) 具有以下有效载荷:

![](img/f437879cc9f5724b13eebb71cee16757.png)

如果一切正常，您应该会得到一个成功的 201 响应👍🏾。

# 结论

每个用户都想要轻松的生活。如果你想让你的应用程序的认证对你的用户来说简单 10 倍，利用 RedisJSON。我希望这篇教程对你有所帮助。

这篇文章是与 Redis 合作的。

了解更多信息:

*   [免费试用 Redis Cloud】](https://redis.info/3NBGJRT)
*   [观看此视频，了解 Redis 云相对于其他 Redis 提供商的优势](https://redis.info/3Ga9YII)
*   [Redis 开发者中心——关于 Redis 的工具、指南和教程](https://redis.info/3LC4GqB)
*   [RedisInsight 桌面图形用户界面](https://redis.info/3wMR7PR)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)**和* [***不和***](https://discord.gg/GtDtUAvyhW) ***。****