# 使用 AST 的新方式

> 原文：<https://javascript.plainenglish.io/new-ways-of-working-with-ast-bd9c697bd8cf?source=collection_archive---------18----------------------->

## 这是您在对象上迭代搜索带有键的属性所需要的。

![](img/881b9acdd319ad06ee58f897cab881a9.png)

Too many steps have been taken
returning to the root and the source.
Better to have been blind and deaf
from the beginning!
Dwelling in one’s true abode,
unconcerned with and without -
The river flows tranquilly on
and the flowers are red
© Zen Ten Bulls

嗨伙计们！新的一天，新的文章😄！

# 得到财产

如果您想通过一个键遍历对象搜索属性，那么您需要的就是[**operator . getproperty()**](https://github.com/coderaiser/putout/blob/master/packages/operate/README.md#getpropertypath-path-name-string)**。**

**假设你有一个物体:**

```
{
    "test": "npm test"
}
```

**以下是如何删除名为`test`的属性:**

```
import {operate} from 'putout';
const {getProperty} = operate;const testPath = getProperty(path, 'test');
testPath.remove();
```

# **获取 ExportDefaultDeclaration**

**当你需要得到`export default`[**operator . getexportdefault()**](https://github.com/coderaiser/putout/tree/v24.5.0/packages/operate#getexportdefaultpath)会帮你解决！**

```
import {operate} from 'putout';
const {getExportDefault} = operate;const exportPath = getExportDefault(path);
exportPath.remove();
```

# **它和插件有什么关系？**

**事情是两个新的规则添加到`[@putout/plugin-madrun](https://github.com/coderaiser/putout/tree/master/packages/plugin-madrun#readme)`中，改善使用疯狂舒适的脚本运行程序🏎`[madrun](https://github.com/coderaiser/madrun)`。**

*   **✅ `[convert-cut-env-to-run](https://github.com/coderaiser/putout/tree/master/packages/plugin-madrun#convert-cut-env-to-run)`**
*   **✅ `[convert-run-to-cut-env](https://github.com/coderaiser/putout/tree/master/packages/plugin-madrun#convert-run-to-cut-env)`**

**他们都使用前面描述的方法来转换 **.madrun.js** 代码，如下所示:**

```
export default {
    'test': () => [env, 'npm test'],
    'test:only': () => 'npm test',
    'coverage': async () => [env, await run('test')],
    'coverage:only': async () => [env, await cutEnv('test:only')],
};
```

**收件人:**

```
export default {
    'test': () => [env, 'npm test'],
    'test:only': () => 'npm test',
    'coverage': async () => [env, await cutEnv('test')],
    'coverage:only': async () => [env, await run('test:only')],
};
```

**[**cutEnv()**](https://github.com/coderaiser/madrun#cutenvname-opt-env)**清除任何已经传递给脚本的 Env 变量，因此可以用一个新变量覆盖它，就像用**测试**一样。****

****当 env 没有通过时，不需要它，就像使用 **test:only 一样。******

****今天就到这里吧！好好改造一下🦉！****

*****更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*****