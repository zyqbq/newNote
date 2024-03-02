# 着色器——uniform

使用着色器语言GLSL编写着色器代码的时候，都会使用关键字`attribute`和`uniform`来声明一些变量，通常关键字`attribute`用来声明一些几何体顶点数据，例如顶点位置数据、顶点法向量数据....，`uniform`关键字通常用来声明模型矩阵、光源颜色、光源位置等变量。

- `attribute`：属性
- `uniform`：统一

Three.js渲染器渲染场景的时候，几何体的顶点位置、颜色、法向量等数据，系统会自动传递给着色器中`attribute`关键字声明的对应顶点变量。

着色器中`uniform`关键字声明的模型矩阵`modelMatrix`、视图矩阵`viewMatrix`、投影矩阵`projectionMatrix`等Three.js系统定义的uniform变量，Threejs系统会自动从对应的Threejs对象中解析数据并自动传递。比如视图矩阵的值Three.js系统会从相机对象中获得具体的值，然后传递给`viewMatrix`变量。

### 自定义`uniform`变量数据传递

如果程序员在着色器中任意命名自定义了一个uniform变量,如果需要给该uniform变量传递数据，在原生WebGL中需要特定的WebGL API来传递数据，在Three.js中不需要这样，只需要在着色器材质对象的`ShaderMaterial`的属性`.uniforms`中定义一个属性，属性名字和着色器中uniform变量保持一致，对于程序员而言只需要保持名字一致，至于数据传递过程，Three.js系统会自动帮你完成。

## 属性`.uniforms`使用案例

片元着色器中通过uniform关键字声明了一个颜色变量color，为了给该变量传递数据在ShaderMaterial对象的uniforms属性中定义了一个名为color的属性，按照Three.js系统uniform变量数据自动传递的机制，如果你在着色器代码中自定义声明了多个uniform变量，只要名字和ShaderMaterial对象中uniform数据的名字保持一直就可以正确完成数据传递。

```JavaScript
<!-- 片元着色器 -->
<script id="fragmentShader" type="x-shader/x-fragment">
  // color变量数据来自ShaderMaterial的uniforms属性的color属性
  uniform vec3 color;
  void main() {
 // gl_FragColor = vec4(1.0,0.0,0.0,1.0);
 gl_FragColor = vec4(color,1.0);
  }
</script>
```

ShaderMaterial的uniforms属性代码

```JavaScript
var material = new THREE.ShaderMaterial({
  //定义uniforms属性，uniforms的属性和着色器中的uniform变量相对应
  uniforms:{
// 颜色属性clor对应片元着色器代码中uniform声明的color变量                                
color:{value:new THREE.Color(0xff0000)}
  },
  // 顶点着色器
  vertexShader: document.getElementById('vertexShader').textContent,
  // 片元着色器
  fragmentShader: document.getElementById('fragmentShader').textContent,
});
```

### 数据类型

着色器声明的uniform变量数据类型要和着色器材质对象的`ShaderMaterial`的属性`.uniforms`的属性的属性值数据类型保持一致。例如`value:new THREE.Color(0xff0000)`对应的着色器中数据类型是`vec3`,`value:new THREE.Matrix4()`对应的着色器中数据类型是`mat4`。

`value`的值和和着色器数据类型的对应关系可以参考Threejs文档core分类下的[Uniform](http://www.yanhuangxueyuan.com/threejs/docs/index.html#api/core/Uniform)