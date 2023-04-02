# 如何用 Vuetify 创建滑块

> 原文：<https://javascript.plainenglish.io/vuetify-slider-7010a3c21b4?source=collection_archive---------18----------------------->

![](img/533391afcb65708b82371ea498a26094.png)

滑块是从一系列值中获取用户输入的好方法。有用于各种功能，如调整显示器的亮度或调节扬声器音量。在这篇文章中，我们将探索用 Vuetify 创建和定制滑块的各种方法。

# 垂直滑块组件

Vuetify 提供了用于创建滑块的`v-slider`组件:

```
<template>
  <v-app>
    <v-row justify="center" class="mt-2">
      <v-col sm="6">
        <v-slider></v-slider>
      </v-col>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/1818ce9a19cc4f60a636762577084562.png)

基本滑块由轨道(长线)和拇指(圆圈)组成。单击轨道上的某个位置会将滑块移动到该位置:

![](img/a1ddee04287c0cac8515e5b3efc2b0f6.png)

# 滑块标签

为了向用户描述我们的滑块，我们可以用`label`属性指定一个标签:

```
<template>
  <v-app>
    <v-row justify="center" class="mt-2">
      <v-col sm="6">
        <v-slider label="Slider"></v-slider>
      </v-col>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/f109c38b58b8583944475c8b151520b3.png)

# 滑块提示

我们可以用`hint`道具显示滑块的提示。

```
<template>
  <v-app>
    <v-row justify="center" class="mt-2">
      <v-col sm="6">
        <v-slider label="Slider" hint="hint"></v-slider>
      </v-col>
    </v-row>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

当您点按拇指时，会显示提示:

![](img/84004f718121fe9e1e1e65ad81df333b.png)

# 使用 v-model 的双向绑定

我们可以使用`v-model`在滑块值和变量之间创建一个双向绑定。

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider label="Slider" hint="hint" v-model="sliderValue"></v-slider>
      </v-col>
    </div>
    <div class="d-flex justify-center">
      <v-col sm="6">Slider value: {{ sliderValue }}</v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

在上面的代码中，我们添加了一些文本来显示滑块的当前值(由`sliderValue`决定):

![](img/a8d146fc5c87885671bd60e4876d0ff1.png)

当滑块接收到输入时`sliderValue`被更新，文本反映了这一点:

![](img/1977fd69973fc48e1e32c55f8de2d862.png)

让我们添加一个【复位】按钮:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider label="Slider" hint="hint" v-model="sliderValue"></v-slider>
      </v-col>
    </div>
    <div class="d-flex justify-center">
      <v-col sm="6">Slider value: {{ sliderValue }}</v-col>
    </div>
    <div class="d-flex justify-center">
      <v-col sm="6"
        ><v-btn color="primary" @click="sliderValue = 0"
          >Reset slider</v-btn
        ></v-col
      >
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

![](img/eeea0118debe9ef7c93a8980691f7041.png)

我们为按钮[添加了一个点击处理程序，当点击按钮](https://codingbeautydev.com/blog/vuetify-buttons/)时，它会将`sliderValue`设置为 0:

![](img/ce337496adc8e5e80bcb823411a62acd.png)

# 用美化来美化

使用 Vuetify 材料设计框架创建优雅 web 应用程序的完整指南。

![](img/ff271935eabc3e42d8f111285dca7821.png)

点击这里下载你的免费版本[！](https://mailchi.mp/583226ee0d7b/beautify-with-vuetify)

# 滑块最小值和最大值

Vuetify 滑块的默认最小值和最大值分别为 0 和 100。我们可以用`min`和`max`道具把它们换成别的东西:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider
          label="Slider"
          hint="hint"
          v-model="sliderValue"
          min="20"
          max="60"
        ></v-slider>
      </v-col>
    </div>
    <div class="d-flex justify-center">
      <v-col sm="6">Slider value: {{ sliderValue }}</v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: null,
  }),
};
</script>
```

现在滑块的最小值是 20:

![](img/bfe4639952b2365a6c1550fcdfd61324.png)

最大值现在是 60:

![](img/281630cc12120d21ceca4f244cc6dcfc.png)

# 滑块自定义颜色

v- `slider`自带道具，允许我们修改其各种元素的[颜色](https://codingbeautydev.com/blog/vuetify-colors/)。

使用`color`道具改变拇指前轨道部分的[颜色](https://codingbeautydev.com/blog/vuetify-colors/):

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider label="color" v-model="sliderValue" color="green"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

![](img/159d4a928d66f0091a8be1afe323380a.png)

`track-color`道具会修改拇指后部分轨迹的[颜色](https://codingbeautydev.com/blog/vuetify-colors/):

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider
          label="track-color"
          v-model="sliderValue"
          track-color="red"
        ></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

![](img/d18685b61f0e49fe6ac3d4ba873f4df8.png)

要改变拇指的[颜色](https://codingbeautydev.com/blog/vuetify-colors/)，使用`thumb-color`道具:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider
          label="thumb-color"
          v-model="sliderValue"
          thumb-color="orange"
          thumb-label="always"
        ></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

![](img/c72929a6808c982ba69dc28d1348069b.png)

# 禁用的滑块

将`disabled`道具设置为`true`，关闭与滑块的交互:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider disabled value="50" label="Disabled"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/7ee3a27fac4bdf42f6a6272d3e2c3f8f.png)

# 离散滑块

默认情况下，Vuetify 滑块的步长值为 1。这些类型的滑块被称为连续滑块，因为滑块从其最小值平滑地移动到最大值。在我们需要较低精度的情况下，我们可以使用`step`道具增加该步长值:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-10">
      <v-col sm="6">
        <v-slider
          v-model="sliderValue"
          step="10"
          thumb-label="always"
        ></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    sliderValue: 0,
  }),
};
</script>
```

![](img/5b857ddd3c9cd0a2c8748176ff90a802.png)

# 滑块图标

`v-slider`提供了显示图标[和滑块](https://codingbeautydev.com/blog/vuetify-icons/)的道具，有助于添加更多的上下文。

`prepend-icon`道具会在滑块前显示相应的图标:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider v-model="volume" prepend-icon="mdi-volume-high"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    volume: 0,
  }),
};
</script>
```

![](img/54bb0dfc0d994ddfc14105244c6ad3a7.png)

`append-icon`将在滑块后显示图标:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider v-model="volume" append-icon="mdi-volume-high"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    volume: 0,
  }),
};
</script>
```

![](img/5b754aebebcbfc7631220aab311b8d53.png)

# 只读滑块

只读滑块也像禁用滑块一样阻止交互，但是它们不会失去它们的[颜色](https://codingbeautydev.com/blog/vuetify-colors/):

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider readonly value="30" label="Readonly"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/866e2cf2286a0c0213f4486b479b5b00.png)

# 反向标签

要在滑块末端显示滑块标签，使用`inverse-label`道具:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider label="Inverse label" inverse-label></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
};
</script>
```

![](img/4418679f9a62fdf23b1982e96d902a8d.png)

# 滑块拇指

`v-slider`为自定义拇指的行为和显示提供了某些支持。将`thumb-label`旋钮设置为`true`显示，以便在使用滑块时仅显示缩略图:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-10">
      <v-col sm="6">
        <v-slider v-model="value" label="Slider" thumb-label></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/e41e52e0a475a08e710e496101b2d9a7.png)

无论用户是否使用滑块，要始终显示缩略图，请将`thumb-label`按钮设置为`always`:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-10">
      <v-col sm="6">
        <v-slider v-model="value" label="Slider" thumb-label="always"></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/81d5e8122b7ec9eec6bd3d114a8ceec9.png)

## 自定义拇指大小

`thumb-size`道具让我们修改拇指大小:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-16">
      <v-col sm="6">
        <v-slider
          v-model="value"
          label="Slider"
          thumb-label="always"
          thumb-size="50"
        ></v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/173c325093d867e1c9f521d939fce924.png)

## 自定义缩略图标签

thumb 通常显示滑块的当前数值，但是我们通过向`v-slider`的`thumb-label`槽提供一个元素来改变它所显示的内容:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-16">
      <v-col sm="6">
        <v-slider
          v-model="value"
          label="Volume"
          thumb-label="always"
          thumb-size="50"
        >
          <template v-slot:thumb-label>
            <v-icon dark>mdi-volume-high</v-icon>
          </template>
        </v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/828308f4f7194a3f3b2c1a9e8425c515.png)

# 滑块刻度

刻度直观地表示用户可以将滑块移动到的值。将`ticks`杆设置为`true`只会在使用滑块时显示滑块:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider v-model="value" step="10" ticks> </v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/d3014cbceeeed41f21c92384def742c3.png)

将`ticks`设置为`always`使刻度一直显示:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider v-model="value" step="10" ticks="always"> </v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/7d9c0bbd603f9a3be898789fa4c827b0.png)

## 自定义刻度大小

我们还可以使用`tick-size`道具自定义刻度大小:

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="6">
        <v-slider v-model="value" step="10" ticks="always" tick-size="4">
        </v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
  }),
};
</script>
```

![](img/935abb6d7ff72f1c2a7a34b68cd06914.png)

# 刻度标签

我们可以添加文字来描述记号。为此，将`tick-labels`属性设置为一个字符串数组。

```
<template>
  <v-app>
    <div class="d-flex justify-center mt-2">
      <v-col sm="12">
        <v-slider
          v-model="value"
          step="10"
          ticks="always"
          :tick-labels="tickLabels"
        >
        </v-slider>
      </v-col>
    </div>
  </v-app>
</template><script>
export default {
  name: 'App',
  data: () => ({
    value: 0,
    tickLabels: ['Terrible!', 'Bad', 'Okay', 'Good', 'Excellent!'],
  }),
};
</script>
```

数组中的每一项都将被分配给一个分笔成交点:

![](img/0fc1d12d426d29ef61332658d4da57a0.png)

# 摘要

Vuetify 提供了`v-slider`组件来创建滑块。我们可以使用它的道具来定制其行为和外观的各个方面。

[*注册*](http://eepurl.com/hRfyJL) *订阅我们的每周简讯，了解 Vuetify 和 Vue 的最新提示和教程。*

*在*[*codingbeautydev.com*](https://codingbeautydev.com/blog/vuetify-slider/)*获取更新文章。*