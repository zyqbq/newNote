### 坐标辅助器

```js
const axesHelper = new THREE.AxesHelper(5):
scene.add (axesHelper);
```

### 轨道控制器

![image-20240228140448897](img/image-20240228140448897.png)

![image-20240228140458417](img/image-20240228140458417.png)

### 物体位移

```js
cube.position.x = 2;
cube.position.set(3, 0, 0);
```

### 缩放

```js
cube.scale.set(2,2, 2);
```

### 旋转

旋转会改变欧拉角的值,并且自身的坐标系会跟随旋转

```js
cube.rotation.x = Math.PI / 4:
```

### 父子模型的关系

> 父元素的旋转缩放平移都会带动子元素一起变化

### 画布大小自适应

```js
// 监听窗口变化
window.addEventListener("resize"，0 =>{
// 重置染器宽高比
renderer.setSize(window.innerWidth, window.innerHeight).
// 重置相机宽高比
camera.aspect = window.innerWidth / window.innerHeight
// 更新相机投影矩阵
camera.updateProjectionMatrix();
});
```

### 全屏和退出全屏

```js
document.body.requestFullscreen0://全屏
document.exitFullscreen0;// 退出全屏
```

### gui使用

```js
// 导入lil.gui
import { GUl ) from "three/examples/jsm/libs/lil-qui.module.min.is";
```

使用方法

> 如果属性值是布尔值,就是勾选框
> gui.add(对象,属性).min(最小值).max(最大值).step(每步变化
> 值).name("这个滑块名称").onChange((val) => [
> 每次值变化执行打印这个值
> console.log(val);
> ).onFinishChange((val) => (
> 值拖动完才打印
> console.log("立方体y轴位置"，val);
> 1)

全屏和退出全屏按钮



```js
let eventObj = {
	Fullscreen: function (){
	// 全屏
	document.body.requestFullscreen()
	console.log("全屏");
},
ExitFullscreen: function (){
	document.exitFullscreen();
	console.log("退出全屏")
	},
 }:
// 创建GUI
const gui = new GUl():
// 添加按钮
gui.add(eventObj"Fullscreen").name("全屏")
gui.add(eventObj,"ExitFullscreen").name("退出全屏");
```

范围滑块

```js
gui.add(cube.position,"x"，-5,5).name("立方体x轴位置");
```

折叠块

![image-20240228141408412](img/image-20240228141408412.png)

颜色

![image-20240228141431365](img/image-20240228141431365.png)

勾选框

线框模式

![image-20240228141459461](img/image-20240228141459461.png)

![image-20240228141508472](img/image-20240228141508472.png)

### 自定义创建三角形

逆时针为正面

![image-20240228141533729](img/image-20240228141533729.png)

![image-20240228141545590](img/image-20240228141545590.png)

### 使用索引绘制2个三角形

通过索引设置点的顺序

![image-20240228141607257](img/image-20240228141607257.png)

给一个物体的两个平面分别设置不同材质

![image-20240228141636869](img/image-20240228141636869.png)

给立方体每个面设置不同材质

![image-20240228141652709](img/image-20240228141652709.png)

## 材质

### 图片等资源访问

public的资源使用./访问

![image-20240228141923112](img/image-20240228141923112.png)

### 基础网格材质

不受光照影响

性能最好

### 标准网格材质

需要光照才会显示对应颜色

## 贴图

### 普通贴图

![image-20240228142101851](img/image-20240228142101851.png)

### 透明贴图

黑色是完全透明(物体可以直接看见后面的物体)
白色是完全不透明(物体完好显示)

![image-20240228142127913](img/image-20240228142127913.png)

### 环境贴图

物体会反射贴图中的画面

hdr需要设置球形映射,否者就作为平面背景

![image-20240228142336963](img/image-20240228142336963.png)

![image-20240228142346993](img/image-20240228142346993.png)

### 高光贴图

白色对应高光区域

黑色对应粗糙区域

![image-20240228142428610](img/image-20240228142428610.png)

### 光照贴图

窗户贴纸一样的光照贴图

![image-20240228142449712](img/image-20240228142449712.png)

### 环境光遮蔽贴图

黑色缝隙等光照不到的地方会变黑

![image-20240228142514545](img/image-20240228142514545.png)

![image-20240228142527539](img/image-20240228142527539.png)

### 色彩空间

![image-20240228142548178](img/image-20240228142548178.png)

THREE.SRGBColorSpace

提供了更多的颜色级别

按人眼强度计算

THREE.LinearSRGColorSpace(默认)

进行计算和处理时，可以提供更精确的结果,可能使颜色在暗区看着很暗

按光照强度来计算

THREE.NoColorSpace按线性空间设置

用于已经处于颜色空间中的纹理



更新纹理

中途需要更新纹理空间时需要调用

![image-20240228142758653](img/image-20240228142758653.png)

### 雾

线性雾会比较均匀

指数雾会突然变浓

![image-20240228142833526](img/image-20240228142833526.png)

### gltf加载

glb是二进制格式

gltf是json格式

![image-20240228142902478](img/image-20240228142902478.png)

![image-20240228142911147](img/image-20240228142911147.png)

通过环境贴图给物体上色

标准网格材质也能上色

![image-20240228142936594](img/image-20240228142936594.png)

### draco压缩

![image-20240228143000506](img/image-20240228143000506.png)

![image-20240228143014423](img/image-20240228143014423.png)

![image-20240228143026065](img/image-20240228143026065.png)

### group

group对象是继承object3D对象的

### 射线拾取

射线拾取的第一个物体就是距离最近的物体

![image-20240228143200621](img/image-20240228143200621.png)

### tween

补间动画

![image-20240228143221841](img/image-20240228143221841.png)

![image-20240228143230519](img/image-20240228143230519.png)

缓动网站：https://tweenjs.github.io/tween.js/examples/03_graphs.html

![image-20240228143340847](img/image-20240228143340847.png)

![image-20240228143356308](img/image-20240228143356308.png)



