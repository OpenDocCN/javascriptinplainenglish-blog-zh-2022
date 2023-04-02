# next auth . js:next . js 的身份验证 API

> 原文：<https://javascript.plainenglish.io/nextauth-js-authentication-api-for-next-js-41ea7da062c5?source=collection_archive---------1----------------------->

![](img/b6b7e881dd5095d243b8b375fcfa64d7.png)

NextAuth.js 自诩为 Next.js 应用程序中用户注册和认证的高效开源解决方案。它的极简方法与对流行服务的内置支持相结合，允许您在几分钟内将身份验证添加到 web 应用程序流中。

**我们将建造什么？:**我们将使用 NextAuth 和 Next.js API 路由构建一个基本级别的认证 API。身份验证将包括使用 NextAuth 的 CredentialsProvider 和 bcrypt 模块的散列密码的电子邮件注册。

**安装:**通过运行以下代码，在 Next.js 应用程序中安装 NextAuth:

```
npm i next-auth
or 
yarn add next-auth
```

**环境变量:**在您的 Next.js 项目中，在项目的根目录下找到环境变量文件`.env.local`，并添加您的 web 应用程序 URL 和端口，以及一个用于 NextAuth 的`secret`，它可以是任何随机的字符串。您可以在开发过程中跳过它，但是不提供`secret`会在生产中抛出一个错误。

```
NEXTAUTH_URL=http://localhost:3000
SECRET=<any random string>
```

*注意:默认情况下，你的 Next.js 项目应该有一个. env.local 文件。如果没有，请随意手动创建一个。*

**SessionProvider:** 是 NextAuth 的`SessionProvider`施展魔法的时候了。打开 pages 目录中的`_app.tsx`文件，并添加以下代码块:

```
import "../styles/globals.css";
import type { AppProps } from "next/app";
import { SessionProvider } from "next-auth/react";

function MyApp({ Component, pageProps }: AppProps) {
return (     
<SessionProvider session={pageProps.session}>       
<Component {...pageProps} />
</SessionProvider>   
)
}
```

`SessionProvider`使我们能够利用 React 上下文跨组件共享会话对象。这反过来负责保持会话在浏览器的所有选项卡和窗口中更新和同步。

**会话钩子:**现在您已经准备好在您的`index.tsx`文件中导入 NextAuth 钩子，即`useSession`和`signOut`。

```
import { useSession, signOut } from ‘next-auth/react’;

const Page: NextPage = () => {

 const { data: session } = useSession();

return (
 <div>

 </div>
 )
}

export default Page;
```

来自`useSession`的`data:session`将包含用户的会话细节，或者如果会话不存在，它将返回 null。我们可以使用 session 对象有条件地呈现登录、注册和注销按钮。

在您的`index.tsx`的 return 语句中添加以下代码块:

```
{session && <button onClick={handleSignout}>Sign out</a>}

{!session && 
<a href="/register">Sign Up</a>
<a href="/login>Sign In</a>
}
```

`handleSignout`是当用户从他的会话退出时调用的 NextAuth 事件。

```
const handleSignout = (e) => {
  e.preventDefault()
  signOut()
}
```

您的`index.tsx`现在应该是这样的:

```
import { useSession, signOut } from 'next-auth/react';

export default function Header () {

const { data: session } = useSession();

  const handleSignout = (e) => {
    e.preventDefault()
    signOut()
  }

  return (
    <div>

    {session && <button onClick={handleSignout}>Sign out</a>}

    {!session && 
    <a href="/register">Sign Up</a>
    <a href="/login>Sign In</a>
    }

    </div>
  )
}
```

**用户注册**:现在在 pages 文件夹中创建一个`register.tsx`文件，并粘贴以下代码块。

```
import type { NextPage } from "next";
import { signIn, getSession } from "next-auth/react";
import Router from "next/router";
import { GetServerSideProps } from "next";

const Page: NextPage = () => {

return (

<form onSubmit={handleSubmit} method="post">

<label>Email</label>
<input type="text" placeholder="Email" name="name" required/>

<label>Password:</label>
<input type="password" placeholder="Password" name="password" 
required/>

<button type="submit">Submit</button>

</form>

);

};

const handleSubmit = async (e) => {

 e.preventDefault();

 const email = e.target.email.value;
 const password = e.target.password.value;

if (
 !email.trim().length ||
 !email.includes("@") ||
 !password.trim().length
 )
 return alert("Invalid details");

 const res = await fetch("/api/auth/register", {
 method: "POST",
 headers: {"Content-Type": "application/json"},
 body: JSON.stringify({email: email,password: password}),
 });

 const data = await res.json();

 if (res.status != 201) return alert(data.message);

 const status = await signIn("credentials", {
 email: email,
 password: password,
 });

 Router.push("/");

 };

 export const getServerSideProps: GetServerSideProps = async (ctx) => {

 const session = await getSession(ctx);

 if (session)
 return { redirect: { destination: "/", permanent: false } };

 return { props: {} };

 };

 export default Page;
```

在`register.tsx`文件中，我们创建了一个带有电子邮件&密码输入字段的常规表单。在表单提交时，我们调用一个`handleSubmit`函数来验证电子邮件和密码输入。一旦通过验证，这些值就会被发送到 Next.js api，`/api/auth/register`。

当从 register api 收到成功的响应时，我们利用 NextAuth 钩子`signIn`让用户成功登录并创建一个会话。下一步，我们还将使用 Next.js 的`Router`方法将用户重定向到主页。

在`register.tsx`页面的`getServerSideProps`中，我们使用`getSession`来确保页面只能在访客模式下访问。

**注册 API** :为了让`/api/auth/register` api 工作，我们还需要创建一个`register.ts`文件。

您的`register.ts`文件需要放在您的`/pages/api/auth/`文件夹中。

```
import type { NextApiRequest, NextApiResponse } from “next”;
import { hash } from “bcryptjs”;
import { findOne, insertOne } from “./models/user”;

const handler = async (req: NextApiRequest, res: NextApiResponse) => {

if (req.method === "POST") {

 const { email, password } = req.body;

if (!email || !email.includes("@") || !password || !username)
return res.status(422).json({ message: "Invalid Data" });

const userExists = await findOne(email);

if (userExists)
 return res.status(422).json({ message: "user already exists" });

const obj = {
 email: email,
 password: await hash(password, 12)
};

const insert = await insertOne(obj);

res.status(201).json({ message: "User created", …insert });

} 
else {
 res.status(500).json({ message: "Route not valid" });
}
};
export default handler;
```

它从数据库模型文件`./model/user`中导入`findOne`和`insertOne`方法，首先验证用户是否已经存在，如果不存在，则插入新的用户记录。我们还使用 Node.js 的`bycrypt`模块进行密码散列。您可以让上面的代码与您选择的任何流行的关系或非关系数据库一起工作。

**用户登录**:登录时，只需在`handleSubmit`功能中稍作代码调整，即可复制大部分`register.tsx`文件。查看`login.tsx`页面下面的`handleSubmit`功能。

```
const handleSubmit = async (e) => {

 e.preventDefault();

 const email = e.target.email.value;
 const password = e.target.password.value;

if (
 !email.trim().length ||
 !email.includes("@") ||
 !password.trim().length
 )
 return alert("Invalid details");

 const status = await signIn("credentials", {
    email: email,
    password: password,
 });

 if (status.error) return alert(status.error);

  Router.push("/");

 };
```

我们现在完全依靠`signIn` hook 来为现有用户完成这项工作。`signIn`使用 NextAuth 的`CredentialsProvider`调用签到函数，传递我们需要认证的邮箱和密码。简而言之，对于用于登录的`handleSubmit`函数，与它在`register.tsx`中的用法相比，我们简单地移除了 Next.js api end。

**credentials provider:**`CredentialsProvider`是 NextAuth.js 提供的众多提供者之一，处理使用任意凭证的登录，例如用户名和密码、域、双因素身份验证或硬件设备(例如 YubiKey U2F / FIDO)。

最后一步，您需要在`/pages/api/auth/`文件夹中创建一个`[...nextauth].js`文件。

```
import NextAuth from “next-auth”;
import { findOne } from “./database/user”;
import { compare } from “bcryptjs”;
import CredentialsProvider from “next-auth/providers/credentials”;

export default NextAuth({
 providers: [

CredentialsProvider({
 authorize: async (credentials: object, req) => {

const user = await findOne(credentials.email);

if (!user)
 throw new Error(“No user found with the email “ + credentials.email);

 const verifyPassword = await compare(
 credentials.password,
 user.password
 );

if (!verifyPassword)
 throw new Error(“Invalid password”);

return Promise.resolve({
 id: user.id,
 email: credentials.email
 });
 },
 }),
 ],
 callbacks: {
 session: async ({ session, token }) => {
 session.user = token.user; 
 return session;
 },
 },
secret: process.env.SECRET,
});
```

`authorize`处理程序接受通过 HTTP POST 提交的凭证作为输入，或者在我们的例子中，由注册和登录流中使用的`signIn`钩子传递。每当检查一个会话时，就会调用`session`回调。作为回报，我们将收到一个`session.user`对象来表明凭证是有效的。`session.user`将包含使用`findOne`方法从数据库获取的用户的唯一 id 和电子邮件地址。

```
return Promise.resolve({
 id: user.id,
 email: credentials.email
 });
```

**结论:**希望这篇教程对你有帮助！请随意浏览 NextAuth 的提供者列表，了解可用于身份验证的各种服务。

*更多内容请看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*