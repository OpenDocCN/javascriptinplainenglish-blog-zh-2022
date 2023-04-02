# 更多商店来保存数据

> 原文：<https://javascript.plainenglish.io/more-stores-to-save-the-data-in-putout-plugins-2c014c5dda3?source=collection_archive---------29----------------------->

## 了解这个代码转换器的插件。

![](img/7fbb2ab3831898b4edb68d5ec327921c.png)

*I hear the song of the nightingale.
The sun is warm, the wind is mild,
willows are green along the shore -
Here no Ox can hide!
What artist can draw that massive head,
those majestic horns?
© Zen Ten Bulls*

嗨伙计们！
今天我们来谈谈万能代码转换器的插件。

# 💪重用-复制-初始化现在支持`MemberExpression`

🐊 [**输出**](https://github.com/coderaiser/putout) 规则 [**重用-复制-初始化**](https://github.com/coderaiser/putout/tree/v24.5.0/packages/plugin-reuse-duplicate-init#putoutplugin-reuse-duplicate-init-) 现在支持 [**成员表达式**](https://babeljs.io/docs/en/babel-types#memberexpression) 。还有这样的代码:

```
const {operator} = require('putout');
const {replaceWith} = require('putout').operator
```

它将很容易转化为:

```
const {operator} = require('putout');
const {replaceWith} = operator
```

# 商店街的新人

当您需要存储遍历数据以备将来处理，并希望正确处理时:使用`[Stores](https://github.com/coderaiser/putout/blob/master/packages/engine-runner/README.md#stores)`，这是首选的保存方式🐊`Putout`数据。`traverse` init 函数只调用一次，其他任何处理变量的方式都很可能导致 bug。

有两种类型的商店:

*   `✅[store](https://github.com/coderaiser/putout/tree/v23.2.0/packages/engine-runner#store)` -向对象存储简单的值；
*   `✅[listStore](https://github.com/coderaiser/putout/tree/v23.2.0/packages/engine-runner#liststore)`存储数组项；

现在我们有了`[upstore](https://github.com/coderaiser/putout/tree/v23.2.0/packages/engine-runner#upstore)`，它能够根据您提供的名称更新您输入的信息。

下面就来分别说一下。

# `listStore`

使用`listStore`保存列表之类的东西。让我们假设您有这样的代码:

```
debugger;
const hello = '';
debugger;
const world = '';
```

我们来处理一下！

```
module.exports.traverse = ({listStore}) => ({
    'debugger'(path) {
        listStore('x');
    },

    Program: {
        exit() {
            console.log(listStore());
            // returns
            ['x', 'x'];
            // for code
            'debugger; debugger';
        },
    },
});
```

# `store`

当你需要`key-value`时，使用`store`:

```
module.exports.traverse = ({push, store}) => ({
    'debugger'(path) {
        store('hello', 'world');
        push(path);
    },

    Program: {
        exit() {
            store();
            // returns
            ['world'];

            store.entries();
            // returns
            [['hello', 'world']];

            store('hello');
            // returns
            'world';
        },
    },
});
```

# `upstore`

当您需要更新已经保存的值时，使用`upstore`:

```
module.exports.traverse = ({push, store}) => ({
    TSTypeAliasDeclaration(path) {
        if (path.parentPath.isExportNamedDeclaration())
            return;

        store(path.node.id.name, {
            path,
        });
    },

    ObjectProperty(path) {
        const {value} = path.node;
        const {name} = value;

        store(name, {
            used: true,
        });
    },

    Program: {
        exit() {
            for (const {path, used} of store()) {
                if (used)
                    continue;

                push(path);
            }
        },
    },
});
```

# `not-rule-`前缀为`Rules`

当您使用特定于您的项目的[规则](https://github.com/coderaiser/putout#rulesdir)，并且您不想发布它们(但是想将它们保存在存储库中)——使用`--rulesdir`:

```
putout --rulesdir rules
```

类似于它在🐊`Putout`目录中的知识库`[/rules](https://github.com/coderaiser/putout/tree/master/rules)`🎉

当你需要重用某些东西时，你可以创建一个带有前缀 **not-rule-** 的文件或目录，例如 **not-rule-common** ，它将在处理选项阶段被忽略。

那都是乡亲们！祝你愉快，🥳！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***