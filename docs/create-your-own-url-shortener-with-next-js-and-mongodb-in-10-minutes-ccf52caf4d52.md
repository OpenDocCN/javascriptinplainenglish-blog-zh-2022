# 用 Next.js 和 MongoDB 在 10 分钟内创建你自己的网址缩写

> 原文：<https://javascript.plainenglish.io/create-your-own-url-shortener-with-next-js-and-mongodb-in-10-minutes-ccf52caf4d52?source=collection_archive---------11----------------------->

## 使用 Next.js 创建 URL shortener 的完整服务和使用 MongoDB 存储链接的指南。

![](img/84fddde7fb46f8457fa7fea94471ca3a.png)

# 动机

几周前，我正在开发一个 Twitter 机器人来发布我的热门文章，我意识到一些文章的链接在 Tweet 中没有被很好地解析。然而，使用[重塑](https://www.rebrandly.com/)来缩短它们效果很好。

所以，我决定为自己做一个网址缩短器。

# 故障

我们需要一个

*   服务为每个长 URL 创建一个唯一的散列
*   用于保持长短 URL 映射的数据库
*   将短链接重定向到其目的地的服务

和往常一样， **Next.js** 是我构建完整服务的首选，而 **MongoDB** 用于存储链接。

# 发展

既然我们已经想出了步骤，让我们一个接一个地做吧

## 设置项目

让我们使用`npx create-next-app url-shortener`命令为我们的应用程序生成一个样板文件。

```
./.env.local 
DB_NAME=url-shortner
ATLAS_URI_PROD=mongodb+srv://<user>:<password><cluster>.mongodb.net/url-shortner?retryWrites=true&w=majority API_KEY=<a-long-random-string> 
HOST=http://localhost:3000
```

这些环境变量也应该存储在您的 Vercel 项目中。

> *`*HOST*`*的值应该在你托管这个项目的时候设置到你的域。如果你没有公共域，就用你的* `*NEXT_PUBLIC_VERCEL_URL*` *环境变量代替* `*HOST*` *。**

## *设置 MongoDB*

1.  *跑`npm i --save mongodb`*
2.  *在 repo 的根目录下创建一个`mongodb.ts`文件。*

```
*// ./mongodb.ts

import { Db, MongoClient } from "mongodb";
import { formatLog } from "./utils";

// Create cached connection variable
let cachedDB: Db | null = null;

// A function for connecting to MongoDB,
export default async function connectToDatabase(): Promise<Db> {
  // If the database connection is cached, use it instead of creating a new connection
  if (cachedDB) {
    console.info(formatLog("Using cached client!"));
    return cachedDB;
  }
  const opts = {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  };
  console.info(formatLog("No client found! Creating a new one."));
  // If no connection is cached, create a new one
  const client = new MongoClient(process.env.ATLAS_URI_PROD as string, opts);
  await client.connect();
  const db: Db = client.db(process.env.DB_NAME);
  cachedDB = db;
  return cachedDB;
}*
```

## *添加创建短链接服务*

*继续添加一个`./api/create-link.ts`文件，为这个服务创建一个 REST 端点。*

*我们需要注意几件事*

1.  *创建短 URL 需要唯一的哈希。我使用`nanoid`为长 URL 生成一个随机的短散列。*
2.  *此端点应仅由 POST 方法访问。*
3.  *我们应该设置一个 API 密钥认证来保护端点。这可以通过生成一个长字符串并将其用作 API-KEY 头来实现。*

```
*// ./api/create-link.ts

import { NextApiRequest, NextApiResponse } from "next";
import connectToDatabase from "../../mongodb";
import { customAlphabet } from "nanoid";
import { COLLECTION_NAMES } from "../../types";

const characters =
  "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
const getHash = customAlphabet(characters, 4);

export default async function CreateLink(
  request: NextApiRequest,
  response: NextApiResponse
) {
  const apiKey = request.headers["api-key"] as string;
  if (request.method !== "POST" || apiKey !== process.env.API_KEY) {
    return response.status(405).json({
      type: "Error",
      code: 405,
      message: "Only POST method is accepted on this route",
    });
  }
  const { link } = request.body;

  if (!link) {
    response.status(400).send({
      type: "Error",
      code: 400,
      message: "Expected {link: string}",
    });
    return;
  }
  try {
    const database = await connectToDatabase();
    const urlInfoCollection = database.collection(COLLECTION_NAMES["url-info"]);
    const hash = getHash();
    const linkExists = await urlInfoCollection.findOne({
      link,
    });
    const shortUrl = `${process.env.HOST}/${hash}`;
    if (!linkExists) {
      await urlInfoCollection.insertOne({
        link,
        uid: hash,
        shortUrl: shortUrl,
        createdAt: new Date(),
      });
    }
    response.status(201);
    response.send({
      type: "success",
      code: 201,
      data: {
        shortUrl: linkExists?.shortUrl || shortUrl,
        link,
      },
    });
  } catch (e: any) {
    response.status(500);
    response.send({
      code: 500,
      type: "error",
      message: e.message,
    });
  }
}*
```

## *将短链接重定向到目标*

*现在我们可以创建短链接，让我们添加将用户重定向到实际目的地的逻辑。*

*为此，我们可以在 Next.js 应用程序中创建一个动态路由，并在服务器端编写重定向逻辑。*

```
*// ./pages/[hash].tsximport { NextApiRequest, NextApiResponse, NextPage } from "next";
import Head from "next/head";
import connectToDatabase from "../mongodb";
import { COLLECTION_NAMES } from "../types";export async function getServerSideProps(request: NextApiRequest) {
  const hash = request.query.hash as string;
  const database = await connectToDatabase();
  const campaign = await database
    .collection(COLLECTION_NAMES["url-info"])
    .findOne({ uid: hash }); if (campaign) {
    return {
      redirect: {
        destination: campaign.link,
        permanent: false,
      },
    };
  } return {
    props: {},
  };
}const HashPage: NextPage = () => {
  return (
    <div>
      <Head>
        <title>URL Shortener</title>
        <meta name="description" content="Generated by create next app" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <h1>Requested link not found</h1>
    </div>
  );
};export default HashPage;*
```

*如果数据库中有`hash`值，该页面会将用户重定向到目的地，否则会显示“未找到链接”消息。*

# *主办；主持*

*主持这个项目是小菜一碟，因为 Next.js 与 Vercel 的集成非常出色。*

*简化的步骤列表:*

1.  *将 Next.js 项目推送到 GitHub 存储库*
2.  *进入 [https://vercel.app](https://vercel.app) ，用你的 GitHub 账号登录*
3.  *通过点击 Vercel 仪表板上的“New Project”按钮导入`url-shortener`存储库。*

*你也可以在这里详细阅读[。](https://vercel.com/docs/concepts/projects/overview)*

*完成上述步骤后，进入项目设置，将我们在`.env.local`文件中定义的环境变量添加到 Vercel 项目的环境变量中。*

> **您也可以从设置中将您的自定义域连接到此项目。**

*🎉Tada！你的网址缩写已经准备好了，现在可以托管了。*

# *下一步是什么？*

*嗯，你可以像我一样继续使用这个项目作为 REST API，或者你可以创建一个前端，使它成为一个 web 应用程序。*

> **在使其成为公共 web 应用程序之前，请确保您添加了额外的安全性。**

*您可以从这个 [GitHub Repo](https://github.com/Anshuman71/url-shotener) 中克隆这个项目。*

*这篇文章并不是要在生产中遵循，而只应该作为学习的目的。*

*在上面的方法中可以进行许多优化，比如使用更好的数据库或适当地索引它以使它更快。*

*希望这篇文章对你有帮助！如果您有任何反馈或问题，请随时在下面的评论中提出。*

*更多此类内容，请关注我的 [Twitter](https://twitter.com/sun_anshuman)*

> **直到下一次**

*![](img/4b46a85d6b9838f1ffd64b9346dc0186.png)*

**原载于 2022 年 3 月 14 日*[*https://theanshuman . dev*](https://theanshuman.dev/articles/create-your-own-url-shortener-with-nextjs-and-mongodb-in-10-minutes-4fg)*。**

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**