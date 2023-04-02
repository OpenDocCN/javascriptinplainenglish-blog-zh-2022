# 如何使用 Vuetify 创建复选框

> 原文：<https://javascript.plainenglish.io/vuetify-checkbox-99d62eb1aefe?source=collection_archive---------8----------------------->

![](img/6b4b1d6f56fd2ce400917c57a4d75ead.png)

复选框允许用户在两个值之间进行选择。当试图获得布尔输入(真或假)时，可以使用它们，也许是在待办事项应用程序中检查任务以显示完成，或者决定是否在 UI 中接受许可协议。在本文中，我们将学习如何在 Vuetify 中创建复选框。

# v 形复选框组件

Vuetify 提供了用于创建复选框的`v-checkbox`组件:

```
<template>
  <v-app>
    <v-row class="ma-2" justify="center">
      <v-checkbox></v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/00084485e44ed15b06f122c76b0c1105.png)

# 从代码设置复选框值

为了控制复选框的当前值，我们可以使用`v-model`在`v-checkbox`和变量之间创建一个双向绑定。

```
<template>
  <v-app>
    <div class="ma-2 d-flex justify-center">
      <v-checkbox v-model="checked"></v-checkbox>
    </div>
    <div class="ma-2 d-flex justify-center">
      <v-btn color="indigo" dark @click="checked = true">Check</v-btn>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    checked: false,
  }),
};
</script>
```

在上面的代码中，我们创建了一个复选框和它下面的[按钮](https://codingbeautydev.com/blog/vuetify-buttons/)。

![](img/7332a0524ddca57eeff951efabc567c9.png)

点击[按钮](https://codingbeautydev.com/blog/vuetify-buttons/)会将`checked`设置为`true`，这将反映在复选框上:

![](img/fa7c487105169ab9b46101ac1a63f2bb.png)

# 用美化来美化

使用 Vuetify 材料设计框架创建优雅 web 应用程序的完整指南。

![](img/ff271935eabc3e42d8f111285dca7821.png)

在这里下载免费的[](https://mailchi.mp/583226ee0d7b/beautify-with-vuetify)****！****

# **验证复选框标签**

**我们可以用`label`属性标记一个 Vuetify 复选框:**

```
<template>
  <v-app>
    <v-row class="ma-2" justify="center">
      <v-checkbox v-model="checked" label="Coding Beauty"></v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    checked: false,
  }),
};
</script>
```

**![](img/623a8d0fd6aa5f80e86c19c21651cfa1.png)**

# **验证复选框标签插槽**

**要在复选框标签中包含 HTML 内容，我们可以将它放在`label`槽中:**

```
<template>
  <v-app>
    <v-row class="ma-2" justify="space-around">
      <v-checkbox color="indigo" input-value="true">
        <template v-slot:label>
          Visit the&nbsp;
          <a
            target="_blank"
            href="https://codingbeautydev.com"
            @click.stop
            v-on="on"
          >
            Coding Beauty website
          </a>
        </template>
      </v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

**![](img/918da5b3ac4aa06c7b10ae838605e5c9.png)**

# **在 Vuetify 中自定义复选框颜色**

**`color`属性允许我们设置复选框背景的[颜色](https://codingbeautydev.com/blog/vuetify-colors):**

```
<template>
  <v-app>
    <v-row class="ma-2" justify="center">
      <v-checkbox
        v-model="checked"
        label="Coding Beauty"
        color="green"
      ></v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    checked: false,
  }),
};
</script>
```

**![](img/fde8a5b85c36f7ef11ff6e797c85297c.png)**

# **禁用复选框**

**我们可以关闭复选框与`disabled`道具的交互。禁用后，它将不再接受输入。**

```
<template>
  <v-app>
    <v-row class="ma-2" justify="space-around">
      <v-checkbox
        label="on disabled"
        color="green"
        input-value="true"
        disabled
      ></v-checkbox>
      <v-checkbox
        label="off disabled"
        color="green"
        disabled
      ></v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

**![](img/8fbbed57a8344ccd9c245d9ccb084d11.png)**

# **不确定复选框**

**我们可以通过使用`indeterminate`属性使复选框不确定**

```
<template>
  <v-app>
    <v-row class="ma-2" justify="space-around">
      <v-checkbox label="indeterminate" color="red" indeterminate></v-checkbox>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

**![](img/b8ea5b9c358c1a53084f8ef3d7b70ff6.png)**

# **摘要**

**当我们需要接受布尔输入时，我们可以使用复选框。Vuetify 提供了`v-checkbox`组件来创建它，并提供各种道具进行定制。**

**[*注册*](http://eepurl.com/hRfyJL) *订阅我们的每周时事通讯，了解关于 Vuetify 和 Vue JS 的最新提示和教程。***

***在*[*【codingbeautydev.com】*](https://codingbeautydev.com/blog/vuetify-checkbox/)*获取更新文章。***