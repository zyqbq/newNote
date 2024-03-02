### PBR材质

基于物理渲染

MeshStandardMaterial

MeshPhysicalMaterial

MesbPhysicalMaterial是MeshStandardMaterial扩展的子类,提供了更多功能属性。

### 网格模型材质整体回顾

![img](http://www.webgl3d.cn/imgthreejs/%E7%BD%91%E6%A0%BC%E6%9D%90%E8%B4%A8.svg)

- MeshLambertMaterial: **Lambert光照模型**(漫反射)
- MeshPhongMaterial：**Phong光照模型**(漫反射、高光反射)
- MeshStandardMaterial和MeshPhysicalMaterial：**基于物理的光照模型**(微平面理论、能量守恒、菲涅尔反射...)

PBR材质相比MeshLambertMaterial和MeshPhongMaterial可以提供更逼真的、更接近生活中的材质效果，当然也会`占用更多的电脑硬件资源`。

通过MeshPhysicalMaterial文档，提供的资源，可以查看多个PBR材质的案例效果，系统课程中轿车展示案例也会用到PBR材质。

### 渲染占用资源和表现能力

整体上来看，就是渲染表现能力越强，占用的计算机硬件资源更多。

- 占用渲染资源 MeshBasicMaterial < MeshLambertMaterial < MeshPhongMaterial < MeshStandardMaterial < MeshPhysicalMaterial
- 渲染表现能力 MeshBasicMaterial < MeshLambertMaterial < MeshPhongMaterial < MeshStandardMaterial < MeshPhysicalMaterial

### metalness金属度

MeshStandardMaterial的metalness表示材质像**金属**的程度, 非金属材料,如木材或石材,使用0.0,金属使用1.0

```javascript
new THREE.MeshStandardMaterial({
    metalness: 1.0,//金属度属性
})
//或
mesh.material.metalness = 1.0;//金属度
```

### 粗糙度roughness

越大越粗糙

地面比较粗糙，比如镜子表面就非常非常光滑

0.0表示平滑的镜面反射,1.0表示完全漫反射,默认0.5。

### 金属物体添加环境贴图envMap

```js
// 加载环境贴图
// 加载周围环境6个方向贴图
// 上下左右前后6张贴图构成一个立方体空间
// 'px.jpg', 'nx.jpg'：x轴正方向、负方向贴图  p:正positive  n:负negative
// 'py.jpg', 'ny.jpg'：y轴贴图
// 'pz.jpg', 'nz.jpg'：z轴贴图
const textureCube = new THREE.CubeTextureLoader()
    .setPath('./环境贴图/环境贴图0/')
    .load(['px.jpg', 'nx.jpg', 'py.jpg', 'ny.jpg', 'pz.jpg', 'nz.jpg']);
    // CubeTexture表示立方体纹理对象，父类是纹理对象Texture 
```

```js
new THREE.MeshStandardMaterial({
    metalness: 1.0,
    roughness: 0.5,
    envMap: textureCube, //设置pbr材质环境贴图
})    
obj.material.envMap = textureCube; //设置环境贴图 
```

### 环境贴图反射率.envMapIntensity

环境贴图对模型表面的影响能力

```js
//默认值1, 设置为0.0,相当于没有环境贴图
obj.material.envMapIntensity = 1.0;
```

环境贴图类似有光源的效果

### 场景环境属性.environment

能影响所有的网格模型

```js
// 环境贴图纹理对象textureCube作为.environment属性值,影响所有模型
scene.environment = textureCube;
```

### 环境贴图色彩空间编码encoding

```js
//如果renderer.outputEncoding=THREE.sRGBEncoding;环境贴图需要保持一致
textureCube.encoding = THREE.sRGBEncoding;  
```

# MeshPhysicalMaterial

物理网格材质

### 清漆层clearcoat

越大漆越重

范围0到1，默认0。

模拟物体表面一层透明图层

### 清漆层粗糙度.clearcoatRoughness

物体表面透明涂层`.clearcoat`对应的的粗糙度

范围是为0.0至1.0。默认值为0.0

值越大越粗糙

```js
const material = new THREE.MeshPhysicalMaterial( {
	clearcoat: 1.0,//物体表面清漆层或者说透明涂层的厚度
	clearcoatRoughness: 0.1,//透明涂层表面的粗糙度
} );

```

### 汽车材质

```js
mesh.material = new THREE.MeshPhysicalMaterial({
        color: mesh.material.color, //默认颜色
        // color: 0x222222,//换一种颜色
        metalness: 0.9,//车外壳金属度
        roughness: 0.5,//车外壳粗糙度
        clearcoat: 1, //清漆层
        clearcoatRoughness: 0.01, //清漆层粗糙度
        envMap: textureCube, //环境贴图
        envMapIntensity: 2.5, //环境贴图对Mesh表面影响程度
    })
```

### 物理材质透光率.transmission

更好的模拟玻璃、半透明塑料一类的视觉效果 代替Mesh普通透明度属性`.opacity`

从0.0到1.0。默认值为0.0

### 折射率`.ior`

非金属材料的折射率从1.0到2.333。默认值为1.5

不同材质的折射率，你可以百度搜索

### 玻璃材质

```js
   mesh.material = new THREE.MeshPhysicalMaterial({
        metalness: 0.0,//玻璃非金属 
        roughness: 0.0,//玻璃表面光滑
        envMap:textureCube,//环境贴图
        envMapIntensity: 1.0, //环境贴图对Mesh表面影响程度
        transmission: 1.0, //玻璃材质透光率，transmission替代opacity 
        ior:1.5,//折射率
    })
```

### 三维软件导出的材质

设置环境贴图即可

```js
mesh1.material.envMap = textureCube; //环境贴图
mesh1.material.envMapIntensity = 1.0; //环境贴图对Mesh表面影响程度
```

