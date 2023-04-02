# 主持一个关于 Firebase 函数的 NestJS 应用程序:完全指南

> 原文：<https://javascript.plainenglish.io/nestjs-with-firebase-the-complete-guide-aa0ade41cdef?source=collection_archive---------0----------------------->

## 使用 Firebase 身份验证和 Firestore 在 Firebase 函数上托管 NestJS 应用程序的分步指南。

![](img/9f1d6bf0926598c51d6b349535df8848.png)

在本文中，我将向您提供使用 NestJS 和 Firebase 创建 API 所需的所有信息，包括在 Firebase 函数上托管 NestJS 应用程序、使用 Firebase 身份验证和 Firestore，让我们开始吧。

*注意:我假设在本文中你已经知道了 NestJS 和 Firebase(但只是理解本文所需的基础知识)，所以我不会详细解释它们。本文旨在帮助您以最佳方式将两者联系起来。*

下面是我们将要经历的步骤:

1.[创建项目](#c8b5)
2。[添加 Firebase 功能](#46b1)
3。[部署到 Firebase 功能](#9828)
4。[添加 Firebase 认证](#94b5)
5。[启用 CORS](#3410)
6。[连接 NestJS 和 Firebase Admin](#a1ef)
7。增强我们的脚本以获得更好的开发者体验。[连接 Firestore](#44ca)

# 1.创建项目

首先，您需要通过运行以下命令来安装 NestJS 和 Firebase 的全局包:

```
npm install -g firebase-tools @nestjs/cli
```

然后创建您的项目:

```
nest new todo
```

# 2.添加 Firebase 函数

首先，你需要从[https://console.firebase.google.com/](https://console.firebase.google.com/)在 Firebase 中创建一个项目，然后你需要将你的计划更改为 Blaze(否则，Firebase 功能将无法工作)，从左侧边栏菜单点击功能，然后点击开始，直到你完成向导

然后转到项目并执行以下命令:

```
firebase login
firebase init functions
```

然后选择`Use an existing project`并选择您刚刚创建的项目。

然后继续。

```
? What language would you like to use to write Cloud Functions? TypeScript
? Do you want to use ESLint to catch probable bugs and enforce style? No
+  Wrote functions/package.json
+  Wrote functions/tsconfig.json
+  Wrote functions/src/index.ts
+  Wrote functions/.gitignore
? Do you want to install dependencies with npm now? No
```

你会发现一个名为 functions 的新文件夹，里面有上面提到的文件。

我们只关心它里面的 package.json，我们需要把它和我们拥有的主 package.json 合并。

为此，我们将把所有脚本从`functions/package.json`复制到我们的主`package.json`，除了构建和启动，因为它们已经在那里了。

然后复制引擎和主属性以及除 TypeScript 之外的所有依赖项(因为它已经在主`package.json`中)。

然后删除`functions`文件夹，并在项目的根目录下创建一个新文件`index.ts`,内容如下:

```
import { NestFactory } from '@nestjs/core';
import { ExpressAdapter } from '@nestjs/platform-express';
import * as express from 'express';
import * as functions from 'firebase-functions';import { AppModule } from './src/app.module';const expressServer = express();const createFunction = async (expressInstance): Promise<void> => {
  const app = await NestFactory.create(
    AppModule,
    new ExpressAdapter(expressInstance),
  );await app.init();
};export const api = functions.https.onRequest(async (request, response) => {
  await createFunction(expressServer);
  expressServer(request, response);
});
```

然后将`package.json`中的 main 改为指向`dist/index.js`而不是`lib/index.js`。

所以，`package.json`应该是这样的:

```
{
  "name": "todo",
  "version": "0.0.1",
  "description": "",
  "author": "",
  "private": true,
  "license": "UNLICENSED",
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json",
    "serve": "npm run build && firebase emulators:start --only functions",
    "shell": "npm run build && firebase functions:shell",
    "deploy": "firebase deploy --only functions",
    "logs": "firebase functions:log"
  },
  "engines": {
    "node": "14"
  },
  "main": "dist/index.js",
  "dependencies": {
    "@nestjs/common": "^8.0.0",
    "@nestjs/core": "^8.0.0",
    "@nestjs/platform-express": "^8.0.0",
    "reflect-metadata": "^0.1.13",
    "rimraf": "^3.0.2",
    "rxjs": "^7.2.0",
    "firebase-admin": "^9.8.0",
    "firebase-functions": "^3.14.1"
  },
  "devDependencies": {
    "@nestjs/cli": "^8.0.0",
    "@nestjs/schematics": "^8.0.0",
    "@nestjs/testing": "^8.0.0",
    "@types/express": "^4.17.13",
    "@types/jest": "^26.0.24",
    "@types/node": "^16.0.0",
    "@types/supertest": "^2.0.11",
    "@typescript-eslint/eslint-plugin": "^4.28.2",
    "@typescript-eslint/parser": "^4.28.2",
    "eslint": "^7.30.0",
    "eslint-config-prettier": "^8.3.0",
    "eslint-plugin-prettier": "^3.4.0",
    "jest": "27.0.6",
    "prettier": "^2.3.2",
    "supertest": "^6.1.3",
    "ts-jest": "^27.0.3",
    "ts-loader": "^9.2.3",
    "ts-node": "^10.0.0",
    "tsconfig-paths": "^3.10.1",
    "typescript": "^4.3.5",
    "firebase-functions-test": "^0.2.0"
  },
  "jest": {
    "moduleFileExtensions": [
      "js",
      "json",
      "ts"
    ],
    "rootDir": "src",
    "testRegex": ".*\\.spec\\.ts$",
    "transform": {
      "^.+\\.(t|j)s$": "ts-jest"
    },
    "collectCoverageFrom": [
      "**/*.(t|j)s"
    ],
    "coverageDirectory": "../coverage",
    "testEnvironment": "node"
  }
}
```

但是请不要复制和粘贴，因为这可能有过时的依赖和/或来自 NestJS 或 Firebase 的一些其他更改，我们需要合并生成的两个`package.json`。

最后但并非最不重要的是修改`firebase.json`文件，因为默认情况下它会查找 functions 文件夹，所以我们需要使它成为`"source": "."`这意味着查看根文件夹而不是 functions one，它看起来像这样:

```
{
  "functions": {
    "predeploy": "npm --prefix \"$RESOURCE_DIR\" run build",
    "source": "."
  }
}
```

现在您需要运行:

```
npm run serve
```

如果一切正常，您将会收到一条很长的消息，其中一条是这样的:

```
functions[us-central1-api]: http function initialized ([http://localhost:5001/todo-7b299/us-central1/api](http://localhost:5001/todo-7b299/us-central1/api)).
```

在浏览器中打开这个 URL 来验证它是否真的在工作，它应该显示`Hello World!`

# 3.部署到 Firebase 功能

我们需要运行:

```
npm run deploy
```

如果一切正常，它会给你一条很长的信息，只有一行:

```
Function URL (api(us-central1)): [https://us-central1-todo-7b299.cloudfunctions.net/api](https://us-central1-todo-7b299.cloudfunctions.net/api)
```

*如果你遇到一个错误，可能是因为你选择的引擎不被 Firebase 支持，或者你在改变* `*package.json*` *后没有运行* `*npm i*` *，或者你的计划不火。*

如果你打开这个网址，它可能会给你:

```
Error: Forbidden
Your client does not have permission to get URL /api from this server.
```

这是因为它尚未公开，要公开它，您需要执行以下操作:

1.  去消防基地控制台[https://console.firebase.google.com/](https://console.firebase.google.com/u/0/)。
2.  选择您的项目。
3.  转到“功能”选项卡。
4.  选择功能名称旁边的三个点，然后选择`Detailed usage stats`，这将带您进入谷歌云。
5.  转到“权限”选项卡并添加权限。
6.  如下图所示，选择“所有用户”主体和云函数调用程序规则并保存。

![](img/a39bd20fbf1acc96e0fb2a5091201c91.png)

make function publicly accessed

现在刷新网址，它也应该给你“你好世界！”这次。

恭喜你！您已经将您的 NestJS 应用程序部署到 Firebase 函数。

# 4.添加 Firebase 身份验证

*注意:您需要启用用户如何进行身份验证，但通常这是前端/移动的一部分。*

让我们从创建一个 todo 资源开始，使用:

```
nest g res todo
```

让我们通过删除`app.controller.ts`和`app.service.ts`以及它们在`app.module.ts`中的提及来清理一下这个项目。

然后，我们需要使所有的 todo 路由只能通过 Firebase JWT 令牌访问，因为现在如果你去`api/todo`它会显示“此操作返回所有 todo ”,而它只显示如果它是一个认证的请求返回。

首先，让我们安装所有必需的依赖项:

```
npm i @nestjs/passport passport passport-firebase-jwt
```

然后，让我们用以下代码创建一个名为`auth`的全局模块:

```
nest g mo auth
```

并在`@Module`前添加`@Global()`，使其可以被我们所有的模块访问。

然后在`auth`文件夹中创建一个新文件`firebase-auth.strategy.ts`，内容如下:

```
import { PassportStrategy } from '@nestjs/passport';
import { Injectable, UnauthorizedException } from '@nestjs/common';
import { Strategy, ExtractJwt } from 'passport-firebase-jwt';
import { auth } from 'firebase-admin';

@Injectable()
export class FirebaseAuthStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
    });
  }

  validate(token) {
    return auth()
      .verifyIdToken(token, true)
      .catch((err) => {
        console.warn(err);
        throw new UnauthorizedException();
      });
  }
}
```

然后在`auth.module.ts`中使用它，看起来如下:

```
import { Global, Module } from '@nestjs/common';
import { PassportModule } from '@nestjs/passport';
import { FirebaseAuthStrategy } from './firebase-auth.strategy';

@Global()
@Module({
  imports: [PassportModule.*register*({ defaultStrategy: 'firebase-jwt' })],
  providers: [FirebaseAuthStrategy],
  exports: [PassportModule],
})
export class AuthModule {}
```

然后最后在`TodoController`里加上`@UseGuards(AuthGuard())`。

现在当你进入`[http://localhost:5001/todo-7b299/us-central1/api/todo](http://localhost:5001/todo-7b299/us-central1/api/todo)`时，它应该返回 401(但是你需要重启服务器)。

# 5.启用 CORS

现在让我们开始测试我们的 API。

我创建了一个非常简单的 Angular 项目来测试 API。

[](https://github.com/robertIsaac/angular-todo) [## GitHub-robertIsaac/angular-todo

### 此项目是使用 Angular CLI 版本 12.2.2 生成的。为开发服务器运行 ng serve。导航到…

github.com](https://github.com/robertIsaac/angular-todo) 

让我们克隆它，修改 environment.ts，看看我们的 API 能否工作。

你将面临的第一个问题是 CORS 错误。

要启用它，只需在 index.ts 文件中添加`app.enableCors()`。

要那样:

```
const createFunction = async (expressInstance): Promise<void> => {
  const app = await NestFactory.create(
    AppModule,
    new ExpressAdapter(expressInstance),
  );
  **app.enableCors();**
  app.useGlobalPipes(new ValidationPipe());
  await app.init();
};
```

完成添加后，请重启`npm run serve`。

你会发现 CORS 错误消失了，但是抛出了一个新的错误:

```
[Nest] 16468  - 08/06/2021, 10:51:49 AM   ERROR [ExceptionsHandler] The default Firebase app does not exist. Make sure you call initializeApp() before using any of the Firebase services.
```

# 6.用 Firebase Admin 连接 NestJS

现在的问题是，NestJS 还不能连接 Firebase，它只能部署代码。

用 Firebase 连接有很多方法，但我更喜欢用 Firebase Config。因此，证书不在代码中，这使它更安全，而且它在本地和云上都工作，而不必以多种方式提供它们。

所以第一步是下载凭证文件。

你会这样截图:

![](img/c47fbcbda5357982927fea8a187fff60.png)

这将下载一个 JSON 文件。

现在您需要对它进行编码，只需使用`JSON.stringify`。

## 之前:

```
{
  "type": "service_account",
  "project_id": "todo-7b299",
  "private_key_id": "foobar",
  "private_key": "-----BEGIN PRIVATE KEY-----...",
  "client_email": "something.iam.gserviceaccount.com",
  "client_id": "123",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com"
}
```

## 之后:

```
"{\"type\":\"service_account\",\"project_id\":\"todo-7b299\",\"private_key_id\":\"foobar\",\"private_key\":\"-----BEGIN PRIVATE KEY-----...\",\"client_email\":\"something.iam.gserviceaccount.com\",\"client_id\":\"123\",\"auth_uri\":\"[https://accounts.google.com/o/oauth2/auth\](https://accounts.google.com/o/oauth2/auth\)",\"token_uri\":\"[https://oauth2.googleapis.com/token\](https://oauth2.googleapis.com/token\)",\"auth_provider_x509_cert_url\":\"[https://www.googleapis.com/oauth2/v1/certs\](https://www.googleapis.com/oauth2/v1/certs\)",\"client_x509_cert_url\":\"[https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com\](https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com\)"}"
```

现在，您可以执行以下命令:

```
firebase functions:config:set todo_firebase_config="{\"type\":\"service_account\",\"project_id\":\"todo-7b299\",\"private_key_id\":\"foobar\",\"private_key\":\"-----BEGIN PRIVATE KEY-----...\",\"client_email\":\"something.iam.gserviceaccount.com\",\"client_id\":\"123\",\"auth_uri\":\"[https://accounts.google.com/o/oauth2/auth\](https://accounts.google.com/o/oauth2/auth\)",\"token_uri\":\"[https://oauth2.googleapis.com/token\](https://oauth2.googleapis.com/token\)",\"auth_provider_x509_cert_url\":\"[https://www.googleapis.com/oauth2/v1/certs\](https://www.googleapis.com/oauth2/v1/certs\)",\"client_x509_cert_url\":\"[https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com\](https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com\)"}"
```

要验证它是否工作，运行`firebase functions:config:get`。

```
$ firebase functions:config:get
{
  "todo_firebase_config": {
    "project_id": "todo-7b299",
    "auth_uri": "[https://accounts.google.com/o/oauth2/auth](https://accounts.google.com/o/oauth2/auth)",
    "client_x509_cert_url": "[https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com](https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-foo.iam.gserviceaccount.com)",
    "token_uri": "[https://oauth2.googleapis.com/token](https://oauth2.googleapis.com/token)",
    "private_key": "-----BEGIN PRIVATE KEY-----...",
    "client_email": "something.iam.gserviceaccount.com",
    "type": "service_account",
    "private_key_id": "foobar",
    "auth_provider_x509_cert_url": "[https://www.googleapis.com/oauth2/v1/certs](https://www.googleapis.com/oauth2/v1/certs)",
    "client_id": "123"
  }
}
```

现在让我们通过修改`index.ts`并添加以下内容来加载它:

```
admin.initializeApp({
  credential: admin.credential.cert(functions.config().todo_firebase_config),
  databaseURL: 'https://todo-c9f6e-default-rtdb.firebaseio.com',
});
```

现在，这在云中可以很好地工作，但在本地仍然是相同的错误，要修复它，我们需要运行一个命令让函数模拟器正常工作，那就是:

```
firebase functions:config:get > .runtimeconfig.json
```

这将把`functions:config:get`的内容返回到一个名为`.runtimeconfig.json`的文件中。

所以我们需要将这个文件添加到`.gitignore`中。

# 7.增强我们的脚本以获得更好的开发者体验

所以现在我们应该在每次开始之前运行这个命令，也就是说，以防同事修改了某些东西，或者有人第一次克隆了这个项目。

现在还有另一个问题，那就是每次我们做出改变时都需要重启我们的应用程序。

因此，我们需要一个更好的脚本来为我们处理这一切。

为此，我使用并发包。使用以下代码将其作为开发工具安装:

```
npm i -D concurrently
```

然后更改脚本，如下所示:

```
"scripts": {
  "prebuild": "rimraf dist",
  "build": "nest build",
 **"build:watch": "nest build --watch",**  "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
  "start": "nest start",
  "start:dev": "nest start --watch",
  "start:debug": "nest start --debug --watch",
  "start:prod": "node dist/main",
  "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
  "test": "jest",
  "test:watch": "jest --watch",
  "test:cov": "jest --coverage",
  "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
  "test:e2e": "jest --config ./test/jest-e2e.json",
 **"get:config": "firebase functions:config:get > .runtimeconfig.json",
  "firebase:emulator": "firebase emulators:start --only functions",
  "serve": "npm run get:config && npm run build && npm run firebase:emulator",
  "serve:watch": "concurrently npm:get:config npm:build && concurrently npm:build:watch npm:firebase:emulator",**  "shell": "npm run build && firebase functions:shell",
  "deploy": "firebase deploy --only functions",
  "logs": "firebase functions:log"
}
```

现在，您只需要运行以下命令:

```
npm run serve:watch
```

它将为您处理一切，不再需要重启应用程序。

# 8.与 Firestore 连接

最后一步是将我们的应用程序与 Firestore 连接起来，以存储我们的数据。

在我们开始之前，您必须在 [Firebase 控制台](http://console.firebase.google.com)中创建数据库。

首先是定义我们的实体和 DTO

`todo.entity.ts`

```
export class Todo {
  id: string;
  title: string;
  details: string;
  userId: string;
  createdAt: string;
}
```

`create-todo.dto.ts`

```
import { IsNotEmpty, IsString } from 'class-validator';

export class CreateTodoDto {
  @IsNotEmpty()
  @IsString()
  title: string;

  @IsString()
  details: string;
}
```

为了进行验证，我们需要安装`class-validator`和`class-transformer`依赖项，并将`app.useGlobalPipes(new ValidationPipe());`添加到我们的`index.ts`文件中。

现在我们需要将我们的服务连接到 firebase，这是完整的代码:

```
import { Inject, Injectable } from '@nestjs/common';
import { CreateTodoDto } from './dto/create-todo.dto';
import { UpdateTodoDto } from './dto/update-todo.dto';
import { firestore } from 'firebase-admin';
import { REQUEST } from '@nestjs/core';
import { Todo } from './entities/todo.entity';
import DocumentSnapshot = firestore.DocumentSnapshot;
import QuerySnapshot = firestore.QuerySnapshot;

@Injectable()
export class TodoService {
  private collection: FirebaseFirestore.CollectionReference<FirebaseFirestore.DocumentData>;

  constructor(@Inject(REQUEST) private readonly request: { user: any }) {
    this.collection = firestore().collection('todos');
  }

  async create(createTodoDto: CreateTodoDto) {
    const userId = this.request.user.uid;
    const todo: Omit<Todo, 'id'> = {
      ...createTodoDto,
      createdAt: new Date().toISOString(),
      userId,
    };

    return this.collection.add(todo).then((doc) => {
      return { id: doc.id, ...todo };
    });
  }

  findAll() {
    return this.collection
      .where('userId', '==', this.request.user.uid)
      .get()
      .then((querySnapshot: QuerySnapshot<Todo>) => {
        if (querySnapshot.empty) {
          return [];
        }

        const todos: Todo[] = [];
        for (const doc of querySnapshot.docs) {
          todos.push(this.transformTodo(doc));
        }

        return todos;
      });
  }

  findOne(id: string) {
    return this.collection
      .doc(id)
      .get()
      .then((querySnapshot: DocumentSnapshot<Todo>) => {
        return this.transformTodo(querySnapshot);
      });
  }

  async update(id: string, updateTodoDto: UpdateTodoDto) {
    await this.collection.doc(id).update(updateTodoDto);
  }

  async remove(id: string) {
    await this.collection.doc(id).delete();
  }

  private transformTodo(querySnapshot: DocumentSnapshot<Todo>) {
    if (!querySnapshot.exists) {
      throw new Error(`no todo found with the given id`);
    }

    const todo = querySnapshot.data();
    const userId = this.request.user.uid;

    if (todo.userId !== userId) {
      throw new Error(`no todo found with the given id`);
    }

    return {
      id: querySnapshot.id,
      ...todo,
    };
  }
}
```

然后在我们的控制器中，我们只需要将 id 从字符串转换为数字:

```
import {
  Body,
  Controller,
  Delete,
  Get,
  Param,
  Patch,
  Post,
  UseGuards,
} from '@nestjs/common';
import { TodoService } from './todo.service';
import { CreateTodoDto } from './dto/create-todo.dto';
import { UpdateTodoDto } from './dto/update-todo.dto';
import { AuthGuard } from '@nestjs/passport';

@UseGuards(AuthGuard())
@Controller('todo')
export class TodoController {
  constructor(private readonly todoService: TodoService) {}

  @Post()
  create(@Body() createTodoDto: CreateTodoDto) {
    return this.todoService.create(createTodoDto);
  }

  @Get()
  findAll() {
    return this.todoService.findAll();
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    **return this.todoService.findOne(id);**
  }

  @Patch(':id')
  update(@Param('id') id: string, @Body() updateTodoDto: UpdateTodoDto) {
    **return this.todoService.update(id, updateTodoDto);**
  }

  @Delete(':id')
  remove(@Param('id') id: string) {
    **return this.todoService.remove(id);**
  }
}
```

现在我们结束了。

在这个应用程序中，我们可以做很多改进，但我希望它尽可能简单。

查看我的 GitHub repo 中的完整代码:

[](https://github.com/robertIsaac/NestJS-with-Firebase) [## GitHub-robertIsaac/NestJS-with-Firebase:这是一个如何连接 NestJS 和 Firebase 的指南…

### 一个渐进式 Node.js 框架，用于构建高效且可伸缩的服务器端应用程序。嵌套框架类型脚本…

github.com](https://github.com/robertIsaac/NestJS-with-Firebase) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***