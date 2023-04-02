# Vuetify Breadcrumbs:如何使用 Vuetify 创建 Breadcrumbs

> 原文：<https://javascript.plainenglish.io/vuetify-breadcrumbs-eab9af62793f?source=collection_archive---------4----------------------->

![](img/5d19895ae1468e799e8b9603f032b654.png)

面包屑是导航助手，允许用户跟踪和维护他们在网站中的位置。它们作为导航工具，使用户能够理解当前页面和更高级页面之间的关系。在本文中，我们将学习如何使用 Vuetify breadcrumbs 组件创建 breadcrumbs。

# Vuetify Breadcrumbs 组件(`v-breadcrumbs`)

Vuetify 提供了用于创建和显示面包屑的`v-breadcrumbs`组件。breadcrumbs 组件带有一个`items`属性，它接受一个数组，该数组包含关于 breadcrumbs 中每一项的信息。每个数组元素都是一个表示一项的对象。下面是我们可以设置的该对象的一些属性:

*   `text`:设置该项目的显示文本。
*   `href`:设置用户通过点击面包屑项目可以导航到的位置。
*   `disabled`:决定用户是否可以点击面包屑导航到`href`指定的位置。

```
<template>
  <v-app>
    <v-breadcrumbs :items="items"></v-breadcrumbs>
  </v-app>
</template>
<script>
export default {
  name: 'App',
  data: () => ({
    items: [
      {
        text: 'Home',
        disabled: false,
        href: 'breadcrumbs_home',
      },
      {
        text: 'Link 1',
        disabled: false,
        href: 'breadcrumbs_link_1',
      },
      {
        text: 'Link 2',
        disabled: true,
        href: 'breadcrumbs_link_2',
      },
    ],
  }),
};
</script>
```

![](img/ac920d35deb41b7fc6d27e0d3561bb24.png)

# 将面包屑分隔器虚拟化

我们可以使用`divider`属性定制面包屑之间显示的分隔符。默认分隔符是正斜杠(`/`)。

```
<template>
  <v-app>
    <div>
      <v-breadcrumbs :items="items" divider="-"></v-breadcrumbs> <v-breadcrumbs :items="items" divider="."></v-breadcrumbs>
    </div>
  </v-app>
</template>
<script>
export default {
  name: 'App',
  data: () => ({
    items: [
      {
        text: 'Home',
        disabled: false,
        href: 'breadcrumbs_home',
      },
      {
        text: 'Link 1',
        disabled: false,
        href: 'breadcrumbs_link_1',
      },
      {
        text: 'Link 2',
        disabled: true,
        href: 'breadcrumbs_link_2',
      },
    ],
  }),
};
</script>
```

![](img/d208aa2ae4cd8a8371abaa7a781cbe9a.png)

# 用美化来美化

使用 Vuetify 材料设计框架创建优雅 web 应用程序的完整指南。

![](img/ff271935eabc3e42d8f111285dca7821.png)

在这里 免费获得一份 [**。**](https://mailchi.mp/583226ee0d7b/beautify-with-vuetify)

# 大面包屑

我们可以通过将`large`属性设置为`true`来增加面包屑的字体大小。`large`将每个项目的`font-size`从默认的`14px`增加到`16px`。

```
<template>
  <v-app>
    <div>
      <v-breadcrumbs :items="items"></v-breadcrumbs> <v-breadcrumbs :items="items" large></v-breadcrumbs>
    </div>
  </v-app>
</template>
<script>
export default {
  name: 'App',
  data: () => ({
    items: [
      {
        text: 'Home',
        disabled: false,
        href: 'breadcrumbs_home',
      },
      {
        text: 'Link 1',
        disabled: false,
        href: 'breadcrumbs_link_1',
      },
      {
        text: 'Link 2',
        disabled: true,
        href: 'breadcrumbs_link_2',
      },
    ],
  }),
};
</script>
```

![](img/b15902349263c135f954dd9605c3b5df.png)

# 面包屑图标分隔线

我们可以使用`v-breadcrumbs`的`divider`槽在面包屑的每一项之间显示定制的 HTML。例如，我们可以使用[验证图标组件](https://codingbeautydev.com/blog/vuetify-icons/) ( `v-icon`)显示[材料设计图标](https://materialdesignicons.com/)中的任意[图标](https://codingbeautydev.com/blog/vuetify-icons/):

```
<template>
  <v-app>
    <div>
      <v-breadcrumbs :items="items">
        <template v-slot:divider>
          <v-icon>mdi-forward</v-icon>
        </template>
      </v-breadcrumbs> <v-breadcrumbs :items="items">
        <template v-slot:divider>
          <v-icon>mdi-chevron-right</v-icon>
        </template>
      </v-breadcrumbs>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    items: [
      {
        text: 'Home',
        disabled: false,
        href: 'breadcrumbs_home',
      },
      {
        text: 'Link 1',
        disabled: false,
        href: 'breadcrumbs_link_1',
      },
      {
        text: 'Link 2',
        disabled: true,
        href: 'breadcrumbs_link_2',
      },
    ],
  }),
};
</script>
```

![](img/6fe88950332dddd3631651044196c834.png)

# Vuetify 面包屑`item`槽

我们可以使用`v-breadcrumbs`的项目槽来定制每个面包屑。例如，这里我们为每个项目显示一个大写文本:

```
<template>
  <v-app>
    <div>
      <v-breadcrumbs :items="items">
        <template v-slot:item="{ item }">
          <v-breadcrumbs-item :href="item.href" :disabled="item.disabled">
            {{ item.text.toUpperCase() }}
          </v-breadcrumbs-item>
        </template>
      </v-breadcrumbs>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    items: [
      {
        text: 'Home',
        disabled: false,
        href: 'breadcrumbs_home',
      },
      {
        text: 'Link 1',
        disabled: false,
        href: 'breadcrumbs_link_1',
      },
      {
        text: 'Link 2',
        disabled: true,
        href: 'breadcrumbs_link_2',
      },
    ],
  }),
};
</script>
```

![](img/a0fdb5cf9c11560ee50ad8524a9bbebd.png)

# 结论

面包屑作为导航工具，帮助用户保持对他们在网站中的位置的了解。我们可以将 breadcrumbs 组件(`v-breadcrumbs`)虚拟化来创建面包屑。

*获得关于 Vuetify、Vue、JavaScript 等的每周提示和教程:【http://eepurl.com/hRfyJL】T5*

*更新于:*[*codingbeautydev.com*](https://codingbeautydev.com/blog/vuetify-breadcrumbs/)