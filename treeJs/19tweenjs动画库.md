### npm安装

在工程化开发的时候可以通过npm命令行安装tween.js模块。

```javascript
npm i @tweenjs/tween.js@^18
import TWEEN from '@tweenjs/tween.js';
```

###  tweenjs基本语法

```javascript
const pos = {x: 0,y: 0};
//传入一个对象
const tween = new TWEEN.Tween(pos);//创建一段tween动画
//经过2000毫秒，pos对象的x和y属性分别从零变化为100、50
to的参数一是对象，2是时间-ms
tween.to({x: 100,y: 50}, 2000);

//tween动画开始执行
tween.start();

function loop() {
    TWEEN.update();//tween更新
    requestAnimationFrame(loop);
}
```

### tweenjs改变threejs模型对象位置

```javascript
//创建一段mesh平移的动画
const tween = new TWEEN.Tween(mesh.position);
//经过2000毫秒，pos对象的x和y属性分别从零变化为100、50
tween.to({x: 100,y: 50}, 2000);
//tween动画开始执行
tween.start(); 

// 渲染循环
function render() {
    TWEEN.update();
    renderer.render(scene, camera);
    requestAnimationFrame(render);
}
render();
```

简写

```javascript
const tween = new TWEEN.Tween(mesh.position).to({x: 100,y: 50}, 2000).start();
```

### 相机运动

- `onStart`：动画开始执行触发
- `onUpdate`：动画执行过程中，一直被调用执行
- `onComplete`：动画正常执行完触发

```javascript
camera.position.set(202, 123, 125);
camera.lookAt(0, 0, 0);
new TWEEN.Tween(camera.position)
.to({x: 202,y: 123,z: -350}, 3000)
// tweenjs改变参数对象的过程中，.onUpdate方法会被重复调用执行
.onUpdate(function(){
    camera.lookAt(0, 0, 0);
})
.start()
```

相机圆周运动

```javascript
const R = 100; //相机圆周运动的半径
new TWEEN.Tween({angle:0})
.to({angle: Math.PI*2}, 16000)
.onUpdate(function(obj){
    camera.position.x = R * Math.cos(obj.angle);
    camera.position.z = R * Math.sin(obj.angle);
    camera.lookAt(0, 0, 0);
})
.start()
```

### 相机靠近观察

```javascript
const A = model.getObjectByName('设备A标注');
const pos = new THREE.Vector3();
//获取三维场景中某个对象世界坐标
A.getWorldPosition(pos);

// 向量的x、y、z坐标分别在pos基础上增加30
const pos2 = pos.clone().addScalar(30);
```

```javascript
// 切换到设备A预览状态
document.getElementById('A').addEventListener('click', function () {
    const A = model.getObjectByName('设备A标注');
    const pos = new THREE.Vector3();
    A.getWorldPosition(pos); //获取三维场景中某个对象世界坐标
    // 相机飞行到的位置和观察目标拉开一定的距离
    const pos2 = pos.clone().addScalar(30);//向量的x、y、z坐标分别在pos基础上增加30
    // 相机从当前位置camera.position飞行三维场景中某个世界坐标附近
    new TWEEN.Tween({
            // 相机开始坐标
            x: camera.position.x,
            y: camera.position.y,
            z: camera.position.z,
            // 相机开始指向的目标观察点
            tx: 0,
            ty: 0,
            tz: 0,
        })
        .to({
            // 相机结束坐标
            x: pos2.x,
            y: pos2.y,
            z: pos2.z,
            // 相机结束指向的目标观察点
            tx: pos.x,
            ty: pos.y,
            tz: pos.z,
        }, 2000)
        .onUpdate(function (obj) {
            // 动态改变相机位置
            camera.position.set(obj.x, obj.y, obj.z);
            // 动态计算相机视线
            camera.lookAt(obj.tx, obj.ty, obj.tz);
        })
  	  .onComplete(function(obj){
  		  controls.target.set(obj.tx, obj.ty, obj.tz);
   		    controls.update();
	})
        .start();
})
```

### 缓动函数

```javascript
// 动画开始缓动方式(类比加速启动)
tween.easing(TWEEN.Easing.Sinusoidal.In);
// 动画结束缓动方式(类比减速刹车)
tween.easing(TWEEN.Easing.Sinusoidal.Out);
// 同时设置In和Out
tween.easing(TWEEN.Easing.Sinusoidal.InOut);
```