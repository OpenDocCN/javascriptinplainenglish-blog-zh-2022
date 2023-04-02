# 如何用类型脚本构建插件系统

> 原文：<https://javascript.plainenglish.io/how-to-build-a-plugin-system-with-typescript-e7efb9f7e1ab?source=collection_archive---------5----------------------->

![](img/d307b1a22476e56357d67d1ba68dd20c.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您正在构建一个极简主义应用程序，您可以允许人们扩展您的应用程序的方法之一是使用插件。插件通常是小的代码包，使用公开的 API 或库来修改和添加应用程序的特性。通常在运行时加载，它们使应用程序更加灵活。

在本教程中，我们将创建一个简单的类型安全插件系统，可以在任何应用程序中使用。

# **开始**

让我们从创建一个新的 Node.js 项目开始。在本教程中，我将使用`npm`作为我的包管理器，但是请随意使用`yarn`。

1.`mkdir my-plugin-manager`

2.`cd my-plugin-manager`

3.`npm init -y`

4.`npm i -D typescript`

# **定义插件**

我们将使用一个由每个插件实现的[抽象类](https://www.typescriptlang.org/docs/handbook/2/classes.html#abstract-classes-and-members)来定义我们的插件。我们需要提供名称和版本，以及加载和卸载插件的开始和停止方法。

我们可以使用一个接口来实现这个，然后为每个插件实现这个接口，但是我们也想提供一种访问其他 API 的方法。否则，插件在它自己的范围之外不能做很多事情。因此，我们将使插件成为一个抽象类，并需要一个泛型类型的输入“应用程序”(“t”)。这可能是你的应用程序的主类，一个包含对多个有用的 API 的访问的对象，或者你的插件想要访问的任何其他方法或值。

```
export abstract class PluginTemplate<T> {
  abstract name: string;
  abstract version: string; app: T; constructor(app: T) {
    this.app = app;
  } abstract start(): Promise<void>;
  abstract stop():  Promise<void>;
}
```

实现类时，名称、版本、开始和停止方法都必须由插件提供。一个使用例如`App`类的插件的例子是…

```
export default class MyPlugin extends PluginTemplate<App> {
  name = "my-plugin";
  version = "1.0.0"; async start() {
    console.log("My plugin started");
  } async stop() {
    console.log("My plugin stopped");
  }
}
```

# **管理多个插件**

为了帮助加载和卸载插件，我们可以创建一个插件管理器类。这个类将被实例化一次，通常由应用程序的主类实例化。

首先，让我们用泛型类型`T`创建一个新的类。像`PluginTemplate`类中的泛型一样，这代表了要暴露给插件的对象。活动插件将存储在`private _plugins`字段中，由类自己的方法(如 unload 方法)使用。

```
export class PluginManager<T> {
  private _plugins: PluginTemplate<T>[] = []; async load(plugin: PluginTemplate<T>) {
    this._plugins.push(plugin);
    await plugin.start();
  } async unload(pluginName: string) {
    let plugin = this._plugins.find(plugin => plugin.name === pluginName);
    if (!plugin) return false;
    await plugin.stop();
    return true;
  }
}
```

为了使从文件系统加载插件更容易，我们可以创建一个从目录中读取所有文件的方法，并将该目录中的任何文件作为插件加载。

```
 async loadDir(app: T, dir: string) {
    let files = await fs.readdir(dir);
    for (let file of files) {
      // The current working is used to resolve the path to the plugins directory.
      let Plugin = await import(path.join(process.cwd(), dir, file));
      let plugin = new Plugin(app);
      await this.load(plugin as PluginTemplate<T>);
    }
  }
```

为了帮助卸载插件，例如当一个应用程序停止时，我们将创建一个方法从`_plugins`字段中卸载每个函数。

```
 async unloadAll() {
    for (let plugin of this._plugins) {
      await plugin.stop();
    }
  }
```

# **添加应用**

我们可以将任何我们希望的泛型作为`T`传递，但最有可能的类型是应用程序的主类。该类也可能包含插件管理器实例。为了一举两得，让我们用一个`pluginManager`模拟一个`App`类。我们可以从当前工作目录(你启动应用的目录)中的`./plugins`目录中加载插件。

```
export class App {
  pluginManager = new PluginManager<App>(); constructor() {} start() {
    this.pluginManager.loadDir(this, './plugins')
  } stop() {
    this.pluginManager.unloadAll();
  }
}
```

# **便捷的打字快捷键**

我们可以定义一个简化用法的快捷方式类型，而不是每次创建插件时都传递类型作为泛型。

```
export type AppPlugin = PluginTemplate<App>;// old
export default class MyPlugin extends PluginTemplate<App> {...}
// new
export default class MyPlugin extends AppPlugin {...}
```

# **结论**

为插件系统添加类型安全使得开发过程更加快速和安全。但是不要忘记暴露正确的类型，比如你的 app/plugin api 和任何快捷方式类型。如果你准备好迎接挑战，尝试将它与你现有的应用程序集成。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***和****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***