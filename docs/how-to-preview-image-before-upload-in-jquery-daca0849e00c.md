# 如何在 jQuery 中预览上传前的图片

> 原文：<https://javascript.plainenglish.io/how-to-preview-image-before-upload-in-jquery-daca0849e00c?source=collection_archive---------10----------------------->

在本文中，我们将了解如何在将图像上传到 jQuery 之前预览它。可以使用`FileReader`对象的 JavaScript `readAsDataURL()`方法来读取指定文件的内容。readAsDataURL()方法用于读取指定的`[Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)`或`[File](https://developer.mozilla.org/en-US/docs/Web/API/File)`的内容。当读操作完成后，`[readyState](https://developer.mozilla.org/en-US/docs/Web/API/FileReader/readyState)`变为`DONE`，触发`[loadend](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/loadend_event)`。

所以，让我们在用 JavaScript 上传之前先看看预览图片，用 jQuery 预览图片。

**举例:**

如何使用此方法读取图像文件，并在上传到服务器之前在浏览器中预览它。

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>How To Preview Image Before Upload In jQuery - Websolutionstuff</title>
<script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
    function previewFile(input){
        var file = $("input[type=file]").get(0).files[0];

        if(file){
            var reader = new FileReader();

            reader.onload = function(){
                $("#previewImg").attr("src", reader.result);
            }

            reader.readAsDataURL(file);
        }
    }
</script>
</head> 
<body>
    <form action="image_upload.php" method="post">
        <p>
            <input type="file" name="image_file" onchange="previewFile(this);" required>
        </p>
        <img id="previewImg" src="/images/example.png" alt="Placeholder">
        <p>
            <input type="submit" value="Submit">
        </p>
    </form>
</body>
</html>
```

**你可能也会喜欢:**

*   **阅读也:** [**jQuery 前后示例**](https://websolutionstuff.com/post/jquery-after-and-before-example)
*   **阅读另:** [**如何使用 JQuery**](https://websolutionstuff.com/post/how-to-remove-spaces-using-jquery) 删除空格
*   **阅读也:** [**如何在 jQuery**](https://websolutionstuff.com/post/how-to-get-children-element-in-jquery) 中获取子元素】
*   **另请阅读:** [**如何使用 jQuery**](https://websolutionstuff.com/post/how-to-convert-image-into-base64-string-using-jquery) 将图像转换为 Base64 字符串

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***