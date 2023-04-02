# 如何使用 Next.js 和 Firebase 创建 Todo 应用程序

> 原文：<https://javascript.plainenglish.io/how-to-create-todo-app-with-nextjs-firebase-383dcee65076?source=collection_archive---------0----------------------->

![](img/14d1cbcf3d559f7f7c9c2d50098120e4.png)

Todo app with Nextjs and firebase

## 嘿 devs，欢迎来到本教程；我们会用 React，Next.js + Firebase 搭建一个实时的 Todo App。

这是这篇文章的视频解释👇

**这个项目的完整代码可以在这个** [**资源库**](https://github.com/anjalbinayak/medium-nextjs-firebase-todo) 中找到👇

[](https://github.com/anjalbinayak/medium-nextjs-firebase-todo) [## TodoApp-Nextjs-Firebase

### 点击此处查看该待办事项应用的代码。别忘了使用黑暗模式😉

github.com](https://github.com/anjalbinayak/medium-nextjs-firebase-todo) 

在我们开始编写代码之前，我想告诉你，我希望你对 React 和 Next.js 有基本的了解。

如果您不熟悉 React 和 Next，请浏览这些文档:

1.  [React 文档](https://reactjs.org/)
2.  [Next.js 文档](https://nextjs.org/)

## 这是我们要建造的东西

完成本教程后，我们的应用程序将如下所示:

![](img/360d8d4ba63682ab9d9b6bd5cce8dd89.png)

## 这是我们这个项目的技术堆栈

1.  **React** :
    我们会为构建这个应用的 UI 做出反应。
2.  **Next.js** :
    Next.js 是一个基于 React 的框架，用于构建现代 web 应用。它提供了一些好处，比如服务器端渲染和许多 SEO 好处
3.  我们将使用 Firebase 作为这个应用程序的后端。我们将数据存储在*Firestore*中。它为创建实时应用程序提供了许多功能。
    (我们的待办事宜应用将是实时的)
4.  **ChakraUI**:
    ChakraUI 是一个造型框架。它已经设计好了可以在应用程序中使用的组件。它提供了响应能力、黑暗模式、吸引眼球的配色方案等等。

## 为什么我们在项目中使用 Firebase？

Firebase 提供了如此多的功能，让人难以忽视。

它仅用 4-5 行代码就提供了社交认证。

我们将使用 Firebase 在我们的项目中实现 **Google Auth** 。

Firebase 的一些功能包括:

1.  证明
2.  实时服务器
3.  低安全风险
4.  社会认证
5.  最小设置

# 目录

1.  创建 Firebase 项目
2.  创建与 Firestore 互动的方法
3.  创建 React 组件(添加 Todo、Auth、TodoList)
4.  npm 运行开发😁

让我们从创建下一个应用程序开始。

键入以下命令安装下一个应用程序:

```
npx create-next-app next-firebase-todo
```

**安装所需的依赖项**

1.  Chakra UI

```
npm i @chakra-ui/react @emotion/react @emotion/styled framer-motion
```

2.重火力点

```
npm i firebase
```

## 创建 Firebase 项目

转到[火焰基座控制台](https://console.firebase.google.com/)。

![](img/847ce7bc93be647fe4a987f1401684d3.png)

点击创建一个项目。

![](img/a875bd1ec2db40e341aa85047aabbf5b.png)

命名您的项目并勾选方框，然后点击**继续。**

![](img/8cb6409f578928cf9a12365c40bf39cd.png)

我们不需要谷歌项目分析。因此，松开按钮并点击**继续。**

创建项目后，您将看到项目仪表板。

![](img/f00ad64f91ea831d61ac5bb82d29d890.png)

如图标所示，第一个按钮用于 IOS 项目，第二个用于 Android 项目，第三个用于 Web 应用程序。

我们正在创建一个 web 应用程序，因此我们将单击它。

![](img/38eb1f709ee2bc660abd33eac0bdfdc2.png)

命名您的 web 应用程序，然后单击**注册应用程序。**

![](img/707829da213d82265896c0816838df15.png)

复制这段代码并点击**继续到控制台。**

**注意**:把这段代码保存在某个地方。我们将在我们的项目中用到它。

![](img/f5351565967df82920bad9ef2f881be7.png)

在左侧，点击**构建。**

![](img/e333b5011f2935f4e360e21b4597efa0.png)

我们只需要这个列表中 firebase 的两个特性。

**认证** —用于添加 Google 登录。
**FireStore 数据库** —用于存储用户的待办事项。

现在，让我们先启用这两个特性。

点击认证。

![](img/49b53a54739911c1beb50ba9e4de577e.png)

单击开始。

![](img/a72ce5c2bc6b6862462f8cfecd68b106.png)

我们将只使用谷歌认证，所以点击谷歌。

![](img/2ec523425e403b629646080dde720edc.png)

启用 Google 身份验证，选择项目支持电子邮件，然后单击保存。

我们已经在 Firebase 项目中成功启用了 Google Auth。

现在让我们启用 Firestore 数据库。

转到左侧边栏，单击构建，然后单击 Firestore 数据库。

![](img/363993dcaa8290ab23cf2a7e3c28fc94.png)

点击创建数据库。

![](img/7022a76e59621fd10a8e6aed8d9d30f9.png)

在测试模式下选择*启动*并点击**下一步，**并点击**启用。**

现在我们已经启用了项目所需的**认证**和 **Firestore 数据库**。

现在让我们开始编码。

让我们转到`pages/_app.js`并复制粘贴以下内容:

```
import { ChakraProvider } from "@chakra-ui/react";function MyApp({ Component, pageProps }) {return (<ChakraProvider><Component {...pageProps} /></ChakraProvider>);}export default MyApp;
```

我们只是把`<Component {…pageProps} />`包在了`<ChakraProvider>`里面。

Chakra UI 的官方文档是这样建议的。

现在，我们将在我们的 web 应用程序中设置 Firebase。

让我们在项目根目录下创建一个名为`firebase`的新文件夹。

在`firebase`目录下创建一个名为`index.js`的文件。

现在粘贴我之前告诉你复制的代码(firebase config):

```
import { initializeApp } from "firebase/app";import { getAuth } from "firebase/auth";import { getFirestore } from "firebase/firestore";**// replace this firebase conFigvariable with your own**const firebaseConfig = {apiKey: "AIzaSyClH1YdssQHAA0peMtQ_wj2A4Crnc4fEgU",authDomain: "medium-firebase-next-todo.firebaseapp.com",projectId: "medium-firebase-next-todo",storageBucket: "medium-firebase-next-todo.appspot.com",messagingSenderId: "989711683222",appId: "1:989711683222:web:bc878dca5a5d251177fcb7",};const app = initializeApp(firebaseConfig);const auth = getAuth(app);const db = getFirestore(app);export { auth, db };
```

我们在这里做的是粘贴 firebase 配置。我们另外创建了两个变量`auth` 和`db` ，它们分别是 **firebase 认证模块**和 **firestore 模块**。

让我们为我们的项目添加一个新的依赖项，它是`react-icons`。

```
npm install react-icons --save
```

React 图标库允许你添加漂亮的图标到你的项目中。

现在让我们创建创建 todos 并与之交互的方法。

## 与 Firestore 互动的方法

在项目的根目录下创建一个名为`api`的目录。

然后创建一个文件`todo.js`。

并将下面的代码复制粘贴到`todo.js`中。

```
import { db } from "../firebase";import {collection,addDoc,updateDoc,doc,deleteDoc,} from "firebase/firestore";const addTodo = async ({ userId, title, description, status }) => {try {await addDoc(collection(db, "todo"), {user: userId,title: title,description: description,status: status,createdAt: new Date().getTime(),});} catch (err) {}};const toggleTodoStatus = async ({ docId, status }) => {try {const todoRef = doc(db, "todo", docId);await updateDoc(todoRef, {status,});} catch (err) {console.log(err);}};const deleteTodo = async (docId) => {try {const todoRef = doc(db, "todo", docId);await deleteDoc(todoRef);} catch (err) {console.log(err);}};export { addTodo, toggleTodoStatus, deleteTodo };
```

现在让我们创建一个身份验证挂钩来检查用户的身份验证状态。

创建一个名为`hooks`的目录

并在`hooks`目录下创建一个文件`useAuth.js`

并将下面的代码复制粘贴到`useAuth.js`中。

```
import { useEffect, useState } from "react";import { auth } from "../firebase";const useAuth = () => {const [user, setUser] = useState(null);const [isLoggedIn, setIsLoggedIn] = useState(false);useEffect(() => {auth.onAuthStateChanged((user) => {setIsLoggedIn(user && user.uid ? true : false);setUser(user);});});return { user, isLoggedIn };};export default useAuth;
```

我们所做的是创建一个 useAuth 钩子来返回当前的`user` 和`isLoggedIn` 布尔值。

每次 auth 状态改变时，调用`onAuthStateChanged` 中的方法。

这个功能是 firebase 本身提供的。

现在让我们创建用户界面。

## 创建 React 组件

在 web 应用程序的根目录下创建`components` 目录。

我们将在应用程序中创建 3 个组件:

1.  AddTodo —用于添加新的 Todo
2.  Auth —用于添加登录/注销按钮
3.  待办事项—用于正确查看所有现有的待办事项

让我们从 AddTodo 开始。

在`components`目录中创建 `AddTodo.jsx`。

将以下代码复制并粘贴到 AddTodo.jsx 中:

```
import React from "react";import {Box,Input,Button,Textarea,Stack,Select,useToast,} from "@chakra-ui/react";import useAuth from "../hooks/useAuth";import { addTodo } from "../api/todo";const AddTodo = () => {const [title, setTitle] = React.useState("");const [description, setDescription] = React.useState("");const [status, setStatus] = React.useState("pending");const [isLoading, setIsLoading] = React.useState(false);const toast = useToast();const { isLoggedIn, user } = useAuth();const handleTodoCreate = async () => {if (!isLoggedIn) {toast({title: "You must be logged in to create a todo",status: "error",duration: 9000,isClosable: true,});return;}setIsLoading(true);const todo = {title,description,status,userId: user.uid,};await addTodo(todo);setIsLoading(false);setTitle("");setDescription("");setStatus("pending");toast({ title: "Todo created successfully", status: "success" });};return (<Box w="40%" margin={"0 auto"} display="block" mt={5}><Stack direction="column"><Inputplaceholder="Title"value={title}onChange={(e) => setTitle(e.target.value)}/><Textareaplaceholder="Description"value={description}onChange={(e) => setDescription(e.target.value)}/><Select value={status} onChange={(e) => setStatus(e.target.value)}><optionvalue={"pending"}style={{ color: "yellow", fontWeight: "bold" }}>Pending ⌛</option><optionvalue={"completed"}style={{ color: "green", fontWeight: "bold" }}>Completed ✅</option></Select><ButtononClick={() => handleTodoCreate()}disabled={title.length < 1 || description.length < 1 || isLoading}variantColor="teal"variant="solid">Add</Button></Stack></Box>);};export default AddTodo;
```

现在，在`component`目录中创建`Auth.jsx`，并将以下代码复制并粘贴到其中:

```
import React from "react";import { Box, Button, Link, Text, useColorMode } from "@chakra-ui/react";import { signInWithPopup, GoogleAuthProvider } from "firebase/auth";import { FaGoogle, FaMoon, FaSun } from "react-icons/fa";import { auth } from "../firebase";import useAuth from "../hooks/useAuth";const Auth = () => {const { toggleColorMode, colorMode } = useColorMode();const { isLoggedIn, user } = useAuth();const handleAuth = async () => {const provider = new GoogleAuthProvider();signInWithPopup(auth, provider).then((result) => {// This gives you a Google Access Token. You can use it to access the Google API.const credential = GoogleAuthProvider.credentialFromResult(result);const token = credential.accessToken;// The signed-in user info.const user = result.user;// ...}).catch((error) => {// Handle Errors here.const errorCode = error.code;const errorMessage = error.message;// The email of the user's account used.const email = error.customData.email;// The AuthCredential type that was used.const credential = GoogleAuthProvider.credentialFromError(error);// ...});};return (<Box position={"fixed"} top="5%" right="5%"><Button onClick={() => toggleColorMode()}>{colorMode == "dark" ? <FaSun /> : <FaMoon />}</Button>{" "}{isLoggedIn && (<><Text color="green.500">{user.email}</Text><Link color="red.500" onClick={() => auth.signOut()}>Logout</Link></>)}{!isLoggedIn && (<Button leftIcon={<FaGoogle />} onClick={() => handleAuth()}>Login with Google</Button>)}</Box>);};export default Auth;
```

现在让我们在`components` 目录中创建`TodoList.jsx` 组件。

并将以下代码复制并粘贴到其中:

```
import {Badge,Box,Heading,SimpleGrid,Text,useToast,} from "@chakra-ui/react";import React, { useEffect } from "react";import useAuth from "../hooks/useAuth";import { collection, onSnapshot, query, where } from "firebase/firestore";import { db } from "../firebase";import { FaToggleOff, FaToggleOn, FaTrash } from "react-icons/fa";import { deleteTodo, toggleTodoStatus } from "../api/todo";const TodoList = () => {const [todos, setTodos] = React.useState([]);const {  user } = useAuth();const toast = useToast();const refreshData = () => {if (!user) {setTodos([]);return;}const q = query(collection(db, "todo"), where("user", "==", user.uid));onSnapshot(q, (querySnapchot) => {let ar = [];querySnapchot.docs.forEach((doc) => {ar.push({ id: doc.id, ...doc.data() });});setTodos(ar);});};useEffect(() => {refreshData();}, [user]);const handleTodoDelete = async (id) => {if (confirm("Are you sure you wanna delete this todo?")) {deleteTodo(id);toast({ title: "Todo deleted successfully", status: "success" });}};const handleToggle = async (id, status) => {const newStatus = status == "completed" ? "pending" : "completed";await toggleTodoStatus({ docId: id, status: newStatus });toast({title: `Todo marked ${newStatus}`,status: newStatus == "completed" ? "success" : "warning",});};return (<Box mt={5}><SimpleGrid columns={{ base: 1, md: 3 }} spacing={8}>{todos &&todos.map((todo) => (<Boxp={3}boxShadow="2xl"shadow={"dark-lg"}transition="0.2s"_hover={{ boxShadow: "sm" }}><Heading as="h3" fontSize={"xl"}>{todo.title}{" "}<Badgecolor="red.500"bg="inherit"transition={"0.2s"}_hover={{bg: "inherit",transform: "scale(1.2)",}}float="right"size="xs"onClick={() => handleTodoDelete(todo.id)}><FaTrash /></Badge><Badgecolor={todo.status == "pending" ? "gray.500" : "green.500"}bg="inherit"transition={"0.2s"}_hover={{bg: "inherit",transform: "scale(1.2)",}}float="right"size="xs"onClick={() => handleToggle(todo.id, todo.status)}>{todo.status == "pending" ? <FaToggleOff /> : <FaToggleOn />}</Badge><Badgefloat="right"opacity="0.8"bg={todo.status == "pending" ? "yellow.500" : "green.500"}>{todo.status}</Badge></Heading><Text>{todo.description}</Text></Box>))}</SimpleGrid></Box>);};export default TodoList;
```

我们已经创建了所有需要的组件，现在我们要把它们放到我们的应用程序中。

转到`pages/index.js`删除所有内容并粘贴以下内容:

```
import { Container } from "@chakra-ui/react";import AddTodo from "../components/AddTodo";import Auth from "../components/Auth";import TodoList from "../components/TodoList";export default function Home() {return (<Container maxW="7xl"><Auth /><AddTodo /><TodoList /></Container>);}
```

我们结束了。

## npm 运行开发

我们已经完成了应用程序的编码。

转到您的终端并键入:

```
npm run dev
```

并在浏览器中转至`localhost:3000`。

您将看到类似这样的内容:

![](img/67fed0922d3c5c6e55fc0c0c84ecfd63.png)

现在你可以**登录谷歌**并开始添加待办事项。

获得完整的代码[在这里](https://github.com/anjalbinayak/medium-nextjs-firebase-todo)。

这里看解说视频[。](https://www.youtube.com/watch?v=wkKzKpTY4w4)

在推特上关注我。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***