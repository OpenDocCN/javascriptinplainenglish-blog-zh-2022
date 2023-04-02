# Prisma 4.7 引入了客户端扩展

> 原文：<https://javascript.plainenglish.io/prisma-4-7-introduces-client-extensions-ce8030c155f1?source=collection_archive---------4----------------------->

![](img/fac7f59d4938fc872e56ec8115fd70f5.png)

Photo by [benjamin lehman](https://unsplash.com/@benjaminlehman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着 Prisma 4.7 的发布，[客户端扩展](https://www.prisma.io/docs/concepts/components/prisma-client/client-extensions)现已推出(作为预览功能)。它们允许您使用自定义行为扩展通用 Prisma 客户端，如自定义查询、客户端和模型方法以及结果。今天，我们将看看如何使用它，以及一些更常见的用例可能是什么。

# **使用客户端扩展**

使用 Prisma 导航到一个项目，或创建一个新项目。然后修改您的`schema.prisma`以包含`clientExtensions`预览功能。

```
generator client {
    provider = "prisma-client-js"
    previewFeatures = ["clientExtensions"]
}
```

使用以下工具重新生成您的 Prisma 客户端:

```
npx primsa generate
```

# **扩展客户端**

客户端扩展目前允许您修改 Prisma 客户端的 4 个方面。顶级客户端、您的模型、查询和查询结果。为了扩展客户端，调用`$extends`方法。您将扩展作为参数传入，函数返回一个新扩展的客户端。

```
import { PrismaClient } from '@prisma/client'

export const prisma = new PrismaClient()

export const xprisma = prisma
  .$extends({
    // extend the prisma client here
  })
```

让我们看一些这种行为的例子。

**自定义查询**

假设我的模式中有以下模型，定义了一个用户:

```
model User {
    id String @id @default(cuid())
    email String
    firstName String
    lastName String
    private Boolean @default(false)
}
```

作为我的应用程序的一部分，人们可以查看所有用户的个人资料列表，但正如你从模型中看到的，用户可能会将他们的个人资料保密。使用 Prisma client extensions，我可以创建一个自定义的 findMany 查询来自动过滤公共帐户。

```
export const xprisma = prisma
  .$extends({
    query: {
      user: {
        async findMany({ model, operation, args, query }) {
          args.where = { private: false, ...args.where }
          const users = await query(args)
          return query(args)
        }
      }
    }
  })
```

**自定义客户端方法**

使用与上面相同的模型，让我们假设我想使用一个用户的电子邮件来获得他的帐户。我可以设计一个查询，但是在这个例子中，我将创建一个自定义方法，我可以在代码的其他地方重用它。

```
export const xprisma = prisma
  .$extends({
    model: {
      user: {
        findByEmail: async (email: string) => {
          return prisma.user.findFirst({
            where: { email },
          });
        }
      }
    }
  })
```

**修改结果对象**

除了修改查询和创建自定义方法之外，还可以修改响应对象。这允许您修改字段，添加全新的字段，甚至添加您自己的方法。

Prisma docs 中的这个例子展示了一个很好的例子。在示例中，只要结果包含`firstName`和`lastName`查询，我们就添加一个额外的字段`fullName`。

```
export const xprisma = prisma
  .$extends({
    result: {
      user: {
        fullName: {
          needs: { firstName: true, lastName: true },
          compute(user) {
            return `${user.firstName} ${user.lastName}`
          }
        }
      }
    }
  })
```

向结果中添加方法的示例可能如下所示。假设我们有一个博客，每篇博文都有一个增量 id。

```
model Post {
  id Int @id @default(autoincrement())
  title String
  content String
}
```

我们通过添加返回博客中下一篇文章的`next`方法来扩展结果。

```
export const xprisma = prisma
  .$extends({
    result: {
      post: {
        next: {
          needs: { id: true },
          compute(post) {
            return () => prisma.post.findUnique({where: {id: post.id+1}})
          }
        }
      }
    }
  })
```

现在当我们用 Prisma 从 db 抓取一个帖子时，可以通过调用`.next()`找到下一个。

```
// get the first post
let post = await xprisma.post.findUnique({where: {id: 1}})

// get the next post
let nextPost = await post?.next()
```

请注意，如果您计划将响应发送给发出请求的客户端应用程序，方法不能序列化，所以要么去掉它们，要么避免在这种情况下使用它们(或者添加一个方法来返回处理过的数据？).

# **共享扩展**

Prisma 有[关于如何创建可以使用](https://www.prisma.io/docs/concepts/components/prisma-client/client-extensions/shared-extensions) [npm](https://www.npmjs.com/) 共享的扩展的优秀文档。简而言之，您可以使用`Prisma.defineExtension`和前缀`$allModels`创建一个扩展名(将来可能会更多)。即使你的扩展在另一个文件或…另一个包中，这也能在你的客户机中保持类型推断。

Prisma 建议对 npm 包使用`prisma-extension-<package-name>`命名约定。这使得寻找扩展变得容易，特别是如果将来它们变成了一件普通的事情。

# **结论**

Prisma 为服务器/数据库通信层带来的第一类类型支持确实令人难以置信，Prisma 客户端扩展带来了许多新的可能性。我迫不及待地想看看人们用这个开发了什么。无论是更强大的查询、不同的结果处理方法，还是其他完全疯狂的事情。

这只是一个小介绍，所以请务必查看[客户端扩展](https://www.prisma.io/docs/concepts/components/prisma-client/client-extensions)文档，以及 [4.7 版本](https://github.com/prisma/prisma/releases/tag/4.7.0)的其余部分。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***