# 让我们给 JavaScript 添加 Swift Guards

> 原文：<https://javascript.plainenglish.io/lets-add-swift-guards-to-javascript-42767b99a3ba?source=collection_archive---------12----------------------->

![](img/2c871de92f9ac00c699545d12a1da725.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> “如果所有其他人都接受了党强加的谎言——如果所有的记录都讲述了同样的故事——那么这个谎言就会成为历史，成为真理。共产党的口号是“谁控制了过去，谁就控制了未来；谁控制了现在，谁就控制了过去””，——《1984》，乔治·奥威尔

[上次](https://medium.com/@coderaiser/how-to-extend-javascript-parser-with-a-new-keyword-36d79be21ef8)我们给 JavaScript 添加了`fn`关键字，让我们试试更复杂的:【Swift 的卫士。

下面是一个简短的例子:

```
fn hello() {
    guard (text !== "world") else {
        return "";
    }

    return "Hello " + text;
}
```

这是 JavaScript 版本:

```
function hello() {
    if (!(text !== 'world')) {
        return '';
    }

    return 'Hello ' + text;
}
```

如你所见，`guard`做的是反转一个表达式，所以它不像`IfStatement` + `UnaryExpression`。听起来很有趣不是吗:)？我们走吧！

# 添加保护关键字

首先，我们需要添加一个新的关键字类型:

```
function newSpeak(Parser) {
    Parser.acorn.keywordTypes.guard = new TokenType('guard', {
        keyword: 'guard',
    });
}
```

然后，我们应该在关键字列表中添加一个新的关键字(如前一篇文章所述)。

```
function newSpeak(Parser) {   
    Parser.acorn.keywordTypes.guard = new TokenType('guard', {
        keyword: 'guard',
    });

    return class extends Parser {
        parse() {
            this.keywords = addKeyword('guard', keywords);
            return super.parse();
        }
    }}
```

然后我们需要`parseStatement`:

```
class extends Parser {
        parseStatement(context, topLevel, exports) {
            if (this.type === Parser.acorn.keywordTypes.guard) {
                return this.parseGuard(context, topLevel, exports);
            }

            return super.parseStatement(context, topLevel, exports);
        }

        parseGuard() {
            this.next();

            const node = this.startNode();

            this.expect(tt.parenL);

            node.test = {
                type: 'UnaryExpression',
                operator: '!',
                prefix: true,
                argument: this.parseExpression(),
            };
            this.expect(tt.parenR);
            this.expect(tt._else);

            node.consequent = this.parseStatement();
            node.alternate = null;

            return this.finishNode(node, 'IfStatement');
        }
    };
```

在`parseGuard`中实际做的是用`UnaryExpression` not 创建一个新的`IfStatement`，它具有从代码中解析的原始表达式。

它不应该有任何`else`，所以`alternate`是`null`，`consequent`是传递给`guard`的原始语句。

整个代码将是这样的:

```
const {TokenType, tokTypes: tt} = require(['acorn'](https://github.com/acornjs/acorn));const {print} = require(['putout'](https://github.com/coderaiser/putout));
const {Parser} = require('acorn');function newSpeak(Parser) {
    Parser.acorn.keywordTypes.fn = new TokenType('fn', {
        keyword: 'fn',
    });

    Parser.acorn.keywordTypes.guard = new TokenType('guard', {
        keyword: 'guard',
    });

    return class extends Parser {
        parse() {
            const keywords = addKeyword('fn', this.keywords);
            this.keywords = addKeyword('guard', keywords);

            return super.parse();
        }
        parseStatement(context, topLevel, exports) {
            if (this.type === Parser.acorn.keywordTypes.fn) {
                this.type = Parser.acorn.keywordTypes.function;
            }

            if (this.type === Parser.acorn.keywordTypes.guard) {
                return this.parseGuard(context, topLevel, exports);
            }

            return super.parseStatement(context, topLevel, exports);
        }

        parseGuard() {
            this.next();

            const node = this.startNode();

            this.expect(tt.parenL);

            node.test = {
                type: 'UnaryExpression',
                operator: '!',
                prefix: true,
                argument: this.parseExpression(),
            };
            this.expect(tt.parenR);
            this.expect(tt._else);

            node.consequent = this.parseStatement();
            node.alternate = null;

            return this.finishNode(node, 'IfStatement');
        }
    };
};

function addKeyword(keyword, keywords) {
    const str = keywords
        .toString()
        .replace(')$', `|${keyword})$`)
        .slice(1, -1);

    return RegExp(str);
}

const {stringify} = JSON;

const MyParser = Parser.extend(
    newSpeak,
);

const ast = MyParser.parse(`
    fn hello() {
        guard (text !== "world") else {
            return ""
        }

        return "Hello " + text
    }
`);

console.log(stringify(ast, null, 4));

console.log(print(ast));
// returns
`
function hello() {
    if (!(text !== 'world')) {
        return '';
    }

    return 'Hello ' + text;
}
`
```

今天就到这里吧！如果你有关于新代码构造的想法，只需在[**Goldstein**](https://github.com/coderaiser/goldstein)**资源库中创建一个问题，它包含一个新的 **JavaScript** 编译器，没有限制😏。**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***