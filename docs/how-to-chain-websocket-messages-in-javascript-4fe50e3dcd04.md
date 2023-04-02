# 如何在 JavaScript 中链接 WebSocket 消息

> 原文：<https://javascript.plainenglish.io/how-to-chain-websocket-messages-in-javascript-4fe50e3dcd04?source=collection_archive---------9----------------------->

## 使用异步和等待是如此简单

![](img/74356f514b79ffe5f13941002a315941.png)

如果您曾经需要使用 JavaScript 向 WebSocket 服务器发送消息，可能在某个时候您想知道是否有一种方法可以链接 WebSocket 服务器调用。

当然有！

在之前的文章[通过命令行下棋](https://medium.com/geekculture/playing-chess-through-the-command-line-e52ed69daf9f)中，我们学习了如何在浏览器控制台的命令行中运行一系列象棋命令，而不考虑它的异步方面。

```
const ws = new WebSocket('ws://127.0.0.1:8080');
ws.send('/start analysis');
ws.send('/piece e2');
```

如果从同步调用的角度来看，这段代码看起来还不错，但实际上并非如此——它是一个涉及象棋服务器的异步代码的例子。之所以看起来有效，是因为第一个命令和第二个命令之间经过了足够长的时间。在编写 JavaScript 代码时，无法假设哪个命令将首先运行。在同步范例中，chess 命令肯定会一次运行一个，一个接一个地运行，然而，在异步范例中，您明确地确保它们这样做。

在 ECMAScript 2017 中， [async/await 语法](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)来拯救代码，使代码在链接异步函数时更具可读性。我们想要控制消息发送到 WebSocket 服务器的顺序，所以它们都被包装到在`[src/actions/serverActions.js](https://github.com/chesslablab/redux-chess/blob/master/src/actions/serverActions.js)`文件中定义的异步 await 函数中。

```
...export const wsMssgUndoMove = async (state) => {
  return await state.server.ws.send(`/undomove`);
};export const wsMssgResign = async (state, action) => {
  return await state.server.ws.send(`/resign ${action}`);
};export const wsMssgRematch = async (state, action) => {
  return await state.server.ws.send(`/rematch ${action}`);
};export const wsMssgRestart = async (state) => {
  return await state.server.ws.send(`/restart ${state.mode.playfriend.hash}`);
};export const wsMssgStartLoadpgn = async (state, movetext) => {
  return await state.server.ws.send(`/start loadpgn "${movetext}"`);
};export const wsMssgResponse = async (state) => {
  return await state.server.ws.send(`/response`);
};
```

现在，当以某种方式组合时，可以很容易地将 WebSocket 消息链接起来，如下例所示。

```
...wsMssgQuit(state).then(() => {
  wsMssgStartPlayfriend(state, color, time, increment);
});
```

上面的代码片段先退出当前游戏；然后，在浏览器相应地接收到来自服务器的响应之后，新的游戏以`[PLAYFRIEND](https://github.com/chesslablab/redux-chess/blob/master/src/constants/modeNames.js)`模式开始。

非常感谢您的阅读！我希望今天的帖子对你有所帮助。

[](https://medium.com/geekculture/playing-chess-through-the-command-line-e52ed69daf9f) [## 通过命令行下棋

### 仅仅通过输入命令来下棋是很有趣的

medium.com](https://medium.com/geekculture/playing-chess-through-the-command-line-e52ed69daf9f) [](/understanding-how-a-complex-react-redux-app-works-934b3600ad13) [## 复杂的 React Redux 应用程序如何工作

### 一步一步理解，不要弄得太乱。

javascript.plainenglish.io](/understanding-how-a-complex-react-redux-app-works-934b3600ad13) [](/check-out-the-redux-chess-demo-acbea003d710) [## 查看 Redux 国际象棋演示

### 请坐下来，享受一杯你最喜欢的啤酒

javascript.plainenglish.io](/check-out-the-redux-chess-demo-acbea003d710) 

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*