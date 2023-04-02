# 创建自己的 JavaScript 运行时

> 原文：<https://javascript.plainenglish.io/create-your-own-javascript-runtime-5929bf1c894e?source=collection_archive---------10----------------------->

## 第 2 部分:处理由输入 JavaScript 代码抛出的异常。

![](img/e3a2d56a7ba09e5f599266f9f7f4405e.png)

Photo by [Mitchell Luo](https://unsplash.com/@mitchel3uo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了快速回顾我们上次取得的进展，我们初始化了我们的项目，并开始使用 V8 运行 JavaScript。我们创建了一个通过命令行使用的 REPL(读取-评估-打印循环)。今天，我们将通过处理输入 JavaScript 代码抛出的异常来增加我们的 REPL。

# **获取异常**

今天的代码将存在于`src`目录下的一个单独的`errors.rs`文件中。我们将用一个`print_error`函数来处理打印错误。

创建新的`errors.rs`文件。导入 V8 机箱并创建功能`print_error`。如果在传递给函数的范围内存在异常，我们可以继续，否则，我们将打印一个错误，指出不存在异常。

```
use v8;pub fn print_error(mut scope: v8::TryCatch<v8::HandleScope>) {
  if let Some(exception) = scope.exception() {
    ...
  } else {
    eprintln!("Internal error: no exception");
  }
}
```

# **构造错误**

在“if”语句中，我们将获取异常字符串，如果可以的话，还将从异常中获取消息对象。如果我们得不到消息，我们将只打印出简单的异常字符串并返回它。

```
 let exception_string = exception.to_string(&mut scope).unwrap().to_rust_string_lossy(&mut scope); let message = if let Some(message) = scope.message() {
      message
    } else {
      eprintln!("{}", exception_string);
      return;
    };
```

我们的错误消息的第 1 行应该由文件名、行号、抛出异常的令牌列以及异常文本组成。消息对象为我们提供了所需的细节。

```
 let filename = message
    .get_script_resource_name(&mut scope)
    .map_or_else(
      || "(unknown)".into(),
      |s| {
        s.to_string(&mut scope)
          .unwrap()
          .to_rust_string_lossy(&mut scope)
      },
    );
    let line_number = message.get_line_number(&mut scope).unwrap_or_default();
    let start_column = message.get_start_column();
    let end_column = message.get_end_column(); eprintln!("{}:{}:{}: {}", filename, line_number, start_column, exception_string);
```

## **有问题的代码**

接下来，让我们展示抛出异常的代码，并指出该行中的特定标记。正如我们在上面看到的，消息对象为我们提供了一些关于错误的信息。开始和结束列表示令牌的开始和结束位置。

首先，我们打印源代码中的这一行，前面是行号。

```
 let source_line = message
    .get_source_line(&mut scope)
    .map(|s| {
      s.to_string(&mut scope)
        .unwrap()
        .to_rust_string_lossy(&mut scope)
    })
    .unwrap();
    eprintln!("{}: {}", line_number, source_line);
```

然后，我们可以打印一些指向有问题的令牌的 carets，记住添加填充来说明行号。

```
 eprint!("{}", " ".repeat(line_number.to_string().len()+2)); for _ in 0..start_column {
      eprint!(" ");
    } for _ in start_column..end_column {
      eprint!("^");
    } eprintln!();
```

## **堆栈跟踪**

最后，我们将打印堆栈跟踪。这暂时不是很有用，因为所有的错误都会出现在 REPL 的输入行上，但是它仍然是错误消息的重要部分，以后会很有用。我们可以从作用域中获取堆栈跟踪，并将其转换为 V8 字符串。然后打印堆栈跟踪。

```
 let stack_trace = if let Some(stack_trace) = scope.stack_trace() {
      stack_trace
    } else {
      return;
    };
    let stack_trace = unsafe { v8::Local::<v8::String>::cast(stack_trace) };
    let stack_trace = stack_trace
      .to_string(&mut scope)
      .map(|s| s.to_rust_string_lossy(&mut scope)); if let Some(stack_trace) = stack_trace {
      eprintln!("{}", stack_trace);
    }
```

**实现错误打印**

回到`main.rs`文件，找到下面这行代码的两个实例。这是第 1 部分中的临时错误处理代码。

```
eprintln!("An error occured when compiling the JavaScript!");
```

导入`print_error`功能。

```
mod error;
use error::print_error;
```

用函数调用替换 print 语句(在两种情况下),传递作用域。

```
print_error(scope);
```

# **结论**

错误完成后，我们现在可以在 REPL 中识别重要的调试信息。下一次，我们将开始添加文件支持的旅程，在我们的设备上运行文件中的代码。从那里，我们可以扩展到多个文件，并构建运行时的其余部分。如果您需要帮助，请查看下面的完整源代码。

# **资源**

——[教程源代码](https://github.com/TheOtterlord/v8-runtime-tutorial/tree/main/02-handling-errors)

- [有用的概念— Node.js GitHub 库](https://github.com/nodejs/node/tree/main/src#helpful-concepts)

- [V8 锈绑定文档— Docs.rs](https://docs.rs/v8/latest/v8/index.html)

- [V8 生锈绑定示例—生锈的 V8 GitHub](https://github.com/denoland/rusty_v8/tree/main/examples)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***