# 如何使用 jQuery 将图像转换成 Base64 字符串

> 原文：<https://javascript.plainenglish.io/how-to-convert-image-into-base64-string-using-jquery-a511efd1b10?source=collection_archive---------5----------------------->

![](img/a8057ee6f39e13392c45970e8da9ef6a.png)

Photo by [Goran Ivos](https://unsplash.com/@goran_ivos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个例子中，我们将看到如何使用 jQuery 将图像转换成 base64 字符串。当需要对二进制数据进行编码时，通常使用 Base64 编码方案，这些二进制数据需要通过为处理 ASCII 而设计的介质进行存储和传输。

我们将使用 jquery 或 javascript 将图像转换为 base64 字符串。为了将 base64 转换为字符串，我们使用 FileReader()函数并从文件中获取结果。

让我们看看，将图像转换为 base64 字符串 jQuery。

## **例 1**

FileReader 用于读取 Blob 或文件的内容。

```
<!DOCTYPE html>
<html>
  <head>
    <title>How To Convert Image Into Base64 String Using jQuery</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  </head>
  <body>
  <form>
    <input type="file" name="img" id="image">
    <button type="submit">Submit</button>
    <a id="base64Img" href=""></a>
  </form>
  </body>
  <script type="text/javascript">
    $('#image').on('change', function() { var img = element.files[0];

      var reader = new FileReader();

      reader.onloadend = function() {

        $("#base64Img").attr("href",reader.result);

        $("#base64Img").text(reader.result);
      } reader.readAsDataURL(img);
    });
  </script>
</html>
```

## **例二**

`createElement()`方法创建一个具有指定名称的元素节点，如按钮、画布等。

```
function base64Img(img) {

   const canvas = document.createElement('canvas');
   const ctx = canvas.getContext('2d');   
   canvas.width = img.width;
   canvas.height = img.height;   
   ctx.drawImage(img, 0, 0);
   return canvas.toDataURL('image/jpeg');
}const img = document.querySelector('#image');
img.addEventListener('load', function (event) {
   const dataUrl = base64Img(event.currentTarget);
   alert(dataUrl);
});
```

**您可能还喜欢:**

*   **阅读也:** [**Laravel 签名板示例**](https://websolutionstuff.com/post/laravel-signature-pad-example)
*   **阅读另:** [**Dropzone 图片上传教程在 Laravel 6/7**](https://websolutionstuff.com/post/dropzone-image-upload-tutorial-in-laravel-6-7)
*   **阅读另:** [**如何在 Jquery 中获取选中的复选框列表值**](https://websolutionstuff.com/post/how-to-get-selected-checkbox-list-value-in-jquery)
*   **阅读也:** [**如何在 Laravel**](https://websolutionstuff.com/post/how-to-integrate-razorpay-payment-gateway-in-laravel) 中集成 Razorpay 支付网关

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*