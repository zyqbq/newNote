### 背景透明和背景颜色

```js
renderer.setClearAlpha(0.0);
或
renderer.setClearColor(0xb9d3ff, 0.4); //设置背景颜色和透明度
// 在构造函数参数中设置alpha属性的值
var renderer = new THREE.WebGLRenderer({
  alpha: true
});
```

### 下载文件

```js
<button type="button" name="button" onclick="saveFile()">下载</button>
<script>
  function saveFile() {
    // 创建一个超链接元素，用来下载保存数据的文件
    const link = document.createElement('a');
    // 通过超链接herf属性，设置要保存到文件中的数据
    link.href = window.URL.createObjectURL(new Blob(['一些数据']));
    link.download = '文件名称.txt';//下载文件名
    link.click();//js代码触发超链接元素a的鼠标点击事件，开始下载文件到本地
  }
</script>
```

### canvas保存为图片

```js
// WebGL渲染器设置
const renderer = new THREE.WebGLRenderer({
    //想把canvas画布上内容下载到本地，需要设置为true
    preserveDrawingBuffer:true,
});
```

Canvas画布通过`.toDataURL()`方法可以获取画布上的像素信息。`canvas.toDataURL("image/png");`表示以png格式获取像素数据，可以直接赋值给超链接元素a的`.herf`属性下载到本地。

```js
// 鼠标单击id为download的HTML元素，threejs渲染结果以图片形式下载到本地
document.getElementById('download').addEventListener('click',function(){
    // 创建一个超链接元素，用来下载保存数据的文件
    const link = document.createElement('a');
    // 通过超链接herf属性，设置要保存到文件中的数据
    const canvas = renderer.domElement; //获取canvas对象
    link.href = canvas.toDataURL("image/png");
    link.download = 'threejs.png'; //下载文件名
    link.click(); //js代码触发超链接元素a的鼠标点击事件，开始下载文件到本地
})

```

以不同的格式获取像素信息

```javascript
canvas.toDataURL("image/png");
canvas.toDataURL("image/jpeg");
canvas.toDataURL("image/bmp");
```

### 距离过近造成的深度冲突

相机位置过远

两个面距离过近

```js
// WebGL渲染器设置
const renderer = new THREE.WebGLRenderer({
    // 设置对数深度缓冲区，优化深度冲突问题
    就是两个面间距比较小的时候，让threejs更容易区分两个面，谁在前，谁在后。
    logarithmicDepthBuffer: true
});
```

### 加载进度8.7

```js
const percentDiv = document.getElementById("per"); // 获取进度条元素
loader.load("../工厂.glb", function (gltf) {
    model.add(gltf.scene);
    // 加载完成，隐藏进度条
    // document.getElementById("container").style.visibility ='hidden';
    document.getElementById("container").style.display = 'none';
}, function (xhr) {
    // 控制台查看加载进度xhr
    // 通过加载进度xhr可以控制前端进度条进度   
    const percent = xhr.loaded / xhr.total;
    console.log('加载进度' + percent);
     
   
    percentDiv.style.width = percent * 400 + "px"; //进度条元素长度
    percentDiv.style.textIndent = percent * 400 + 5 + "px"; //缩进元素中的首行文本
    // Math.floor:小数加载进度取整
    percentDiv.innerHTML = Math.floor(percent * 100) + '%'; //进度百分比
})
```

