# MongoDB 用 Mongoose 和 Node.js 流更新

> 原文：<https://javascript.plainenglish.io/mongodb-updates-with-mongoose-and-node-js-streams-c1839783b07d?source=collection_archive---------5----------------------->

![](img/82d0bd2a7c757698dd3d0699a83860b4.png)

Photo by [Andy Mai](https://unsplash.com/@veroz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 MongoDB 上工作的一个常见任务是通过一些重新计算来更新一个大型集合，这是直接数据库查询无法完成的。

第一种方法是将整个集合读入内存，然后更新文档。如果收集量很大，那么发生 oom 的几率是不可避免的。

Update all documents in memory

第二种方法是使用分页，然后批量更新。
第二种方法的问题是，我们是分批进行的，而且是连续处理的。

首先，我们获得一个批处理，然后应用一些转换，然后保存文档。

Update in batches

**如果我们能同时做这三件事会怎么样？**
我们在处理和保存上一批数据的同时，得到下一批数据。
这就是流处理和管道发挥作用的地方。
1。想象一下从 MongoDB 中以读取流的形式批量读取

2.然后，我们使用转换流将转换应用于文档

3.最后，使用写流将数据保存到数据库

因此，并行运行这 3 个流是通过使用管道实现的。

![](img/b7a3eeae56b28905f0e40eb90f25026e.png)

Photo by [Crystal Kwok](https://unsplash.com/@spacexuan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 支持带有`stream`包的流，Mongoose 支持使用`cursor`方法读取流以进行`find`查询

**1。在模型**上创建样本读取流

```
const readStream = Model.find(filters).cursor({batchSize: 10});
```

**2。创建一个转换流**

```
const transformStream = new Transform({
    objectMode: true,
    transform: (doc, encoding, callback) => {
        // processing logic on each doc
        callback(null, doc);
    },
});
```

**3。创建到数据库的写流**

```
const writeStream = new Writable({
    objectMode: true,
    write: async(doc, encoding, callback) => {
      await doc.save();
      callback();
    }
});
```

*注意:-我们已经将 objectMode 设置为 true，因为默认情况下流使用缓冲区，但是我们使用的是对象*

**连接所有三样东西**

```
readStream.pipe(transformStream).pipe(writeStream);
```

**如何等待所有流完成？**

```
writeStream.on('end', ()=>{
   console.log('Done');
});
```

更好的方法是使用 Nodejs `stream`包中的`pipeline`

```
pipeline(readStream, transformStream, wrriteStream, (err)=>{
    if(err) {
        console.error(err);
        return;
    }
    console.log('Done');
});// Or using pipeline from stream/promisesawait pipeline(readStream, transformStream, wrriteStream);
```

我们用 Mongoose 编写了一个通用的 util 方法来处理这种模式的事情。

**上述实用程序有 5 个参数**

1.  模型类
2.  流式传输时要应用的过滤器
3.  转换函数
4.  写入功能
5.  选项:- `batchSize`默认 10 张单据批量取数据

**样品用途**

```
// Assume we are breaking fullName to firstName and lastNameconst filters = {
    fullName: {
      $exists: true
    }
};const transform = (doc)=> {
  const [firstName, lastName] = doc.fullName.split(' ');
  doc.firstName = firstName;
  doc.lastName = lastName;
  delete doc.fullName;
  return doc;
}const save = doc => doc.save();await updateWithStream(Person, filters, transform, save, {
   batchSize: 20,
});
```

**参考文献:-**

Util 代码:-[https://gist . github . com/Deepak 13245/d 920 Fe 4035 DC 52894 DC 084 c 29 f 7 B4 b 5 e](https://gist.github.com/Deepak13245/d920fe4035dc52894dc084c29f7b4b5e)

Nodejs 流:-[https://nodejs.org/api/stream.html](https://nodejs.org/api/stream.html)

猫鼬光标:-[https://mongoosejs.com/docs/api/querycursor.html](https://mongoosejs.com/docs/api/querycursor.html)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***