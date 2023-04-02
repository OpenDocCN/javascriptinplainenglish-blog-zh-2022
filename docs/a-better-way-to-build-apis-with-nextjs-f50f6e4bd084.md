# 用 NextJS 构建 API 的更好方法

> 原文：<https://javascript.plainenglish.io/a-better-way-to-build-apis-with-nextjs-f50f6e4bd084?source=collection_archive---------6----------------------->

![](img/13c6b91b23b0c84a5ebf631d4c133ba5.png)

luis gomes

上个月，我受命为一家新闻出版物开发一款全栈应用，我决定利用这个机会学习 NextJS。我不得不说——它真的很棒。这很容易上手，我对最终的结果非常满意。

也就是说，在开发过程中，我不得不做出相当多困难的设计决策。NextJS 在如何组织服务器端代码方面提供了很大的灵活性。灵活性带来自由，但自由也带来责任。

为我的应用程序设计一个可伸缩的后端需要在各种需求之间进行折衷:

1.  **无服务器**。与我过去构建的大多数后端不同，我不能只保持一个数据库连接。相反，无服务器函数需要为每个请求打开一个新的连接，无论是对 API 的请求还是对页面的请求。
2.  **认证**。我想使用 JWT 对每个请求的用户进行身份验证，如果用户未经授权，根据页面返回 401。
3.  **简单明了的错误处理**。为用户可能犯的每个错误手动调用`res.status(4xx).json({ error: "etc" })`是很烦人的。我能找到一个允许我写类似于`throw new UnauthorizedError()` ( [有点像 NestJS](https://medium.com/better-programming/stop-using-express-js-to-make-web-servers-faed1942eaf3) )的解决方案吗？
4.  **干码**。代码重复告诉我，我没有用正确的方式看待问题。在客户机和服务器之间共享代码的能力是选择 NextJS 的一个主要因素。作为 TypeScript 的忠实信徒，共享类型定义也是如此。

经过大量的重构和修补，我找到了一个优雅的解决方案，成功地解决了所有这些需求。

# 连接到数据库

我首先编写了一个简单的函数，它连接到我的数据库，初始化模型，并返回连接供以后使用。

```
async function connectToDB() {
  const conn = await mongoose.createConnection(DATABASE_URL as string);
  conn.model("Article", ArticleSchema);
  conn.model("Sub", SubSchema);
  conn.model("User", UserSchema);
  return conn;
}
```

简单到目前为止。不幸的是，我在这里定义的模型立即失去了它们的类型。也就是说，如果我尝试使用其中一个模型，像这样:

```
conn.models.Article.findOneById(id);
```

返回类型将是`any`。对类型安全没有好处。

为了解决这个问题，我为我的数据库创建了一个类型:

```
export type MyDB = mongoose.Connection & {
  models: {
    User: Model<IUser>;
    Article: Model<IArticle>;
    Sub: Model<ISub>;
  };
};
```

并返回`conn`作为`MyDB`:

```
async function connectToDB() {
  const conn = await mongoose.createConnection(DATABASE_URL as string);
  conn.model("Article", ArticleSchema);
  conn.model("Sub", SubSchema);
  conn.model("User", UserSchema);
  return conn as MyDB;
}
```

我们现在可以打开到数据库的连接。但是有一个问题——如上所述，在无服务器应用程序中打开和重用单个数据库连接是不可行的，因为代码只是一个大型函数，一旦函数调用完成，它就会丢失任何状态。

相反，每次我们想要查询数据库时，我们都需要打开一个新的连接，并在完成后关闭它。为此，我编写了一个包装函数，它接受一个回调函数，数据库`conn`被传递给这个函数，如下所示:

```
export async function withDB<K>(
  callback: (conn: MyDB) => Promise<K>;
): Promise<K> {
  const conn = await connectToDB();
  const result = await callback(conn);
  conn.close();
  return result as K;
}
```

我现在已经完全隐藏了连接和断开数据库的逻辑。我只要打电话给`withDB()`。

# 请求处理程序

让我们假设一个用户向`/users`发出帖子请求注册。我们需要一些代码来处理这个请求，称为**处理程序**。NextJS 为我们提供了一个创建处理程序的基本 API，但是在摆弄了几分钟之后，我意识到我可以设计出更加健壮的东西。

## 什么是真正的处理程序？

开箱即用，NextJS 让您负责根据请求的 HTTP 方法选择要调用的服务器代码。我的第一个目标是将这种无趣和重复的行为抽象掉。

为此，我们将改变处理程序的概念。让我们把处理特定路径请求的函数想象成处理特定 HTTP 方法对特定路径的请求**的函数。这样，我们可以定义完全独立的函数来处理对`/users`的 POST 请求，并将请求发送到相同的路径。**

因此，处理程序接受一些参数——`req`对象读取查询参数或请求体；`res`对象，比如说，需要写头；`conn`对象，以便处理程序可以轻松地访问数据库；以及发出请求的用户的`userId`，以防处理程序需要知道是谁发出的请求。

此外，处理程序不应该负责实际上*发送*一个响应，而只是确定*响应应该是什么*。无论函数返回什么值，最终都会在响应中以 JSON 的形式发送回来。

这为方法处理程序产生了以下类型定义:

```
export type MethodHandler<BODY, RESPONSE> = (params: {
  req: Omit<NextApiRequest, "body"> & { body: BODY };
  res: NextApiResponse;
  conn: MyDB;
  userId: string | undefined;
}) => Promise<RESPONSE>;
```

## 处理各种方法

记住一个`MethodHandler`是针对一个特定的 HTTP 方法的，但是下一个 API routes 希望您导出一个函数，这个函数可以处理该路径上的每一个 HTTP 方法。

让我们创建一个函数，它将 HTTP 方法映射到它们各自的方法处理程序，并返回另一个函数，该函数接受对特定路径的请求，并根据请求的方法调用相应的处理程序。

首先，我们将为这样的地图定义一种类型:

```
export type Methods = "get" | "post" | "put" | "patch" | "delete";

export type MethodHandlers = {
  [key in Methods]?: MethodHandler<any, any>;
};
```

接下来，我们创建一个函数，该函数选择适当的方法处理程序，通过数据库连接执行它，并用处理程序返回的任何对象进行响应:

```
export default function createHandler(methodHandlers: MethodHandlers) {
  return async (req: NextApiRequest, res: NextApiResponse<any>) => {
    const response = await withDB((conn) => {
      const handler =
        methodHandlers[(req.method?.toLowerCase() as Methods) ?? "get"];
      if (handler) {
        const userId = getUserIdFromReq(req);
        return handler({ req, res, conn, userId });
      }
    });
    const statusCode = req.method === "GET" ? 200 : 201;
    res.status(statusCode);
    res.json(response);
  };
}
```

## 处理错误

对于每个 API 请求，都有各种错误的无数可能性。我没有去记忆状态代码、错误响应格式，也没有去创建一个早期返回的复杂网络，我决定一个更好的设计是简单地扩展 Javascript 的`Error`类。

首先，我定义了一些常见的错误类型:

```
export class NotFoundError extends Error {
  constructor(message?: string) {
    super(message);
    this.name = "NotFoundError";
  }
}

export class UnauthorizedError extends Error {
  ...
}
```

然后，我创建了一个从错误类别到状态代码的映射:

```
const errorStatusCodes = {
  ValidationError: 400,
  NotFoundError: 404,
  UnauthorizedError: 401,
  MethodNotAllowedError: 405,
  ConflictError: 409,
};
```

最后，我定义了一个助手函数，它接受一个`res`对象和任何错误，并适当地处理它:

```
export function handleError(error: Error, res: NextApiResponse) {
  if (Object.hasOwn(errorStatusCodes, error.name)) {
    res
      .status(errorStatusCodes[error.name as keyof typeof errorStatusCodes])
      .json({ name: error.name, message: error.message });
  } else {
    console.error(error);
    res
      .status(500)
      .json({ name: "ServerError", message: "Internal server error" });
  }
}
```

然后，我在上面定义的`createHandler()`函数中使用了一个`try/catch`,将它们组合在一起:

```
export default function createHandler(methodHandlers: MethodHandlers) {
  return async (req: NextApiRequest, res: NextApiResponse<any>) => {
    try {
      const response = await withDB((conn) => {
        const handler =
          methodHandlers[(req.method?.toLowerCase() as Methods) ?? "get"];
        if (handler) {
          const userId = getUserIdFromReq(req);
          return handler({ req, res, conn, userId });
        } else {
          throw new MethodNotAllowedError("Method not allowed");
        }
      });
      const statusCode = req.method === "GET" ? 200 : 201;
      res.status(statusCode);
      res.json(response ?? {});
    } catch (e) {
      handleError(e as Error, res);
    }
  };
}
```

# 创建我们的第一个处理程序

完成这些抽象之后，就该为创建用户定义一个处理程序了:

```
type CreateUserRequest = {
  name: string;
  email: string;
  password: string;
};
type CreateUserResponse = IUser;

const createUserHandler: MethodHandler<
  CreateUserRequest,
  CreateUserResponse
> = async ({ req, conn, userId }) => {
  const { name, email, password } = req.body;
  const hashedPassword = await hashPassword(password);
  try {
    const newUser = await conn.models.User.create({
      name: name,
      email: email,
      password: hashedPassword,
    });
    return newUser;
  } catch (e) {
    throw new ConflictError("Name or email already in use");
  }
};
```

为了实际定义一个 NextJS 可以用来处理 API 请求的函数，我们必须将这个处理程序传递到`createHandler()`中，并从`pages/api`中的一个文件中导出它，如下所示:

```
export default createHandler({
  post: createUserHandler,
});
```

# 发出 API 请求

我们已经有了一个抽象，它将 NextJS 的默认 API 打得落花流水。但是不要忘记最后的要求:在客户机和服务器之间共享逻辑和类型。

请注意，`MethodHandlers`对象也拥有我们创建一个能够*发送*请求的函数所需的几乎所有信息。它唯一缺少的是处理程序的路径；NextJS 从文件在项目中的位置知道这一点，但是这个路径只能作为字符串提供。

让我们从定义一个可以发出请求的函数的类型开始:

```
export type RequestMaker<BODY, RESPONSE> = (body: BODY) => Promise<RESPONSE>;
```

我们的目标是编写一个函数，它可以接受一个`MethodHandlers`对象——与提供给`createHandler()`的对象相同——并使用它来返回函数，然后这些函数可以用于*发出*请求。

这要求我们*重新映射*对象`MethodHandlers`。我们将接收一个从 HTTP 方法到它们的处理程序的映射，并返回一个从 HTTP 方法到它们对应的`RequestMaker`函数的映射。我们可以用以下类型来表示这种重新映射:

```
export type RequestMakerReturn<K extends MethodHandlers> = {
  [key in keyof K]: K[key] extends MethodHandler<infer B, infer R>
    ? RequestMaker<B, R>
    : never;
};
```

如果你害怕这种类型，不要害怕！查看我在难度增加指南中的[打字稿，了解这是如何工作的。](https://medium.com/javascript-in-plain-english/the-fundamentals-of-typescript-in-increasing-levels-of-difficulty-c54bab69fbb9)

## 编写函数

我们终于准备好好玩的部分了。我们需要一个接受两件事的函数:

1.  请求者发出请求的路径
2.  返回类型(`RequestMakerReturn`)所基于的`MethodHandlers`对象

并返回重新映射的类型(`RequestMakerReturn`)。

对于任何复杂的函数，从签名开始都是最简单的:

```
export default function createRequestMakers<K extends MethodHandlers>(
  path: string,
  requestMakerData: K
): RequestMakerReturn<K> {
  ...
}
```

为了重新映射一个对象，我们将它分解成一个条目数组(键/值对)，映射*到*数组，并从新的条目重新构建它。这是此类操作的模板:

```
export default function createRequestMakers<K extends MethodHandlers>(
  path: string,
  requestMakerData: K
): RequestMakerReturn<K> {
  return Object.fromEntries(
    Object.entries(requestMakerData).map(([method]) => {
      const requestMaker = ...
      return [method, requestMaker];
    })
  ) as RequestMakerReturn<K>; 
}
```

现在，我们需要做的就是定义一个请求生成器函数，根据请求的方法和路径发送请求，就像这样:

```
export default function createRequestMakers<K extends MethodHandlers>(
  path: string,
  requestMakerData: K
) {
  return Object.fromEntries(
    Object.entries(requestMakerData).map(([method]) => {
      const requestMaker = async (body: any) => {
        const res = await axios(path, {
          method,
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            ...body,
          },
        });
        return res.data;
      };
      return [method, requestMaker];
    })
  ) as RequestMakerReturn<K>;
}
```

## 错误处理

剩下唯一要做的就是在客户端添加错误处理。我们可以重用为服务器定义的自定义错误类。

任何非 OK ( `>200`)响应都会导致 Axios 抛出一个`AxiosError`。我们的服务器端错误处理程序将类名和消息作为响应中的数据发送，我们可以提取这些数据并在客户端使用它们来重新抛出相同的错误对象:

```
export function propagateError(status: number, responseData: any) {
  switch (status) {
    case 400:
      throw new ValidationError(responseData.message);
    case 401:
      throw new UnauthorizedError(responseData.message);
    case 404:
      throw new NotFoundError(responseData.message);
    case 405:
      throw new MethodNotAllowedError(responseData.message);
    case 409:
      throw new ConflictError(responseData.message);
    default:
      throw new Error(responseData.message);
  }
}
```

最后，将这个整合到`createRequestMakers`中就像`try/catch`一样简单:

```
export default function createRequestMakers<K extends MethodHandlers>(
  path: string,
  requestMakerData: K
) {
  return Object.fromEntries(
    Object.entries(requestMakerData).map(([method]) => {
      const requestMaker = async (body: any) => {
        try {
          const res = await axios(path, {
            method,
            headers: {
              "Content-Type": "application/json",
            },
            data: {
              ...body,
            },
          });
          return res.data;
        } catch (e) {
          if (e instanceof AxiosError) {
            propagateError(e.status ?? 500, e.response?.data);
          }
        }
      };
      return [method, requestMaker];
    })
  ) as RequestMakerReturn<K>;
}
```

# 把所有的放在一起

让我们回到我们在`/pages/api`中的文件，在这里我们定义了我们的`MethodHandlers`对象并导出了 NextJS 的请求处理程序。

我们现在可以将同一个对象传递给`createRequestMakers()`来获得发送请求的函数:

```
const methodHandlers = {
  post: createUserHandler,
};

export default createHandler(methodHandlers);

export const { post } = createRequestMakers(
  "/users",
  methodHandlers
);
```

您可能希望用更具描述性的名称导出您的请求生成器函数，而不仅仅是“post”。我是这样做的:

```
export const { post: makeCreateUserRequest } = createRequestMakers(
  "/users/createUser",
  methodHandlers
);
```

现在，从任何 React 组件，您都可以像这样创建一个用户:

```
const user = await makeCreateUserRequest({
  name: "test-username",
  email: "test@email.com",
  password: "testpassword",
});
```

清晰的界面，优雅一致的错误处理，以及客户机和服务器之间共享的类型定义。使用这种设计，很难编写有错误的代码，所有平凡的、重复的逻辑都被抽象掉了。软件开发人员还想要什么？

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*