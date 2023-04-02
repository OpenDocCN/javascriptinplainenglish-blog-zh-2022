# 如果您在项目中使用多个外部服务，这是很好的实践

> 原文：<https://javascript.plainenglish.io/using-multiple-external-services-in-your-project-af21d1463414?source=collection_archive---------7----------------------->

## 管理多个外部服务，以处理任何企业项目中的关键操作

![](img/a460c536767e30fa7f9ed2cc30c0805c.png)

Photo by [NordWood Themes](https://unsplash.com/fr/@nordwood?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 在项目中使用多个外部服务

您将需要管理多个外部服务来处理任何企业项目中的关键操作。例如，使用 Auth0 管理身份验证，使用脸书图形 API 进行社交管理，或者使用 Odoo 进行 CRM 管理

人们一直在他们的控制器中使用直接代码，并在同一个地方进行管理，我认为这不是一个好的做法。当代码库增加时，管理这些外部端点总是很困难

## 外部服务的示例

Instagram Graph API，微软 Graph API，Odoo 服务 API，预订 API。任何提供某种服务的端点

## 我们应该遵循哪些做法？

*   设计模式——遵循设计模式总是会让你的生活变得轻松。它可以是任何单一或工厂或任何其他设计模式
*   使用 Oops 原则——服务是可以在应用程序的后端或前端或任何级别使用的公共基础
*   服务版本化——因为服务可以在外部修改，所以维护服务版本很容易改变方法

## 实践中见

假设我们必须使用 WhatsApp graph APIs 来动态或以编程方式发送消息，另一个约束是我们使用的是他们的 graph API 版本 13。我们将创建一个名为`WhatsAppGraph13`的类来确认图形的版本，还将在该类中存储 Axios 属性，以便进行端点调用，从而存储 Axios 的默认值。为了使用`/messages`API，我们需要将在图形仪表板上生成的`phoneNumberId`

```
import Axios, { AxiosInstance } from 'axios'

class WhatsAppGraph13 {
  axios: AxiosInstance;
  phoneNumberId: string | undefined;

  constructor(token: string, phoneNumberId: string) {
    this.axios = Axios.create({
      baseURL: `https://graph.facebook.com/v13.0`,
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    this.phoneNumberId = phoneNumberId;
  }
}

export default WhatsAppGraph13;
```

现在，让我们创建一个方法`sendMessageToOnePerson`来发送消息并使用我们刚刚创建的属性

```
 sendMessageToOnePerson(
    recipientPhoneNumber: string,
    body: string
  ) {
    const commonPayload = {
      messaging_product: "whatsapp",
      recipient_type: "individual",
      to: recipientPhoneNumber,
      type: "text",
      text: {
        preview_url: false,
        body: body,
      },
    };
    return this.axios.post(`/${this.phoneNumberId}/messages`, commonPayload);
  }
```

在本例中，我们使用了我们创建的 Axios 实例，对于路由，我们将使用我们使用的另一个属性

以下程序的用法如下所示

```
 sendMessage(user: User){
    const body = LandingTemplate
    const service = new WhatsAppGraph13(process.env.token, process.env.number)
    service.sendMessageToOnePerson(user.phone, body)
  }
```

但是除此之外，我们还可以使用服务来管理实例。所以让我们创建一个名为`fromEnv`的静态方法

因此，让我们创建一个`env.ts`，并为环境添加一些结构

```
const Env = {
  WhatsApp: {
    AccessToken: process.env.NEXT_PUBLIC_ACCESS_TOKEN ?? '',
    PhoneNumberId: process.env.NEXT_PUBLIC_PHONE_NUMBER_ID ?? '',
    WebhookVerifyToken: process.env.NEXT_PUBLIC_WHATSAPP_CLOUD_API_VERIFY ?? '',
  },
  Google: {
    AnalyticId: process.env.NEXT_PUBLIC_GOOGLE_ANALYTICS_ID
  }
}

export default Env
```

现在，我们已经准备好了一个环境，我们可以编写另一个静态方法作为参考，该方法将创建一个实例，而无需将环境暴露给控制器

```
 static fromEnv(){
    const token = Env.WhatsApp.AccessToken
    const phoneNumberId = Env.WhatsApp.PhoneNumberId
    return new WhatsAppGraph13(token, phoneNumberId)
  }
```

该方法的用法如下所示

```
export const processWebhook = async (req: NextApiRequest) => {
  const { entry, object } = req.body as IWhatsappWebhookRequestPayload;
  const [event] = entry;
  const [primaryChange] = event.changes;
  // process webhook based on event
  if(primaryChange.field === 'messages' && primaryChange.value.messages){
    const whatsappService = WhatsAppGraph13.fromEnv()
    const from = primaryChange.value.messages.from
    await whatsappService.sendMessageToOnePerson(from, 'Hello world!')
  }
  return new CustomResponse(200, { event, object });
};
```

服务的整个源文件将如下所示

```
import Axios, { AxiosInstance } from "axios";
import Env from "../constant/env";

class WhatsAppGraph13 {
  axios: AxiosInstance;
  phoneNumberId: string | undefined;

  constructor(token: string, phoneNumberId: string) {
    this.axios = Axios.create({
      baseURL: `https://graph.facebook.com/v13.0`,
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    this.phoneNumberId = phoneNumberId;
  }

  sendMessageToOnePerson(
    recipientPhoneNumber: string,
    body: string
  ) {
    const commonPayload = {
      messaging_product: "whatsapp",
      recipient_type: "individual",
      to: recipientPhoneNumber,
      type: "text",
      text: {
        preview_url: false,
        body: body,
      },
    };
    return this.axios.post(`/${this.phoneNumberId}/messages`, commonPayload);
  }

  static fromEnv(){
    const token = Env.WhatsApp.AccessToken
    const phoneNumberId = Env.WhatsApp.PhoneNumberId
    return new WhatsAppGraph13(token, phoneNumberId)
  }
}

export default WhatsAppGraph13;
```

## 结论

创建服务还有其他方法，但这将有助于您更好地组织服务文件。

感谢阅读！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***