# 如何在 React 中上传和预览图像

> 原文：<https://javascript.plainenglish.io/how-to-upload-and-preview-image-in-react-js-ece15b63f5c0?source=collection_archive---------8----------------------->

在本文中，我们将了解如何在 react js 中上传和预览图像。您可以学习如何在 react js 中将图像上传到服务器之前显示图像预览。如果您想在将图像上传到 react 应用程序之前显示图像预览。因此，我们将创建一个简单的 react js 应用程序，它将使用 HTML 文件输入字段以及一些事件来显示图像预览。对于后端，我们将使用一个简单的 PHP 应用程序，该应用程序公开一个惟一的端点，该端点接受包含文件/图像的 POST 请求来上传图像。

所以，我们来看看 react js 图片上传带预览和 react js 图片上传带预览显示。

```
**Step 1: Create React App****Step 2: Install Axios and Bootstrap 4****Step 3: Create Simple Image Upload with Preview Component****Step 4: Add Component in App.js****Step 5: Create PHP File**
```

**第一步:创建 React 应用**

在这一步中，我们将使用以下命令创建一个新的 react 应用程序。

```
npx create-react-app my-react-app
```

要运行 react 应用程序，请在您的终端上执行以下命令。

```
npm start
```

**阅读也:** [**如何在 React JS 中上传文件**](https://websolutionstuff.com/post/how-to-file-upload-in-react-js)

**步骤 2:安装 Axios 和引导程序 4**

在这一步中，我们将把 bootstrap 4 库安装到 react app 中。

```
npm install bootstrap --savenpm install axios --save
```

在`src/App.js`文件中添加 **bootstrap.min.css** 文件:

```
import React from 'react';
import '../node_modules/bootstrap/dist/css/bootstrap.min.css';

function App() {
  return (
    <div>
      <h2>How To Upload And Preview Image In React JS - Websolutionstuff</h2>
    </div>
  );
}

export default App;
```

**步骤 3:使用预览组件创建简单的图像上传**

在这一步，我们将创建**imageuploadpreviewcomponent . js**组件。

```
import React, { Component } from 'react';
import axios from 'axios';

class ImageUploadPreviewComponent extends Component {

    constructor(props) {
        super(props)
        this.state = {
            file: null
        }
        this.uploadSingleFile = this.uploadSingleFile.bind(this)
        this.upload = this.upload.bind(this)
    }

    uploadSingleFile(e) {
        this.setState({
            file: URL.createObjectURL(e.target.files[0])
        })
    }

    upload(){
        const formData = { image: this.state.file }

        let url = "http://localhost:8000/upload.php";
        axios.post(url, formData, { // receive two parameter endpoint url ,form data 
        })
        .then(res => { // then print response status
            console.warn(res.data);
        })

    }

    render() {
        let imgPreview;
        if (this.state.file) {
            imgPreview = <img src={this.state.file} alt='' />;
        }
        return (
            <form>
                <div className="form-group preview">
                    {imgPreview}
                </div>

                <div className="form-group">
                    <input type="file" className="form-control" onChange={this.uploadSingleFile} />
                </div>
                <button type="button" className="btn btn-primary btn-block" onClick={this.upload}>Upload</button>

            </form >
        )
    }
}
```

要上传文件，您需要一个 HTML 模板。在此模板中，您将创建一个“文件输入”元素，允许我们选择文件和一个上传文件的按钮。所以，在 **render()** 方法内部定义了 if 语句。

**注意:**当用户选择一个文件时会调用` **uploadSingleFile** `方法。它将获取所选文件的 file 对象，并将其存储在` **file** 状态。并将使用一个简单的 PHP 应用程序，该应用程序公开一个惟一的端点，该端点接受包含文件/图像的 POST 请求，将图像上传到服务器。

**阅读另:** [**如何在 React JS**](https://websolutionstuff.com/post/how-to-get-multiple-checkbox-value-in-react-js) 中获取多个复选框值】

**第四步:在 App.js 中添加组件**

在这一步，我们将在`src/App.js`文件中添加**imageuploadpreviewcomponent . js**文件。

```
import React from 'react';
import '../node_modules/bootstrap/dist/css/bootstrap.min.css';
import ImageUploadPreviewComponent from './ImageUploadPreviewComponent'

function App() {  

  return (  
    <div className="App">  
      <ImageUploadPreviewComponent/>  
    </div>  
  );  
}  

export default App;
```

**第五步:创建 PHP 文件**

在这一步，我们将创建一个 PHP 文件，命名为**upload.php**。并向其中添加以下代码。

```
<?php

    header("Access-Control-Allow-Origin: *");
    header("Access-Control-Allow-Methods: PUT, GET, POST");
    header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept");

    // Folder Path For Ubuntu
    // $folderPath = "/var/www/my-app/uploads";
    // Folder Path For Window
    $folderPath = "uploads/";

    $file_tmp = $_FILES['image']['tmp_name'];
    $file_ext = strtolower(end(explode('.',$_FILES['image']['name'])));
    $file = $folderPath . uniqid() . '.'.$file_ext;
    move_uploaded_file($file_tmp, $file);

   return json_encode(['status'=>true]);
?>
```

*   **阅读还:** [**如何在 React JS 中使用数组**](https://websolutionstuff.com/post/how-to-use-array-in-react-js)
*   **阅读也:** [**如何一步步安装 React JS**](https://websolutionstuff.com/post/how-to-install-react-js-step-by-step)
*   **阅读另:** [**如何在 Laravel 9**](https://websolutionstuff.com/post/how-to-upload-multiple-image-in-laravel-9) 中上传多个图像
*   **阅读还:** [**如何在 jQuery**](https://websolutionstuff.com/post/how-to-preview-image-before-upload-in-jquery) 中上传前预览图片

如果这篇文章有帮助，请点击拍手👏下面的按钮。几次以示支持。⬇⬇

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) *。*