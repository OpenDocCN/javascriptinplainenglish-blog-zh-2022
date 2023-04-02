# 用 100 行 JavaScript 创建一个虚拟助手

> 原文：<https://javascript.plainenglish.io/create-a-complete-ai-assistant-in-100-lines-of-javascript-a80a40a8dfa9?source=collection_archive---------5----------------------->

## 用 Web 语音 API 构建一个简单的人工智能助手

![](img/718446d19d19aa678d4a05aebdeccd8b.png)

[Photo](https://unsplash.com/photos/OYzbqk2y26c) on Unsplash

在本教程中，我们将用几行 JavaScript 在浏览器中创建一个名为**索尼娅**的虚拟助手(就像 Siri 或 Cortana 一样)。这个机器人会听用户的语音命令，并用合成语音做出回应。我们的目标是只使用[网络语音 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API) ，在不牺牲太多功能的情况下，让应用程序尽可能简单。你可以在这里测试 app [。](https://nasosg.github.io/sonya-assistant-medium/)

# 您需要的工具

*   [谷歌浏览器](https://www.google.com/chrome/)
*   您选择的文本编辑器

# 语音到文本功能的 API

我们需要的是一个能够将文本和语音相互转换的 API。希望这个工具存在，它就是 [Web 语音 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API) ，它提供了两个不同的功能领域——语音识别和语音合成(文本到语音)。我们将在这个故事中探索这两个领域。

> Web Speech API 仍处于试验阶段，因此该应用可以在许多浏览器中运行，但不是所有浏览器。截至目前，它可以在最新版本的 Chrome、Edge、Opera 和 Safari 中工作。不幸的是，它在 Firefox 中还不能完全工作*😔*。

# 我们需要实现什么

为了构建这个 web 应用程序，我们需要实现四个组件:

1.  要显示的简单聊天 UI:

*   用户怎么说
*   助理的回答
*   一个触发助手的按钮(比如“嘿 Siri”命令)
*   顶部有一个小的帮助区域，向用户解释一些事情

2.将用户的语音转换成文本(使用[网络语音 API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API)

3.处理文本并根据文本执行操作

4.将文本转换回语音，改变 Sonya 的声音和音调

# 用户界面

第一步是创建一个简单的 UI。我们将创建一个 HTML 文件，其中包含一个`button`来触发助手，并且在顶部有一个小的帮助区域向用户显示一些可用的命令。我们还将创建一个`div`元素来显示用户说了什么和 Sonya 回复了什么，并创建一个`p`元素来显示处理信息。在 JavaScript 中，我们将使用元素对象的唯一 id 属性来检索它们。

**HTML**

```
<html>
<head>
  ...
</head>
<body>
  <div id="content">
    <h1>Sonya</h1>
    <p>Give it a try with 'hi/hello', 'how are you', 'joke', 'coin 
    flip', 'what's your name', 'what time is it', 'bye/stop'</p>
    <p>You can also try 'play despacito' &#128516;. It will play 
    on Youtube. Note: the pop-up may be blocked by your browser</p>
  </div>
  <button id="startBtn">Start listening</button>
  <div id="result"></div>
  <p id="processing"></p>
  <script src="script.js"></script>
</body>
</html>
```

**JavaScript**

```
const startBtn = document.getElementById("startBtn");
const result = document.getElementById("result");
const processing = document.getElementById("processing");
```

# 语音转文本

让我们制作一个组件，它捕获语音命令并将其转换为文本以供进一步处理。我们将使用`SpeechRecognition` 接口。由于该 API 仅在受支持的浏览器中可用，我们将显示一条警告消息，并阻止开始按钮在不受支持的浏览器中显示。

```
const SpeechRecognition = window.SpeechRecognition 
                          || window.webkitSpeechRecognition;
let toggleBtn = null;
if (typeof SpeechRecognition === "undefined") {
  startBtn.remove();
  result.innerHTML = "Your browser doesn't support Speech API. 
                      Please download latest Chrome version.";
}
```

我们将创建一个`SpeechRecognition`的实例，并设置一些[属性](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition)来定制语音识别。我们会将`continuous`和`interimResults`设置为`true`，以实时显示口述文本，即使用户稍有停顿，也会继续录制**。**当`continuous`设置为真时，暂停时间为约 15 秒。

```
const recognition = new SpeechRecognition();
recognition.continuous = true;
recognition.interimResults = true;
```

然后，我们添加一个句柄来处理来自语音 API 的`onresult`事件。每当语音 API 捕获一行代码时，`onresult`中的这段代码就会被调用**。到目前为止，我们捕获的所有行都保存在`event`中，这是一个`SpeechRecognitionEvent`对象。因为我们只需要当前行，所以我们使用`resultIndex`属性来获取已经改变的`[SpeechRecognitionResultList](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognitionResultList)`数组中索引值最低的结果。**

最后，我们得到用户所说内容的文本`transcript`。该文本经过一个`process`函数，该函数被调用来处理用户的问题并找到答案。然后调用`readOutLoud`函数读出答案。`readOutLoud`和`process`功能将在接下来的步骤中执行。用户和助理的语音命令也显示为文本。

```
recognition.onresult = event => {
  const current = event.resultIndex;
  const recognitionResult = event.results[current];
  const recognitionText = recognitionResult[0].transcript;

  if (recognitionResult.isFinal) {
    processing.innerHTML = "processing ...";

    const response = process(recognitionText);
    const p = document.createElement("p");
    p.innerHTML = `<strong>You said:</strong> ${recognitionText} 
                   </br><strong>Sonya said:</strong> ${response}`;
    processing.innerHTML = "";
    result.appendChild(p);

    readOutLoud(response);
  } else {
    processing.innerHTML = `listening: ${recognitionText}`;
  }
};
```

我们还需要将识别作为一个开关来切换。因此，我们只需添加一个 click 事件，并将 UI `button`与`recognition`对象相关联，这样，当单击`button`时，语音识别服务将停止或开始侦听传入的音频，按钮的文本也会发生变化。

> `start()`方法启动语音识别服务，监听输入的音频以识别与当前`[SpeechRecognition](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition)`相关的语法。
> 
> `stop()`方法停止语音识别服务的监听，并尝试使用目前捕获的音频返回结果。

```
let listening = false;

toggleBtn = () => {
  if (listening) {
    recognition.stop();
    startBtn.textContent = "Start listening";
  } else {
    recognition.start();
    startBtn.textContent = "Stop listening";
  }
  listening = !listening;
};

startBtn.addEventListener("click", toggleBtn);
```

# 处理文本并执行操作

在这一步中，我们将构建一个简单的对话逻辑并处理一些基本操作。虽然处理器是 Sonya 的大脑，但它只是一个条件语句的例子，允许 Sonya 响应命令`hi`、`how are you`、`what's your name`、`joke`、`coin flip`、`what time is it`等等。如果 Sonya 不知道答案，她将打开一个新标签，通过谷歌搜索。最后，我们可以通过说`bye`或者`stop`来阻止她听。

要创建一个简单的`process`，只需考虑您希望 Sonya 做什么，并为其添加一个 if case。如果添加更多的条件，Sonya 可以执行更多的任务。你可以进一步扩展这个`process`功能，使用 API 或者 AI 库，让助手变得随心所欲的智能。

```
function process(rawText) {
  let text = rawText.replace(/\s/g, "").replace(/\'/g, "");
  text = text.toLowerCase();
  let response = null;

  if (text.includes("hello") || text.trim() == "hi" || text.includes("hey")) {
    response = getRandomItemFromArray(hello);
  } else if (text.includes("your name")) {
    response = "My name's Sonya.";
  } else if (text.includes("howareyou")||text.includes("whatsup")) {
    response = "I'm fine. How about you?";
  } else if (text.includes("whattimeisit")) {
    response = new Date().toLocaleTimeString();
  } else if (text.includes("joke")) {
    response = getRandomItemFromArray(joke);
  } else if (text.includes("play")) && text.includes("despacito")) {
    response = "Opened it in another tab";
    window.open("https://www.youtube.com/watch?v=kJQP7kiw5Fk",
                "_blank", "noopener");
  } else if (text.includes("flip") && text.includes("coin")) {
    response = Math.random() < 0.5 ? 'heads' : 'tails';
  } else if (text.includes("bye") || text.includes("stop")) {
    response = "Bye!!";
    toggleBtn();
  }

  if (!response) {
    window.open(`http://google.com/search?q=${rawText.replace("search", "")}`,
                "_blank");
    return `I found some information for ${rawText}`;
  }

  return response;
}
```

## *请注意，在新窗口中打开的弹出窗口可能会被浏览器阻止，您需要允许访问。

## 随机答案

对于某些答案，Sonya 会根据一个数组中指定的一组回复给出一个随机答案。例如，如果你说“你好”，Sonya 会从一组问候中随机选择一项作为回应。为了得到这些答案，实现了 getRandomItemFromArray 函数。

```
function getRandomItemFromArray(array) {
  const randomItem = array[Math.floor(Math.random() * array.length)];
  return randomItem;
};
```

# 文本到语音

最后一步，我们使用 Web Speech API 的`speechSynthesis`控制器给我们的助手一个声音。加载声音后，我用更好的声音替换了桑娅的声音。如果你想看到更多的声音，查看文档。我还改变了一点说话的音调和语速。

```
function readOutLoud(message) {
  const speech = new SpeechSynthesisUtterance();

  speech.text = message;
  speech.volume = 1;
  speech.rate = 1;
  speech.pitch = 1.8;
  speech.voice = voices[3];

  window.speechSynthesis.speak(speech);
}
```

# 文本到语音参数

## **声音**

从声音开始，我想把 Sonya 的默认声音改为更女性化的声音，类似于 Siri 或 Cortana 等其他助手。为此，我必须用`getVoices()`方法检索所有可用的声音，并从中选择一个。一开始我把所有的声音都包括进来，让用户自己选择，但后来我觉得没必要这样。

请注意，根据 [Web Speech API 勘误表](https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi-errata.html)(E11 2013–10–17)，语音列表在页面上异步加载，加载时会触发一个`onvoiceschanged`事件。所以我用这个事件来设定声音。

```
// wait on voices to be loaded before fetching list
window.speechSynthesis.onvoiceschanged = function() {
    voices = window.speechSynthesis.getVoices();
};
```

> **voiceschanged** :当 **getVoices()** 返回的 SpeechSynthesisVoiceList 的内容发生变化时触发。**例如**:服务器端合成，其中*列表被异步确定，或者当客户端语音被安装(卸载)时。*

## **音调、速率和音量**

我使用的其他参数是**音调、速率和音量，**这些都是`[SpeechSynthesisUtterance](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesisUtterance)`接口的属性，用于获取和设置说话时的音调、速率或音量。

用于这些参数的值如下:

**螺距= 1.8** :介于 **0** 和 **2** 之间的浮点数，其中 1 为当前默认螺距。**直觉上，音高是关于音频的。高频声音被感知为高音，低频声音被感知为低音。所以我选择了更高的音调，因为女性说话的音调更高，助理的声音也更女性化。**

![](img/3bd932c46437ebfe8b3890840353b73b.png)

**rate = 1** :语速简单来说就是助理说话的速度(每分钟说出的字数)。它是一个浮动值，范围从 0.1 到 10，默认汇率为 **1** 。1 到 1.5 之间的值相当于正常的语速。

**volume = 1** :机器人的声音有多大。它是一个介于 0 和 1 之间的浮点数。

那都是乡亲们！！！我们有一个很酷的助手，只有 100 行代码。代码可以在这个 GitHub [库](https://github.com/NasosG/sonya-assistant-medium)找到，演示可以在[这里](https://nasosg.github.io/sonya-assistant-medium/)查看。

下一步是什么？[在 Medium 上关注我](https://medium.com/@gthanos)成为第一个阅读我的故事的人。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*****