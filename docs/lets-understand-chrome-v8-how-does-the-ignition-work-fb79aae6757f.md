# 让我们来了解一下 Chrome V8:点火是如何工作的

> 原文：<https://javascript.plainenglish.io/lets-understand-chrome-v8-how-does-the-ignition-work-fb79aae6757f?source=collection_archive---------4----------------------->

## 第 30 章:加载 JSfunction 并执行字节码

![](img/2229cb027639f57877eb360bf75cd927.png)

*欢迎阅读* [*其他章节让我们来了解一下 Chrome V8*](https://medium.com/@huidou)

在本文中，我将讨论 ignition，并让您了解它是如何工作的，它如何加载 JSfunction，以及它在执行之前会做什么。

# **1。调用 JSfunction**

对于 V8 解释器，所有这些都从加载 JSfunction(V8 术语是 invoke)开始，因为它有一个字节码数组。下面是调用函数。

在调用 JSfunction 之前，V8 将它包装到 invoke-params 中，但不会添加其他新内容，所以我们不关心它，但要记住哪个成员是其中的 JSfcuntion。我把重要的内容列在下面。

**(1)** 第 1–13 行，SetupForCall()就是我提到的包装函数。

**(2)** 第 17 行，代码是 Builtin::kJSEntry 函数地址。

**(3)** 第 24 行，stub_entry 是 Builtin::kJSEntry 的第一条指令。

**(4)** 第 27 行，func 是一个将执行的 JSfunction。

**(5)** 第 31 行，存根 _ 分录。调用开始进入点火状态以执行您的 JavaScript。**注意:**现在您的 JavaScript 还没有被调用，因为 Ignition 正在创建调用堆栈，然后会跳转到您的代码中。

# **2。Builtin::kJSEntry**

在讲 Builtin::kJSEntry 之前，我想强调一下 JSFunction 的一些成员，这个函数经常用在 Ignition 中。

**(1) SharedFunction** ，是 JSFunction 的成员，我们需要知道的关键是 SharedFunction 有点火将执行的字节码数组。

**(2)** **代码**，是 Builtins::kinterpetertentrytrampoline。

**(3)** **上下文**，是当前运行时对应的上下文。

让我们进入内置::kJSEntry。

在上面的代码中，第 2 行调用 Generate_JSEntryVariant()，它的第三个参数是最终调用我们的字节码的 trampoline。

第 15 行，arg_reg_1 表示 isolate-> isolate _ data()-> isolate_root()，我之所以强调它，是因为 isolate _ root()包含所有必要的东西，如 builtins 和 heap，所有这些对运行时都很有用。

第 17–22 行，将顶部的帧推入堆栈，就像我们在 X86 中所做的一样。

第 24–26 行，将当前上下文加载到 ScratchRegister 中。

第 46–48 行，exectue JSEntryTrampoline。

# **3。内置::kJSEntryTrampoline**

在上面的代码中，第 7–28 行将参数推入堆栈，其中参数函数是来自 JavaScript 的字节码。第 40–49 行，注释描述了堆栈框架布局。第 53 行，获取 builtin 地址，即 Builtin::kCall_ReceiverIsAny。

# **4。builtin::kCall _ receive risany**

在上面的代码中，第 13 行， *rdi* 是正在执行的 JSFunction， *rcx* 是它的 map。一般情况下，CmpObjectType 为 true，跳转到第 14 行，最后调用 kCallFunction _ ReceiverIsAny。

# **5。builtin::kCallFunction _ receive risany**

在上面的代码中，第 7–19 行将参数压入堆栈， *rax* 寄存器对于确保 JavaScript 参数始终匹配至关重要，因为如果参数丢失，V8 会填充一个 Null，或者 V8 会丢弃多余的参数。第 10-14 行， *rdi* 是 js 函数， *rdx* 是它的 shared 函数。最后执行第 20 行。

# **6。InvokeFunctionCode**

在上面的代码中，第 23 行调用的是 *rcx* ，而 *rcx* 只是 Builtins::kinterpetereentrytrampoline，这是我们的 JavaScript 的序言。换句话说，如果您想知道 JavaScript 是如何执行的，从这里开始调试是最简单的方法。

以下描述来自 v8.dev。

当在运行时调用该函数时，会进入 InterpreterEntryTrampoline 存根。这个存根设置了一个适当的堆栈框架，然后分派给解释器的字节码处理程序，处理函数的第一个字节码，以便在解释器中开始执行函数。基于字节码，每个字节码处理程序的末尾通过全局解释器表的索引直接分派到下一个处理程序。”

好了，这部分就到此为止了。下次再见，保重！

如果你有任何问题，请联系我。**微信** : qq9123013 **邮箱**:[v8blink@outlook.com](mailto:v8blink@outlook.com)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***