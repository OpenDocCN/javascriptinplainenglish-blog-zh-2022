# 如何在 Angular 13 生成二维码

> 原文：<https://javascript.plainenglish.io/how-to-generate-qr-code-in-angular-13-9d0f8a133773?source=collection_archive---------20----------------------->

![](img/bab77ac9dc92be5094bf797fe2950675.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将看到如何在 angular 13 中生成二维码。在本例中，我们将使用 angularx-qrcode npm 包在 angular 13 应用程序中生成 QR 码。我们将简单地安装 angularx-qrcode npm 包，并使用 QRCodeModule 模块来生成 QR 代码。

那么，我们来看看如何在 angular 13 中生成二维码，angular 13 二维码生成器示例，如何在 angular 12/13 中创建二维码，angular 二维码生成器，angular rx-QR code 示例。

**第一步:创建新应用**

在这一步，我们将使用下面的命令创建一个新的角度应用。

```
ng new qr-code
```

**阅读还:** [**如何在 Laravel 9**](https://websolutionstuff.com/post/how-to-create-dynamic-xml-sitemap-in-laravel-9) 中创建动态 XML 站点地图

**第二步:安装 angularx-qrcode npm 包**

在这一步，我们将安装**angular rx-QR code**包

```
npm install angularx-qrcode --save
```

**第三步:导入 QRCodeModule**

现在，我们将导入 QRCodeModule 模块。

**src/app/app.module.ts**

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { QRCodeModule } from 'angularx-qrcode';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    QRCodeModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**读也:** [**两路数据装订成角**12](https://websolutionstuff.com/post/two-way-data-binding-in-angular-12)

**步骤 4:更新 ts 文件**

在此步骤中，我们将更新 app.component.ts 文件。

**src/app/app . component . ts**

```
import { Component, VERSION } from '@angular/core';@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  public QrCode: string = null; constructor() {
    this.QrCode = 'websolutionstuff.com';
  }
}
```

**第五步:更新 HTML 文件**

现在，我们将更新 app.component.html 文件。

**src/app/app . component . html**

```
<h2 style="text-align:center;margin-top:40px">How To Generate QR Code In Angular 13 - Websolutionstuff</h2><qrcode
  [qrdata]="'stringQrCode'"
  [width]="300"
  [errorCorrectionLevel]="'M'"
  style="text-align:center"
></qrcode>
```

**阅读也:** [**有角度的 13 个裁剪图像上传前带预览**](https://websolutionstuff.com/post/angular-13-crop-image-before-upload-with-preview)

**第六步:运行服务器**

最后，我们需要使用下面的命令运行服务器。

```
ng serve
```

现在，转到您的 web 浏览器，键入给定的 URL 并查看应用程序输出。

[http://localhost:4200](http://localhost:4200)

**输出:**

![](img/68627d0a7a37f391d61e156ceea23a2b.png)

**你可能也会喜欢:**

*   **阅读也:** [**如何在 Node.js 中生成二维码**](https://websolutionstuff.com/post/how-to-generate-qr-code-in-node-js)
*   **阅读也:** [**Laravel 9 条码生成器示例**](https://websolutionstuff.com/post/laravel-9-barcode-generator-example)
*   **阅读还:** [**Laravel 9 二维码生成器示例**](https://websolutionstuff.com/post/laravel-9-qr-code-generator-example)
*   **阅读另:** [**如何使用 Javascript 生成二维码**](https://websolutionstuff.com/post/how-to-generate-qr-code-using-javascript)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，****[***不和***](https://discord.gg/GtDtUAvyhW)*** *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。***