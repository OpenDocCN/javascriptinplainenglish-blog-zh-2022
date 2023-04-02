# 动态获取 Three.js 场景中的对象位置

> 原文：<https://javascript.plainenglish.io/get-object-position-in-a-three-js-scene-dynamically-fcc355edfbad?source=collection_archive---------11----------------------->

## 如何在一个 Three.js 场景中动态获取物体位置的指南。

![](img/af24949cc516f38ef7b59e4227799a31.png)

我是新来的 [Three.js](https://threejs.org/) 。

我有一个场景，其中有一个对象，我们可以使用 [TransformControls.js](https://github.com/mrdoob/three.js/blob/master/examples/js/controls/TransformControls.js) 在场景的所有 X、Y 和 Z 轴上移动。

当我使用鼠标点击并拖动任一轴(即 X、Y 和 Z)在场景内平移/移动对象时。我想获得场景中特定对象的更新后的 X、Y 和 Z 位置坐标。

在渲染场景之前，我使用`mesh.position.set( 0, 0, 0 );`来设置对象的位置，但是我不知道如何在场景中获得对象的动态位置。

最后，我希望在转换操作后保存更新的位置坐标，并在用户返回页面或进行页面刷新时，使用更新的位置坐标重新呈现对象所在的场景。

任何指点都会很有帮助。

## **解决方案**

`THREE.TransformControls`需要几步才能使用。

1.  创造你的三个。TransformControls 对象
2.  将其添加到您的场景中
3.  将其附加到要操纵的对象上

```
var xformControl = new THREE.TransformControls(camera, renderer.domElement);
scene.add(xformControls);
// assuming you add "myObj" to your scene...
xformControl.attach(myObj);
// and then later...
xformControl.detatch();
```

将控件附加到对象会将操纵“gizmo”插入到场景中。拖动 gizmo 的各个部分将执行不同类型的变换。当你用小控件变换完零件后，检查`mesh.position`应该会反映出新的位置。

## **为清晰起见，附加信息:**

对象的位置将不会更新，直到您使用“gizmo”来移动它。举个例子，

1.  您的对象位于场景中的(10，10，10)
2.  `xformControl.attach(yourObject)`
3.  “gizmo”在(10，10，10)处创建
4.  你的对象保持在(10，10，10)
5.  使用“gizmo”在+Y 方向平移对象
6.  您的对象现在将有一个更新的位置
7.  `console.log(yourObject.position.y > 10); // true`

现在你知道了。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*