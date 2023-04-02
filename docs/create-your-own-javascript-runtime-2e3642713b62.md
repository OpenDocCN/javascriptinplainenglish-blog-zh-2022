# 创建自己的 JavaScript 运行时

> 原文：<https://javascript.plainenglish.io/create-your-own-javascript-runtime-2e3642713b62?source=collection_archive---------3----------------------->

## 关于如何使用 V8 JavaScript 引擎创建自己的基本 JavaScript 运行时的教程。

![](img/10c7f9568dbc623f17dd182d77535e4b.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无论是浏览器运行时还是像 Node.js 这样的服务器端运行时，我们都使用某种运行时来运行 JavaScript 代码。今天，我们将使用 V8 JavaScript 引擎创建一个我们自己的基本 JavaScript 运行时。

# **什么是 JavaScript 运行时？**

JavaScript 运行时只是一个环境，它通过提供有用的 API 来扩展 JavaScript 引擎，并允许程序与其容器外部的世界进行交互。这不同于引擎，引擎只是简单地解析代码并在一个包含的环境中执行它。

正如我前面提到的，V8 是一个 JavaScript 引擎，这意味着它处理 JavaScript 源代码的解析和执行。Node.js 和 Chrome(都由 v8 支持)提供了对象和 API，允许代码与文件系统(通过`node:fs`)或窗口对象(在 Chrome 中)进行交互。

# 设置

在本教程中，我们将使用 Rust 来创建我们的运行时。我们将使用由 Deno 团队维护的 [V8 绑定](https://crates.io/crates/v8)。因为创建一个运行时是一个复杂的过程，今天我们将从简单的开始，通过实现一个 REPL(读取-评估-打印循环)。一次运行 JavaScript 一行输入的提示符。

 [## V8 — Crates.io: Rust 包注册表

### 生锈的 V8 装订

crates.io](https://crates.io/crates/v8) 

首先，用`cargo init`创建一个新项目。然后，向`Cargo.toml`文件添加一些依赖项。`v8`包包含对 V8 JavaScript 引擎的绑定，`clap`是一个用于处理命令行参数的流行库。

```
[dependencies]
v8 = "0.48.0"
clap = "3.2.16"
```

# **管理命令输入**

当使用我们的运行时，我们可能希望为它提供一些命令行参数，比如运行什么文件，或者修改行为的任何标志。打开`src/main.rs`，在`main`函数中，用定义子命令和输入参数的代码替换`println`调用。如果没有提供子命令，我们将做与 Node.js 相同的事情，将用户扔进 REPL。我们还将创建一个子命令“run ”,我们将在后面的教程中实现它。`run`，一旦实现，将允许用户运行一个 JavaScript 文件(与我们定义的任何其他参数)。

```
use clap::{Command, arg};fn main() {
  let cmd = clap::Command::new("myruntime")
  .bin_name("myruntime")
  .subcommand_required(false)
  .subcommand(
    Command::new("run")
      .about("Run a file")
      .arg(arg!(<FILE> "The file to run"))
      .arg_required_else_help(true),
  );
}
```

现在，我们将根据这个模式匹配参数，并相应地处理响应。

```
 ... let matches = cmd.get_matches();
  match matches.subcommand() {
    Some(("run", _matches)) => unimplemented!(),
    _ => {
      unimplemented!("Implement this in the next step")
    },
  };
```

我们现在只有两种可能。第一个是`run`，我们今天不会实现，第二个是没有子命令，这将打开我们的 REPL。在实现 REPL 之前，我们首先需要创建 JavaScript 环境。

# **初始化 V8 &创建引擎实例**

在我们对 V8 做任何事情之前，我们必须首先初始化它。然后，我们需要制造一个隔离区。一个包罗万象的对象，表示 JavaScript 引擎的单个实例。

在文件顶部添加一条`use`语句，以包含`v8`板条箱。接下来，让我们回到 REPL 的未实现代码部分，初始化 V8，并创建一个隔离区，将其封装在一个`HandleScope`中。

```
use v8;...
    _ => {
      let platform = v8::new_default_platform(0, false).make_shared();
      v8::V8::initialize_platform(platform);
      v8::V8::initialize(); let isolate = &mut v8::Isolate::new(v8::CreateParams::default());
      let handle_scope = &mut v8::HandleScope::new(isolate);
    },
```

# **创造 REPL**

为了帮助管理我们的代码，我们将在一个`struct`中创建我们的运行时。当创建一个新实例时，我们将创建一个`Context`。`Context`允许一组全局和内置对象存在于一个“上下文”中。说到全局对象，我们将创建一个名为 global 的对象模板，以便在后面的教程中使用。这个对象允许我们绑定自己的全局函数，但是现在，我们只是用它来创建上下文。

```
struct Runtime<'s, 'i> {
  context_scope: v8::ContextScope<'i, v8::HandleScope<'s>>,
}impl<'s, 'i> Runtime<'s, 'i>
where
  's: 'i,
{
  pub fn new(
    isolate_scope: &'i mut v8::HandleScope<'s, ()>,
  ) -> Self {
    let global = v8::ObjectTemplate::new(isolate_scope); let context = v8::Context::new_from_template(isolate_scope, global);
    let context_scope = v8::ContextScope::new(isolate_scope, context);Runtime { context_scope }
  }
}
```

接下来，让我们在`Runtime`中定义一个方法，负责处理 REPL，并且只处理 REPL。使用一个`loop`，我们将在每次迭代中获取输入，如果成功的话就运行它。我们还需要从文件顶部的`std::io`导入一些东西。

```
use std::io::{self, Write};...pub fn repl(&mut self) {
    println!("My Runtime REPL (V8 {})", v8::V8::get_version()); loop {
      print!("> ");
      io::stdout().flush().unwrap();

      let mut buf = String::new();
      match io::stdin().read_line(&mut buf) {
        Ok(n) => {
          if n == 0 {
            println!();
            return;
          }

          // prints the input (you'll replace this in the next step)
          println!("input: {}", &buf);
        }
        Err(error) => println!("error: {}", error),
      }
    }
  }
```

现在让我们返回`main`中的 REPL 命令，创建一个运行时实例，并初始化 REPL。

```
 ... let mut runtime = Runtime::new(handle_scope);
      runtime.repl();
```

# 运行代码

我们的`run`方法将接受代码和文件名(对于 REPL，我们将简单地使用`(shell)`)进行错误处理。我们创建一个新的作用域来处理脚本的执行，并将其包装在一个`TryCatch`作用域中，以获得更好的错误处理(我们将在未来的教程中实现)。接下来，我们初始化脚本并创建一个 origin 对象，它定义了脚本的来源(在一个文件中)。

```
 fn run(
    &mut self,
    script: &str,
    filename: &str,
  ) -> Option<String> {
    let scope = &mut v8::HandleScope::new(&mut self.context_scope);
    let mut scope = v8::TryCatch::new(scope); let filename = v8::String::new(&mut scope, filename).unwrap();
    let undefined = v8::undefined(&mut scope);
    let script = v8::String::new(&mut scope, script).unwrap();
    let origin = v8::ScriptOrigin::new(
      &mut scope,
      filename.into(),
      0,
      0,
      false,
      0,
      undefined.into(),
      false,
      false,
      false,
    );}
```

现在，继续`run`，我们编译脚本，捕捉任何错误，并打印错误发生。然后，我们运行脚本，再次捕捉任何错误，并记录是否发生了错误。然后，我们返回脚本的结果(如果发生错误，则返回`None`)。

```
 ... let script = if let Some(script) = v8::Script::compile(&mut scope, script, Some(&origin)) {
      script
    } else {
      assert!(scope.has_caught());
      eprintln!("An error occurred when compiling the JavaScript!");
      return None;
    }; if let Some(result) = script.run(&mut scope) {
      return Some(result.to_string(&mut scope).unwrap().to_rust_string_lossy(&mut scope));
    } else {
      assert!(scope.has_caught());
      eprintln!("An error occurred when running the JavaScript!");
      return None;
    }
```

在我们的`repl`方法中返回这两行。

```
 // prints the input (you'll replace this in the next step)
          println!("input: {}", &buf);
```

我们现在可以实现我们的`run`方法了。用一个`if`语句替换`println`来运行脚本，并打印结果。

```
 if let Some(result) = self.run(&buf, "(shell)") {
            println!("{}", result);
          }
```

# **结论**

恭喜你！您已经迈出了使用 V8 引擎创建自己的 JavaScript 运行时的第一步。本教程的完整代码可以在 [GitHub](https://github.com/TheOtterlord/v8-runtime-tutorial/tree/main/01-creating-a-repl) 上找到，我在下面列出了一些使本教程成为可能的精彩资源。

下一次，我们将使用一些已经准备好的代码(比如`TryCatch`范围)来处理错误。

# **资源**

*   [教程源代码](https://github.com/TheOtterlord/v8-runtime-tutorial/tree/main/01-creating-a-repl)
*   [有用的概念— Node.js GitHub 库](https://github.com/nodejs/node/tree/main/src#helpful-concepts)
*   [V8 防锈绑定文档— Docs.rs](https://docs.rs/v8/latest/v8/index.html)
*   [V8 生锈绑定示例—生锈的 V8 GitHub](https://github.com/denoland/rusty_v8/tree/main/examples)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***