# 使用 AWS Cognito 和 Next.js 进行基本身份验证

> 原文：<https://javascript.plainenglish.io/basic-authentication-with-aws-cognito-nextjs-69ef122096cf?source=collection_archive---------13----------------------->

![](img/9e52e0951ec4848eba5c886b64a70878.png)

我以前写过不少关于认证的文章。这是另一篇用户授权文章。

然而，这一次，有点不一样了。以前的文章都是关于自己管理用户认证的。在本文中，我们将利用 AWS Cognito 及其用户池来实现相同的功能。

您可以在这里查看我以前的一些关于手动处理用户授权的文章:

1.  [如何用 Express & Passport.js](https://kelvinmwinuka.com/how-to-create-registration-authentication-with-express-passportjs/#more-918) 创建注册&认证。
2.  [如何在快递中处理密码重置](https://kelvinmwinuka.com/how-to-handle-password-reset-in-expressjs/)。
3.  [如何在快递中验证用户](https://kelvinmwinuka.com/how-to-verify-users-in-expressjs/)

# 设置

本文假设您已经设置了一个 AWS Cognito 用户池，并且还设置了一些 Next.js 样板代码。我将写另一篇文章解释如何使用 AWS 控制台设置 Cognito 用户池。

首先，我们来了解一下项目结构。

```
.
├── components
│   ├── layouts
│   │   └── InputLayout.js
│   ├── AuthLinkText.js
│   ├── InputField.js
│   ├── InputHelperText.js
│   ├── Label.js
│   └── SubmitButton.js
├── hooks
│   ├── useAuth.js
│   ├── useRegister.js
│   └── useValidationSchema.js
├── pages
│   ├── api
│   │   ├── confirm
│   │   │   ├── index.js
│   │   │   └── send.js
│   │   ├── password
│   │   │   ├── reset.js
│   │   │   └── reset_code.js
│   │   ├── login.js
│   │   └── register.js
│   ├── password
│   │   ├── reset.js
│   │   └── reset_code.js
│   ├── _app.js
│   ├── confirm.js
│   ├── index.js
│   ├── login.js
│   └── register.js
├── public
│   ├── favicon.ico
│   └── vercel.svg
├── styles
│   ├── Home.module.css
│   └── globals.css
├── README.md
├── next.config.js
├── package-lock.json
└── package.json
```

大多数都没什么特别的，因为它们是在设置 Next.js 项目时自动创建的。

“组件”文件夹包含所有可重用的定制组件，如表单输入字段和布局。

在这篇文章中，我将重点介绍“钩子”和“页面”文件夹。如果你想看完整的代码，你可以在 [Github](https://github.com/kelvinmwinuka/cognito-next) 上找到。

“hooks”文件夹有 3 个文件:

1.  useAuth.js 包含一个钩子来处理用户登录和密码重置。
2.  js 包含一个钩子来处理用户注册和验证。
3.  useValidationSchema.js 包含表单验证架构。我们不会在文章中涉及这一点。请随时查看回购的更多细节。

我更喜欢使用钩子，因为它们允许我将组件中的业务逻辑和 UI 逻辑分开。

“页面”文件夹有一个“API”子目录。这是所有后端代码所在的地方。

Next.js 使用基于文件系统的路由，因此文件结构决定了 API 端点。

API 子目录之外的所有其他文件和子目录将被视为前端页面。

确保安装了[@ AWS-SDK/client-cognito-identity-provider](https://www.npmjs.com/package/@aws-sdk/client-cognito-identity-provider)包。

您可以参考完整的[CognitoIdentityServiceProvider SDK](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-cognito-identity-provider/index.html#aws-sdkclient-cognito-identity-provider)来获得对本文所讨论内容的更深入的解释。

# 签约雇用

首先，让我们处理用户注册。导航到“pages/api/register.js”并添加以下代码:

```
import { CognitoIdentityProviderClient, SignUpCommand } from '[@aws](http://twitter.com/aws)-sdk/client-cognito-identity-provider'const { COGNITO_REGION, COGNITO_APP_CLIENT_ID } = process.envexport default async function handler(req, res) {
    if (req.method !== 'POST') return res.status(405).send()const params = {
        ClientId: COGNITO_APP_CLIENT_ID,
        Password: req.body.password,
        Username: req.body.username,
        UserAttributes: [
            {
                Name: 'email',
                Value: req.body.email
            }
        ]
    }const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO\_REGION
    })
    const signUpCommand = new SignUpCommand(params)try {
        const response = await cognitoClient.send(signUpCommand)
        return res.status(response['$metadata'].httpStatusCode).send()
    } catch (err) {
        console.log(err)
        return res.status(err['$metadata'].httpStatusCode).json({ message: err.toString() })
    }
}
```

这是“/api/register”端点的处理程序。包括一个 guard 子句，以确保只允许 POST 请求，对于任何其他类型的请求都返回 405 错误。

在参数中，我们有以下内容:

1.  ClientId —您在 AWS 控制台中为此用户池创建的应用程序客户端 Id。
2.  密码—用户选择的密码。
3.  用户名-用户选择的用户名。
4.  UserAttributes —用户在注册时提供的任何附加属性。默认的属性列表包括地址、昵称、生日、电话号码、电子邮件、姓氏、首选用户名、性别、个人资料、名字、zoneinfo、地区、更新时间、中间名、网站和姓名。您也可以添加自定义属性(例如，如果您正在为一个组织创建一个身份验证系统，则为“部门”)。

请记住，如果您正在设置自定义用户属性，您需要遵循以下格式:

```
{
    Name: 'custom:<AttributeName>',                
    Value: '<AttributeValue>'
}
```

在添加部门属性的情况下，它看起来像这样:

```
{
    Name: 'custom:Department',                
    Value: 'Engineering'
}
```

然后我们发送注册命令来触发用户注册。如果一切顺利，返回 status 200 响应，否则，返回来自 Cognito 的错误代码和错误的字符串化版本。

Cognito 通常会返回如下所示的错误:

```
UsernameExistsException: User already exists
...
{
  '$fault': 'client',
  '$metadata': {
    httpStatusCode: 400,
    requestId: '9442223e-ef29-40c1-880e-6689638d8042',
    extendedRequestId: undefined,
    cfId: undefined,
    attempts: 1,
    totalRetryDelay: 0
  },
  __type: 'UsernameExistsException'
}
```

抓取状态码和消息，然后转发到前端。

当请求成功时，Cognito 将返回如下所示的响应:

```
{
  '$metadata': {
    httpStatusCode: 200,
    requestId: '67f6d99c-d13c-4677-ab46-957d88f62bb9',
    extendedRequestId: undefined,
    cfId: undefined,
    attempts: 1,
    totalRetryDelay: 0
  },
  AuthenticationResult: {
    AccessToken: "...",
    ExpiresIn: 3600,
    NewDeviceMetadata: undefined,
    RefreshToken: "...",
    TokenType: "Bearer"
  },
  ChallengeName: undefined,
  ChallengeParameters: {},
  Session: undefined
}
```

对于这个应用程序，我们只对身份验证结果感兴趣，因为它包含访问和刷新令牌。

充实 useRegister 挂钩，以便利用我们在上面创建的 API 端点。

使用以下逻辑创建一个名为“register”的方法:

```
import { useRouter } from 'next/router'export default function useRegister() {const router = useRouter()const register = (values, { setSubmitting }) => {
        fetch('/api/register', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(values)
        }).then(res => {
            if (!res.ok) throw res
            router.push({
                pathname: '/confirm',
                query: { username: values?.username }
            },
                "/confirm")
        }).catch(err => {
            console.error(err)
        }).finally(() => {
            setSubmitting(false)
        })
    }const confirm = (values, { setSubmitting }) => {
        // Confirm the user
    }return {
        register,
        confirm
    }
}
```

register 方法是我们注册表单的提交方法。“values”对象包含表单数据,“setSubmitting”允许我们在处理完请求后更新加载状态。

这将是这个项目中大多数钩子的共同主题。

将 Content-Type 头设置为“application/json ”,以帮助 Next.js 解析请求体。

在这个方法中，我们调用 register 端点并传递所有表单值(包括用户名、电子邮件和密码)。如果请求成功，我们将重定向到确认页面，并提示用户验证他们的电子邮件地址。在[验证](https://kelvinmwinuka.com/basic-authentication-with-aws-cognito-and-nextjs#verification)部分有更多相关信息。

您可能会注意到我们这里有一个空的确认方法。该方法将处理验证用户的请求。我们也将在验证阶段讨论这一点。

下面是注册表单的样子，注意我们导入了 useRegister 钩子，并将 Register 方法作为表单提交处理程序传递。

```
import { Formik } from "formik";
import InputLayout from "../components/layouts/InputLayout";
import Label from "../components/Label";
import InputField from "../components/InputField";
import InputHelperText from "../components/InputHelperText";
import AuthLinkText from "../components/AuthLinkText";
import SubmitButton from "../components/SubmitButton";
import useValidationSchema from "../hooks/useValidationSchema";
import useRegister from '../hooks/useRegister'
import Link from "next/link";export default function Register() {const { registerSchema } = useValidationSchema()
    const { register } = useRegister()return (
        <div style={{
            padding: "10px"
        }}>
            <Formik
                initialValues={{
                    username: "",
                    email: "",
                    password: "",
                    confirm_password: ""
                }}
                validationSchema={registerSchema}
                onSubmit={register}
                validateOnMount={false}
                validateOnChange={false}
                validateOnBlur={false}>
                {({
                    isSubmitting,
                    errors,
                    values,
                    handleSubmit,
                    handleChange,
                    handleBlur
                }) => (
                    <form onSubmit={handleSubmit}>
                        <InputLayout>
                            <Label>Username</Label>
                            <InputField
                                type="text"
                                name="username"
                                placeholder="Username"
                                onChange={handleChange}
                                onBlur={handleBlur}
                                value={values?.username}
                            />
                            <InputHelperText isError>{errors?.username}</InputHelperText>
                        </InputLayout>
                        <InputLayout>
                            <Label>Email</Label>
                            <InputField
                                type="email"
                                name="email"
                                placeholder="Email"
                                onChange={handleChange}
                                onBlur={handleBlur}
                                value={values?.email}
                            />
                            <InputHelperText isError>{errors?.email}</InputHelperText>
                        </InputLayout>
                        <InputLayout>
                            <Label>Password</Label>
                            <InputField
                                type="password"
                                name="password"
                                placeholder="Password"
                                onChange={handleChange}
                                onBlur={handleBlur}
                                value={values?.password}
                            />
                            <InputHelperText isError>{errors?.password}</InputHelperText>
                        </InputLayout>
                        <InputLayout>
                            <Label>Confirm password</Label>
                            <InputField
                                type="password"
                                name="confirm_password"
                                placeholder="Confirm password"
                                onChange={handleChange}
                                onBlur={handleBlur}
                                value={values?.confirm_password}
                            />
                            <InputHelperText isError>{errors?.confirm_password}</InputHelperText>
                        </InputLayout>
                        <InputLayout>
                            <AuthLinkText href="/login">Already have an account? Log in</AuthLinkText>
                        </InputLayout>
                        <SubmitButton isSubmitting={isSubmitting} />
                    </form>
                )}
            </Formik>
        </div>
    )
}
```

# 签到

现在我们已经注册了我们的用户，是时候允许他们登录我们的应用程序了，方法是根据我们的 Cognito 用户池对他们进行身份验证。

将以下代码添加到“pages/api/login.js”文件中。

```
import { CognitoIdentityProviderClient, AdminInitiateAuthCommand } from "@aws-sdk/client-cognito-identity-provider"

const { COGNITO_REGION, COGNITO_APP_CLIENT_ID, COGNITO_USER_POOL_ID } = process.env

export default async function handler(req, res) {
    if (req.method !== 'POST') return res.status(405).send()

    const params = {
        AuthFlow: 'ADMIN_USER_PASSWORD_AUTH',
        ClientId: COGNITO_APP_CLIENT_ID,
        UserPoolId: COGNITO_USER_POOL_ID,
        AuthParameters: {
            USERNAME: req.body.username,
            PASSWORD: req.body.password
        }
    }

    const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO_REGION
    })
    const adminInitiateAuthCommand = new AdminInitiateAuthCommand(params)

    try {
        const response = await cognitoClient.send(adminInitiateAuthCommand)
        console.log(response)
        return res.status(response['$metadata'].httpStatusCode).json({
            ...response.AuthenticationResult
        })
    } catch(err) {
        console.log(err)
        return res.status(err['$metadata'].httpStatusCode).json({ message: err.toString() })
    }
}
```

目前，我们只处理用户名/密码认证。为此，我们需要使用`ADMIN_USER_PASSWORD_AUTH`流程。此身份验证流程需要开发人员凭据。如果你在一个安全的服务器上认证用户，这是推荐的方法，优于使用`USER_PASSWORD_AUTH`的`InitiateAuthCommand`。

最后一个参数是 AuthParameters。它只包含提交表单时传递给端点的用户名和密码。这里要小心，确保 auth 参数都是大写的，否则，它们不会被识别。

现在让我们把注意力转移到“useAuth”钩子上。将此代码添加到“hooks/useAuth.js”文件中:

```
import { useRouter } from "next/router";export default function useAuth(){const router = useRouter()const login = (values, { setSubmitting }) => {
    fetch('/api/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(values)
    }).then(res => {
      if (!res.ok) throw res
    }).then(data => {
      console.log(data)
    }).catch(async err => {
      const responseData = await err.json()
      if (responseData?.message?.includes("UserNotConfirmedException:")) {
        // Trigger confirmation code email
        await fetch('/api/confirm/send', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ username: values.username })
        })
        await router.push(
      {
            pathname: "/confirm",
            query: {username: values.username},
          },
          "/confirm")
      }
    }).finally(() => {
      setSubmitting(false)
    })
  }const resetPasswordRequest = (values, { setSubmitting }) => {
    // Send the password reset code
  }const resetPassword = (values, { setSubmitting }) => {
    // Send request to reset password
  }return {
    login,
    resetPasswordRequest,
    resetPassword
  }
}
```

这里我们有一个类似于上面创建的注册方法的登录方法。“值”对象表示我们的表单数据(用户名和密码)。

需要注意的是，如果用户还没有被验证/确认，Cognito 将不允许用户被认证。因此尝试使用未经确认的用户登录将会返回一个错误。

要处理这种情况，触发一个端点向用户发送确认电子邮件，然后将他们重定向到确认页面，以便他们可以被验证。在[验证](https://kelvinmwinuka.com/basic-authentication-with-aws-cognito-and-nextjs#verification)部分有更多关于这个端点的信息。

我们的登录页面有以下代码:

```
import { Formik } from "formik";
import InputLayout from "../components/layouts/InputLayout";
import Label from "../components/Label";
import InputField from "../components/InputField";
import InputHelperText from "../components/InputHelperText";
import AuthLinkText from "../components/AuthLinkText";
import SubmitButton from "../components/SubmitButton";
import useAuth from "../hooks/useAuth";
import useValidationSchema from "../hooks/useValidationSchema";
import { useRouter } from "next/router";export default function Login() {const router = useRouter();
  const { success } = router.query;const { loginSchema } = useValidationSchema();
  const { login } = useAuth();return (
    <div style={{
      padding: "10px"
    }}>
      {
        success === "true" &&
        <div style={{
          paddingTop: "10px",
          paddingBottom: "10px",
          color: "green"
        }}>
          {'You\\'re signed up!'}
        </div>
      }
      <Formik
        initialValues={{
          username: "",
          password: ""
        }}
        validationSchema={loginSchema}
        onSubmit={login}
        validateOnMount={false}
        validateOnChange={false}
        validateOnBlur={false}>
        {({
          isSubmitting,
          errors,
          values,
          handleChange,
          handleBlur,
          handleSubmit
        }) => (
          <form onSubmit={handleSubmit}>
            <InputLayout>
              <Label>Username</Label>
              <InputField
                type="text"
                name="username"
                placeholder="Username or email"
                onChange={handleChange}
                onBlur={handleBlur}
                value={values?.username}
              />
              <InputHelperText isError>{errors?.username}</InputHelperText>
            </InputLayout>
            <InputLayout>
              <Label>Password</Label>
              <InputField
                type="password"
                name="password"
                placeholder="Password"
                onChange={handleChange}
                onBlur={handleBlur}
                value={values?.password}
              />
              <InputHelperText isError>{errors?.password}</InputHelperText>
            </InputLayout>
            <InputLayout>
              <AuthLinkText href="/password/reset_code">{'Forgot password?'}</AuthLinkText>
            </InputLayout>
            <InputLayout>
              <AuthLinkText href="/register">{'Don\\'t have an account? Register.'}</AuthLinkText>
            </InputLayout>
            <SubmitButton isSubmitting={isSubmitting} />
          </form>
        )}
      </Formik>
    </div>
  );
}
```

就像前面一样，我们导入 useAuth 钩子，并利用它的 login 方法作为表单提交处理程序。

我们将在[密码重置](https://kelvinmwinuka.com/basic-authentication-with-aws-cognito-and-nextjs#passwordreset)部分讨论 useAuth 挂钩中的两种密码重置方法。

# 确认

所以我们已经注册了我们的用户，但是我们不能验证他们，因为他们没有被验证。让我们解决这个问题。

在我们继续之前，需要注意一些事情:

1.  我已经设置了我的用户池，使用电子邮件代码进行验证。AWS 将在这里发送一封电子邮件，其中包含用户必须在您的应用程序上手动输入的代码。其他身份验证方法包括:可点击的验证链接和发送到他们电话号码的验证码。如果您使用任何其他验证方法(除了电话号码的验证码)，那么您可以跳过这一部分。
2.  成功注册后，Cognito 将自动触发所选的验证方法。验证也可以通过 SDK 触发。

在“pages/api/confirm/index.js”文件中，添加以下代码:

![](img/40be220c944be216b2349770248fbaa5.png)

```
import {
    CognitoIdentityProviderClient,
    ConfirmSignUpCommand
} from "[@aws](http://twitter.com/aws)-sdk/client-cognito-identity-provider"const { COGNITO_REGION, COGNITO_APP_CLIENT_ID } = process.envexport default async function handler (req, res) {
    if (req.method !== 'POST') return res.status(405).send()const params = {
        ClientId: COGNITO_APP_CLIENT_ID,
        ConfirmationCode: req.body.code,
        Username: req.body.username
    }const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO_REGION
    })
    const confirmSignUpCommand = new ConfirmSignUpCommand(params)try {
        const response = await cognitoClient.send(confirmSignUpCommand)
        console.log(response)
        return res.status(response['$metadata'].httpStatusCode).send()
    } catch (err) {
        console.log(err)
        return res.status(err['$metadata'].httpStatusCode).json({ message: err.toString() })
    }
}
```

在这里创建并发送带有以下参数的`confirmSignUpCommand`:

1.  ClientId。
2.  ConfirmationCode —由 Cognito 发送到用户电子邮件/电话的代码。
3.  用户名—您要验证的用户的用户名。

注意，因为这是确认目录中的索引文件，所以我们在调用这个端点时不需要指定文件名。端点应该是“/api/confirm”

在同一个确认目录中，我们有一个名为“send.js”的文件。该文件负责手动触发确认码电子邮件。

将以下代码添加到该文件中:

```
import {
    CognitoIdentityProviderClient,
    ResendConfirmationCodeCommand
} from "[@aws](http://twitter.com/aws)-sdk/client-cognito-identity-provider"const { COGNITO_REGION, COGNITO_APP_CLIENT_ID } = process.envexport default async function handler (req, res) {
    if (req.method !== 'POST') return res.status(405).send()const params = {
        ClientId: COGNITO_APP_CLIENT_ID,
        Username: req.body.username
    }const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO_REGION
    })
    const resendConfirmationCodeCommand = new ResendConfirmationCodeCommand(params)try {
        const response = await cognitoClient.send(resendConfirmationCodeCommand)
        console.log(response)
        return res.status(response['$metadata'].httpStatusCode).send()
    } catch (err) {
        console.log(err)
        return res.stat(err['$metadata'].httpStatusCode).json({ message: err.toString() })
    }
}
```

在这里，只需创建并发送带有 params 对象的`ResendConfirmationCodeCommand`，该对象包含您想要验证的用户的 ClientId 和用户名。

Cognito 将搜索具有指定用户名的用户，然后根据您的设置和/或提供的设置向他们的电子邮件/电话号码发送验证码。

你可能想知道为什么这个命令叫做`ResendConfirmationCodeCommand`。

Cognito 会在注册时自动向用户发送一个验证码。

如果您手动触发注册，那么您总是“重新发送”代码。

还记得 useRegister 钩子中“confirm”方法吗？是充实它的时候了。

在该方法中添加以下逻辑:

```
const confirm = (values, { setSubmitting }) => {
        fetch('/api/confirm', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(values)
        }).then(res => {
            if (!res.ok) throw res
            router.push({
                pathname: '/login',
                query: { confirmed: true }
            },
                "/login")
        }).catch(err => {
            console.error(err)
        }).finally(() => {
            setSubmitting(false)
        })
    }
```

从此方法中，使用表单值调用“/api/confirm”端点。如果确认成功，将用户重定向到登录页面，以便他们可以登录。

下面是“pages/confirm.js”文件中的确认页面:

```
import { Formik } from "formik";
import InputLayout from "../components/layouts/InputLayout";
import Label from "../components/Label";
import InputField from "../components/InputField";
import InputHelperText from "../components/InputHelperText";
import SubmitButton from "../components/SubmitButton";
import useValidationSchema from "../hooks/useValidationSchema";
import useRegister from "../hooks/useRegister";
import { useRouter } from "next/router";export default function Confirm(){const router = useRouter();
    const { username } = router.query;const { confirm } = useRegister();
    const { confirmSchema } = useValidationSchema();return (
        <div style={{
            padding: "10px"
        }}>
            <Formik
                initialValues={{
                    username: username,
                    code: ""
                }}
                onSubmit={confirm}
                validationSchema={confirmSchema}
                validateOnMount={false}
                validateOnChange={false}
                validateOnBlur={false}>
                {
                    ({
                        isSubmitting,
                        errors,
                        values,
                        handleSubmit,
                        handleChange,
                        handleBlur
                     }) => (
                        <form onSubmit={handleSubmit}>
                            <InputLayout>
                                <Label>Confirmation Code</Label>
                                <InputField
                                    type={"text"}
                                    name={"code"}
                                    placeholder={"Code"}
                                    onChange={handleChange}
                                    onBlur={handleBlur}
                                    value={values?.code}
                                />
                                <InputHelperText isError>{errors?.code}</InputHelperText>
                            </InputLayout>
                            <SubmitButton isSubmitting={isSubmitting} />
                        </form>
                    )
                }
            </Formik>
        </div>
    )
}
```

# 密码重置

任何授权系统中最重要的特性之一是重置密码的能力。

幸运的是，Cognito 使密码重置变得非常简单。

密码重置流程类似于验证流程，但有一些额外的步骤:

1.  用户单击“忘记密码”链接，并被重定向到提示他们输入用户名的页面。
2.  向用户的电子邮件/号码发送确认码。
3.  如果代码发送成功，将用户重定向到一个重置页面，用户在该页面上输入代码和新密码。

首先，准备端点来触发包含代码的验证电子邮件。

将以下代码添加到“pages/API/password/reset _ code . js”中:

```
import { CognitoIdentityProviderClient, ForgotPasswordCommand } from '[@aws](http://twitter.com/aws)-sdk/client-cognito-identity-provider'const { COGNITO_REGION, COGNITO_APP_CLIENT_ID } = process.envexport default async function handler (req, res) {
    if (req.method !== 'POST') return res.status(405).send()const params = {
        ClientId: COGNITO_APP_CLIENT_ID,
        Username: req.body.username
    }const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO_REGION
    })
    const forgotPasswordCommand = new ForgotPasswordCommand(params)try {
        const response = await cognitoClient.send(forgotPasswordCommand)
        console.log(response)
        return res.status(response['$metadata'].httpStatusCode).send()
    } catch (err) {
        console.log(err)
        return res.status(err['$metadata'].httpStatusCode).json({ message: toString() })
    }
}
```

这里我们接受“ForgotPasswordCommand”命令的 ClientId 和 username 参数。Cognito 将找到具有匹配用户名的用户，并使用配置的方法向他们发送验证码。

在“pages/api/password/reset.js”文件中，添加以下代码:

```
import {
    CognitoIdentityProviderClient,
    ConfirmForgotPasswordCommand
} from "[@aws](http://twitter.com/aws)-sdk/client-cognito-identity-provider"const { COGNITO_REGION, COGNITO_APP_CLIENT_ID } = process.envexport default async function handler(req, res) {
    if (req.method !== 'POST') return res.status(405).send()const params = {
        ClientId: COGNITO_APP_CLIENT_ID,
        ConfirmationCode: req.body.code,
        Password: req.body.password,
        Username: req.body.username
    }const cognitoClient = new CognitoIdentityProviderClient({
        region: COGNITO_REGION
    })
    const confirmForgotPasswordCommand = new ConfirmForgotPasswordCommand(params)try {
        const response = await cognitoClient.send(confirmForgotPasswordCommand)
        console.log(response)
        return res.status(response['$metadata'].httpStatusCode).send()
    } catch (err) {
        console.log(err)
        return res.status(err['$metadata'].httpStatusCode).json({ message: err.toString() })
    }
}
```

在这里，我们接受发送给用户的确认码、他们的新密码和用户名。

Cognito 将负责所有的逻辑，确保所提供的代码是有效的，并且是发送给具有指定用户名的用户的代码。

你会记得在 useAuth 钩子中，我们有两个空方法“resetPasswordRequest”和“resetPassword”。我们现在要把它们充实起来。

将以下逻辑添加到这些方法中:

```
const resetPasswordRequest = (values, { setSubmitting }) => {
    fetch('/api/password/reset\_code', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(values)
    }).then(res => {
      if (!res.ok) throw res
      router.push({
        pathname: '/password/reset',
        query: { username: values.username }
      },
        "/password/reset")
    }).catch(err => {
      console.error(err)
    }).finally(() => {
      setSubmitting(false)
    })
  }const resetPassword = (values, { setSubmitting }) => {
    fetch('/api/password/reset', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(values)
    }).then(res => {
      if (!res.ok) throw res
      router.push({
        pathname: '/login',
        query: { reset: true }
      },
        "/login")
    }).catch(err => {
      console.error(err)
    }).finally(() => {
      setSubmitting(false)
    })
  }
```

`resetPasswordRequest`方法触发“/api/password/reset_code”端点。

从用户的角度来看，他们被重定向到输入用户名的页面。提交表单后，他们会收到一封电子邮件，并被重定向到密码重置页面(如果电子邮件发送成功)。

`resetPassword`方法触发“/api/password/reset”端点来实际重置密码。

以下是忘记密码表单的外观:

```
import { Formik } from "formik";
import InputLayout from "../../components/layouts/InputLayout";
import Label from "../../components/Label";
import InputField from "../../components/InputField";
import InputHelperText from "../../components/InputHelperText";
import SubmitButton from "../../components/SubmitButton";
import useValidationSchema from "../../hooks/useValidationSchema";
import useAuth from '../../hooks/useAuth';export default function ResetCode(){const { resetPasswordRequestSchema } = useValidationSchema();
    const { resetPasswordRequest } = useAuth();return (
        <div style={{
            padding: "10px"
        }}>
            <Formik
                initialValues={{
                    username: ""
                }}
                onSubmit={resetPasswordRequest}
                validationSchema={resetPasswordRequestSchema}
                validateOnMount={false}
                validateOnChange={false}
                validateOnBlur={false}
                >
                {
                    ({
                        isSubmitting,
                        errors,
                        values,
                        handleSubmit,
                        handleChange,
                        handleBlur
                    }) => (
                        <form onSubmit={handleSubmit}>
                            <InputLayout>
                                <Label>Username</Label>
                                <InputField
                                    type={"text"}
                                    name={"username"}
                                    placeholder={"Username"}
                                    onChange={handleChange}
                                    onBlur={handleBlur}
                                    value={values?.username}
                                />
                                <InputHelperText isError>{errors?.username}</InputHelperText>
                            </InputLayout>
                            <SubmitButton isSubmitting={isSubmitting} />
                        </form>
                    )
                }
            </Formik>
        </div>
    )
}
```

下面是密码重置表单的外观:

```
import { Formik } from "formik";
import InputLayout from "../../components/layouts/InputLayout";
import Label from "../../components/Label";
import InputField from "../../components/InputField";
import InputHelperText from "../../components/InputHelperText";
import SubmitButton from "../../components/SubmitButton";
import useValidationSchema from "../../hooks/useValidationSchema";
import useAuth from '../../hooks/useAuth';
import { useRouter } from "next/router";export default function Reset(){const router = useRouter()
    const { username } = router.queryconst { resetPasswordSchema } = useValidationSchema();
    const { resetPassword } = useAuth()return (
        <div style={{
            padding: "10px"
        }}>
            <Formik
                initialValues={{
                    username: username,
                    code: "",
                    password: "",
                    confirm\_password: ""
                }}
                validationSchema={resetPasswordSchema}
                onSubmit={resetPassword}
                validateOnMount={false}
                validateOnChange={false}
                validateOnBlur={false}
            >
                {
                    ({
                        isSubmitting,
                        errors,
                        values,
                        handleSubmit,
                        handleBlur,
                        handleChange
                    }) => (
                        <form onSubmit={handleSubmit}>
                            <InputLayout>
                                <Label>Reset code</Label>
                                <InputField
                                    type={"text"}
                                    name={"code"}
                                    placeholder={"Reset code"}
                                    onChange={handleChange}
                                    onBlur={handleBlur}
                                    value={values?.code}
                                />
                                <InputHelperText isError>{errors?.code}</InputHelperText>
                            </InputLayout>
                            <InputLayout>
                                <Label>New password</Label>
                                <InputField
                                    type={"password"}
                                    name={"password"}
                                    placeholder={"New password"}
                                    onChange={handleChange}
                                    onBlur={handleBlur}
                                    value={values?.password}
                                />
                                <InputHelperText isError>{errors?.password}</InputHelperText>
                            </InputLayout>
                            <InputLayout>
                                <Label>Confirm password</Label>
                                <InputField
                                    type={"password"}
                                    name={"confirm_password"}
                                    placeholder={"Confirm password"}
                                    onChange={handleChange}
                                    onBlur={handleBlur}
                                    value={values?.confirm_password}
                                />
                                <InputHelperText isError>{errors?.confirm_password}</InputHelperText>
                            </InputLayout>
                            <SubmitButton isSubmitting={isSubmitting} />
                        </form>
                    )
                }
            </Formik>
        </div>
    )
}
```

# 警告

我们刚刚创建的实现的一个主要警告是，2 个或更多的用户实际上可以用同一个电子邮件注册。

我们不希望任何用户收到另一个用户的密码重置代码。

出于这一原因以及许多其他原因，您可能希望为每个用户强制使用唯一的电子邮件。

我们可以使用 Cognito 触发器轻松实现这一点，cogn ITO 触发器是运行定制 lambda 函数的事件触发器。这些允许我们定制我们的工作流程。

我们可以在以下任何事件(以及更多事件)期间触发 lambdas:

1.  预注册—就在触发 Cognito 注册之前。
2.  预认证—就在用户被 Cognito 认证之前。
3.  自定义消息—就在发送验证/确认消息之前。我们可以在这里动态编辑消息。
4.  身份验证后—用户成功通过身份验证后。如果身份验证失败，这将不会被触发。
5.  确认后—用户通过验证/确认后。您可以使用它来发送欢迎电子邮件或启用某些只有已确认用户才能使用的权限。

这些只是我们可用的触发器中的几个。你可以在这里找到关于这些触发器[的更多信息。](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools-working-with-aws-lambda-triggers.html)

在我们的例子中，我们最感兴趣的触发器是预注册触发器。我们可以检查是否有任何当前用户的电子邮件地址与我们刚刚收到的注册电子邮件地址相同。如果是这样，在 Cognito 注册之前抛出一个错误并失败。

我将发表一篇文章来演示如何实现这一点。

【https://kelvinmwinuka.com】最初发表于[](https://kelvinmwinuka.com/basic-authentication-with-aws-cognito-and-nextjs)**。**

**更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**