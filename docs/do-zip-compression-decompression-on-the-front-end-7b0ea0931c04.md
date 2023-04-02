# 对前端进行压缩/解压缩

> 原文：<https://javascript.plainenglish.io/do-zip-compression-decompression-on-the-front-end-7b0ea0931c04?source=collection_archive---------6----------------------->

![](img/aac98bc492cb778c9baf9f5d046df053.png)

不久前，当我研究前端如何解析 excel 表单时，我了解了 jszip 库，它可以在前端直接压缩和解压缩 zip 包。让我们看看如何使用。

## 使用

更不用说安装了，只需要 npm 直接安装 jszip。

## 读取本地文件

要读取本地 zip 文件，我们只需要使用 loadAsync 传入一个文件对象，首先创建一个用于选择文件的文件输入:

```
<input type="file" id="file" name="file" />
```

然后在文件选择之后，我们调用 loadAsync 来读取文件内容:

```
document.querySelector('#file').addEventListener('change', async e => {
    const file = e.target.files[0];
    if (!file) return;
    const zip = await JSZip.loadAsync(file);
});
```

读取完成后，我们可以在返回的 zip 对象的 files 属性中看到压缩包中的所有文件:

```
const zip = {
    files: {
        'Hello.txt': ZipObject,
        'images/': ZipObject,
        'images/smile.gif': ZipObject
    }
};
```

所有的文件和文件夹都会按照路径挂在文件中，zipport 包含文件压缩信息，但是需要注意的是，文件的内容在这个时候仍然是压缩的，所以我们不能把它当作一个普通的文件。要使用这个文件，我们需要在使用它之前进行第二次转换。例如，如果我们想读取上面 Hello.txt 中的内容，我们可以首先将其转换为 blob 对象，然后使用文件阅读器读取它:

```
const txtBlob = await zip.files['Hello.txt'].async('blob');
const fileReader = new FileReader();
file.onload = r => console.log(r.target.result);
reader.readAsText(f);
// log: Hello World\n
```

当然，我们也可以直接使用内置的方法直接转换成字符串:

```
const text = await zip.files['Hello.txt'].async('string');
```

在浏览器端，jszip 支持以下数据类型:

*   `array`
*   `arraybuffer`
*   `base64`
*   `blob`
*   `string`
*   `uint8array`

在节点方面，jszip 还支持 nodebuffer 和 nodestream。

## 读取远程文件

除了读取本地文件，jszip 还支持读取远程 zip 文件:

```
new Promise(function (resolve, reject) {
    JSZipUtils.getBinaryContent('/jszip/test/ref/text.zip', function (err, data) {
        if (err) {
            reject(err);
        } else {
            resolve(data);
        }
    });
})
    .then(JSZip.loadAsync)
    .then(function (zip) {
        return zip.file('Hello.txt').async('string');
    });
```

这里使用 zip.file 方法读取文件，这与上面使用文件读取的方法相同。官方的 JSZipUtils.getBinaryContent 函数可以直接获取远程文件进行读取，而且这个包非常方便。

## 压缩文件

除了上面提到的解压缩文件，jszip 还支持在浏览器端直接压缩文件。首先，我们需要实例化一个 zip 对象:

```
const zip = new JSZip();
zip.file('Hello.txt', 'Hello world\n');
```

通过文件向对象添加文件，然后通过 generateAsync 生成 blob 文件:

```
const blob = await zip.generateAsync({ type: 'blob' });
```

文件生成后，可通过文件的另存为直接下载文件保存:

```
saveAs(blob, 'hello.zip');
```

## 压缩解压缩原理

让我们谈谈压缩和解压缩的原理。由于我对压缩和解压缩算法没有太多的研究，我不打算在这里谈论太多深入的内容。我只是去了解相关内容。这里有一个简单的声明:压缩主要是通过合并连续的字符来完成的。压缩，可以简单地认为，例如，当遇到像 44444999999 这样的字符时，zip 压缩会将其压缩为 4，5，9，6 的形式，从而达到压缩的目的。当然，实际的算法比这个复杂得多。

其实压缩和解压缩都没有 web 盲点，只是算法复杂，但是使用的能力比较基础，只能把文件数据取出来，然后再进行解析，所以前端确实是可以实现的。而且因为前端压缩解压场景太少，这也是为什么很少有人知道前端可以做压缩解压，根本没想过的原因。

## 要使用的场景

在实际业务需求中，前端很少用于压缩或解压缩。个人能想到的实际使用场景如下:

*   在线压缩和解压缩工具网站
*   解析 excel 文件和其他依赖 zip 压缩的文件
*   工具网站上传 zip 包资源解析及使用

## 总结

总的来说，jszip 的 API 设计还是很不错的。很好用，没有那么多麻烦的事情。另外用 Promise 配合 async/await 真的很好。如果以后遇到需要的场景会是一个不错的选择。

[](/how-to-parse-excel-files-with-javascript-114752b6aa1d) [## 如何用 JavaScript 解析 Excel 文件

### 今天就来说说如何用 JS 解析 excel 文件。当然，用库没什么意思，比如…

javascript.plainenglish.io](/how-to-parse-excel-files-with-javascript-114752b6aa1d) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***