# 如何构建一个简单的浏览器内全文搜索引擎

> 原文：<https://javascript.plainenglish.io/building-a-simple-in-browser-search-engine-d87c86ac3261?source=collection_archive---------0----------------------->

## 因为有时候官僚主义会碍事。

![](img/dc132ee44dd456c6cd6e7f7451d51779.png)

Photo by [Ruchindra Gunasekara](https://unsplash.com/@ruchindra?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/warehouse?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

几年前，我被要求为一个气隙 [conda 存储库](https://anaconda.org/conda-forge)创建一个文件存储库。这个想法是，出于安全原因，我们将在非常昂贵的安全环境中有一个允许的库的列表，并且只有那些库。这是一个[相当简单的设置](https://anaconda.org/conda-forge/conda-mirror)，只需要大量的存储空间和一个简单的静态 web 服务器来传递它们。

简单的过滤镜像使我们能够更快地响应用户需求，并快速地在安全环境中添加或删除库。这意味着安全团队更愿意让包进入环境，因为他们知道删除它们只需几个小时，而不是几个月或几年。

*   他们太激动了，我们开始使用模式来允许包。
*   我们很快从几十个包变成了几千个。
*   用户开发了一个新问题，可以打电话询问:

> 有哪些图书馆？

可用库的列表少于官方库，但明显大于一个人可以合理地期望通读，它也分布在几个文件夹中。总而言之，这是很难保持跟踪。

用户需要的是一个搜索引擎，像 Anaconda.org，但仅限于我们的组织可用的软件包。

> **旁白**
> 
> 就在这个时候，在我们的故事中，我发现自己因公离开了家。在魁北克加蒂诺的一家酒吧参加了一个关于利用技术系统影响社会变革的晚间讲座，喝了几杯酒后，我发现自己在加拿大隆冬时节独自走回了酒店。为了不被冻死，并找出我的酒店在哪里，我开始思考搜索问题。当我回到酒店时，我无法入睡，所以开始实施解决方案。
> 
> 啊…程序员的生活。

不幸的是，官僚主义阻碍了发展。获得静态 HTTP 服务器是一个谈判的壮举。为了通过 HTTP 共享文件系统，我已经明确声明只打开静态渲染。这让我们跳过了几个月的安全评估，没有服务器端处理意味着网络没有安全风险。

为了适应对搜索引擎的需求和服务器端处理的缺乏，我在浏览器内部构建了一个简单的搜索引擎。

# 履行

事实上，我以前已经这样做过几次了。在我的职业生涯中，有几个例子表明，获得工具和计算机对于一个简单的数据处理引擎来说是很大的障碍。这里的关键是，您可以将一个简单的`html`文件放到您的服务位置，然后它可以查找存储在服务器上的数据。

为了读者的利益，我有一个简单的例子工作，索引中情局世界概况，然后提供内容的搜索。搜索结果提供了一个到中情局网站实际页面的链接。

[](https://gitlab.com/jefferey-cave/simple-search-demo/-/tree/main) [## 文件主 Jeff Cave /简单搜索演示

### GitLab.com

gitlab.com](https://gitlab.com/jefferey-cave/simple-search-demo/-/tree/main) 

## 自动索引和加载

关键是要确保某种形式的自动索引开启。服务器必须通告要处理的可用数据集，以便客户端发现它们需要处理。有几种方法可以实现这一点，最简单的是在服务器上打开服务。

在类似的系统中，我还使用了“bash”或“PowerShell”脚本来列出所有存在的数据集:没有关于它们的信息，只是说它们存在

```
ls --format=single-column ./data/* > **index.txt**
```

然后，可以将该文件的位置传递给脚本，作为收集所有信息的起点

```
const basePath = window.location;
const datasets = `${basePath}/**index.txt**`;
```

一旦我们有了要聚合的数据列表，我们就可以开始下载、解析和存储的过程。

假设我们使用了 PouchDB，我们可以立即开始将文本加载到本地数据库中。

```
const db = new PouchDB('searcher');
async function LoadDB(){
    let recs = await fetch('./index.txt');
    recs = await rec.text();
    recs = rec.split('\n');
    for(let loc of recs){
      let content = await fetch(loc);
      let nRec = {
          _id: loc,
          text: nRec
      }; let oRec = await db.get(loc);
      if(RecordsDiffer(nRec,oRec)){
          db.put(nRec);
      }
    }
}
```

全文现在存储在数据库中，供用户将来使用。建议定期对此进行扫描，以查看是否发生了任何变化。( [loader.js](https://gitlab.com/jefferey-cave/simple-search-demo/-/blob/main/scripts/loader.js#L80-109) )

## 净化文本

在数据库开发和搜索中，索引可以被认为是快速参考。在手动搜索的时代，卡片目录提供了按主题排序的字母搜索，这允许快速查找。你可以在一个盒子里浏览一个更小的目录，而不必浏览整栋楼里的每本书。

少即是多，小即是快。

出于讨论的目的，有几个我们想要搜索的文档是很有用的:

> 事实 21:问题复杂性每增加 25 %,软件解决方案的复杂性就会增加 100%。这不是一个试图改变的条件(尽管降低复杂性总是一件值得做的事情)；事情就是这样。
> 
> 事实 22:80%的软件工作是脑力劳动。相当一部分是创造性的。很少是文书工作。
> 
> —罗伯特·l·格拉斯,《软件工程的事实和谬误》

因此，我们讨论的示例将围绕着对 Glass 事实的文本进行索引，以便快速查找。这可能有助于安装在办公室的麦克风上，然后根据正在讨论的内容显示适当的“事实”。

每个事实可以放在一个单独的记录中，供我们以后索引时使用。这将允许我们把每个事实当作一个不同的实体。

```
./data/fact-01.txt
./data/fact-02.txt
./data/fact-03.txt
```

诸如此类的文本的一个问题是，许多文本实际上毫无意义，或者至少意义不大。应该执行某种级别的转换来删除不必要的信息。

```
function sanitize(text){
    text = text.toLowerCase();
    text = text.replace(/[^a-z]/g,'.');
    text = text.split('.');
    text = text.filter(d=>{return d.length > 3;});
    return text;
}let sanitized = sanitize(facts[21]);
```

作为索引事实 21 的一部分，我们删除了

*   情况
*   非文本
*   短词(三字，又名:[停词](https://en.wikipedia.org/wiki/Stop_word))

从而产生净化的单词列表。( [crepo.js](https://gitlab.com/jefferey-cave/simple-search-demo/-/blob/main/scripts/crepo.js#L31-42) )

```
[ 'every', 'percent', 'increase', 'problem', 'complexity', 'there', 'percent', 'increase', 'complexity', 'software', 'solution', 'that', 'condition', 'change', 'even', 'though', 'reducing', 'complexity', 'always', 'desirable', 'thing', 'that', 'just' ] 
```

通过注意重复的单词，可以进一步减少列表。字数统计是衡量搜索项价值的一种有用方式

```
function WordCount(list){
    let count = {};
    for(let word of list){
        count[word] = count[word] || 0;
        count[word]++;
    }
    return count;
}
let count = WordCount(sanitized);
```

## 创建索引

出于搜索的目的，我选择对每个单词进行匹配。这样做是为了简单，因为它允许无序搜索单词。

我希望用户能够使用的搜索类型示例:

*   ` complexity `:一个过于复杂的单词(可能是`complex`)
*   ` ompl `:部分匹配的单词
*   `软件 olut `:多个单词
*   `解决方案软件`:单词顺序不对

这些例子代表了我们需要处理的几种不同的情况。最有趣的是“部分匹配”场景。

为了创建一个索引，我们需要一个基于查找值的列表

```
| key      | score | document |
| -------- | ----- | -------- | 
| database |   100 |  <url>   | 
| atabase  |    99 |  <url>   | 
| tabase   |    98 |  <url>   | 
| abase    |    97 |  <url>   | 
| base     |    96 |  <url>   |
| ase      |    95 |  <url>   | 
| databas  |    99 |   ...    | 
| databa   |    98 |   ...    |
| ...      |   ... |   ...    |
```

当你搜索“数据搜索”时，它会找到

```
document 1 
data 97 
document 1 
search 100
```

总计 197 分，然后按得分最高的文档排序(代码: [search.js](https://gitlab.com/jefferey-cave/simple-search-demo/-/blob/main/scripts/search.js#L97-116) )

# 临时演员

## 词汇化

作为另一层，我们可以考虑引理。词汇化指的是一个词所代表的最基本的词。例如，`intellectual`可以认为与`intellect`相同。这将有助于减少以后可能出现的印刷差异，例如，一个记得`that is`的人应该找到`that's`，想起来了，`is`是一个短词。

[https://github . com/mich mech/lemma tization-lists/blob/master/lemma tization-en . txt](https://github.com/michmech/lemmatization-lists/blob/master/lemmatization-en.txt)

```
every 25 **percent** increase problem **complex** there 100 **percent** increase **complex** software solution **that** condition change even though **reduce complex** always **desire** thing **that** just
```

这是一个更简单的文本版本，它将减少信息熵的数量(也就是在记忆时大脑中可能出错的事情)。

这篇文章已经整理好了，可以做索引了。

# 结论

第二天早上，写完解决方案后，我对自己有了一个完整的解决方案感到非常满意，我可以通过电子邮件将它发送给我的主要客户(整个组织中的一些数据科学经理)。我非常高兴，把它展示给了一位同事，他帮我优化了索引。

![](img/f1495b73d469dcae333edb794a5259bd.png)

[Found this Intersting? Leave a Tip…. it helps](https://www.buymeacoffee.com/jeffereycave)

多年后，这仍然是该组织跟踪可用的康达软件包的方式。

公平地说，我能够在一夜之间完成这件事的唯一原因是我已经实现了很多次。我已经使用浏览器端索引实现了用于回归测试、员工工作分配、个人博客搜索和古腾堡项目搜索引擎的仪表板。它甚至成为我教授的一门 JavaScript 入门课的基础。

这是我喜欢 JavaScript 的原因之一:它总是可用于数据处理，[无论你在那个时刻碰巧有什么疯狂的想法](https://ai.plainenglish.io/fun-with-markov-network-brains-8041c35ca883)。

自从最初写这篇文章以来，我发现 Lawson 实际上已经为 PouchDB 写了一个[全文搜索。你应该使用他基于](https://github.com/pouchdb-community/pouchdb-quick-search) [lunr 引擎](https://github.com/olivernn/lunr.js)的解决方案。

## 非最佳的

这不是最佳解决方案。

在这种情况下，搜索引擎的每个用户都必须下载并生成自己的索引实例。这要求客户端第一次为他们使用的每个浏览器下载整个数据集(增加网络流量)。

在回归测试仪表板中，测试结果的初始下载和解析花费了大约 3 个小时。缓存意味着如果你每天保持更新，它几乎是即时的，但是第一次加载是很大的。

服务器端处理的一个关键优势是能够获取入站数据，并为所有客户生成一次索引。您可以通过在服务器上生成索引并让客户端下载构建的索引来消除这种差异。这将在用于中央数据的中央处理器和用于单独搜索的分布式处理之间分割处理负载。

这暗示了共享和分布式处理之间有趣的平衡。使用支持 CouchDB 交换协议的数据库( [CouchBase](https://en.wikipedia.org/wiki/Couchbase_Server) 、 [CouchDB](https://en.wikipedia.org/wiki/Apache_CouchDB) 、 [PouchDB](https://pouchdb.com/) 、 [CloudAnt](https://en.wikipedia.org/wiki/Cloudant) )，每个用户都可以在发现新数据时对其进行处理，而且还可以将结果共享回中央池，供下一个人使用。这种数据处理的延迟加载形式在理论上有一些优势(在可信环境中),因为它需要很少的中央处理(昂贵),而是依赖于已经在使用的工作站。同时，它将分担工作负载，以确保没有一台计算机承担全部计算的压力。

最后，如果这个解决方案引起了您的兴趣，您应该看看为 CouchDB 提供的基于 Lucene 的搜索，它包含在所有商业产品中。

请留下评论或提出问题，如果您发现此内容有价值，请记得[点击关注](https://jefferey-cave.medium.com/)。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***