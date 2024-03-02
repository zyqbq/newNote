### 6setup 

setup() :开始创建组件之前，在beforeCreate和created之前执行

![image-20231107221926841](img/image-20231107221926841.png)

### ref和reactive的使用

引入

![image-20231107222351879](img/image-20231107222351879.png)

reactive

用来定义复杂类型数据

![image-20231107222206764](img/image-20231107222206764.png)



ref(更加常用)

定义简单类型数据

![image-20231107222425279](img/image-20231107222425279.png)

在js中使用

![image-20231107222537379](img/image-20231107222537379.png)

模板中使用,不用加.value

![image-20231107222720305](img/image-20231107222720305.png)

ref是浅层解包



两个使用场景

reactive：1.应用于本地数据2.多个数据间是有联系的

ref:网络数据,本地简单数据

![image-20231107223208294](img/image-20231107223208294.png)

### readonly 

单向数据流：父组件传递给子组件的内容不能在子组件中直接修改

子组件如果想修改父组件的数据推荐使用emit触发事件，让父组件修改自己的数据

![image-20240116182225864](img/image-20240116182225864.png)

普通对象，reactive和ref数据都可以用

readonly包裹的内容修改也是具有响应式的

用readonly在父组件中包裹数据再传递出去就避免了被修改

![image-20231110172828734](img/image-20231110172828734.png)

### isProxy

判断是否是proxy对象

用法

```js
	isProxy(info)->true
```

### isReactive

判断是不是由reactive返回的数据

readonly包裹reactive的数据也会返回true

### toRaw

返回readonly和reactive的原始数据

### toRefs和toRef

解构响应式数据

toRefs解构reactive的多个数据

toRef解构reactive的单个数据

![image-20231110174538136](img/image-20231110174538136.png)

### unRef方法

如果参数是ref,返回其.value值

如果参数不是ref,就返回这个参数

用法:

unRef(参数)

![image-20240116222416702](img/image-20240116222416702.png)

### isRef

判断是否是ref对象

isRef(要判断的值)

### shallowRef

创建浅层的ref响应数据

用法:

```js
 const info=shallowRef({name:"zjx"})
 info.value.name修改不具有响应式
```

### triggerRef

让shallowRef在没有响应式的情况下,手动去触发响应式

![image-20240116223639869](img/image-20240116223639869.png)

### computed

setup中的计算属性写法

使用

![image-20240117063027447](img/image-20240117063027447.png)

set和get

![image-20240117064328668](img/image-20240117064328668.png)

修改computed的值

![image-20240117064417281](img/image-20240117064417281.png)

### ref获取dom或组件

获取dom

.value值就是dom

![image-20240117065349057](img/image-20240117065349057.png)

获取子组件

![image-20240117065546304](img/image-20240117065546304.png)

### 生命周期

vue2和vue3对照

![image-20240117070105627](img/image-20240117070105627.png)

### provide

![image-20240117070741770](img/image-20240117070741770.png)

![image-20240117071107769](img/image-20240117071107769.png)

### watch

可以侦听props和data中的数据

侦听简单数据

![image-20240117161123634](img/image-20240117161123634.png)

侦听复杂数据

![image-20240117161317487](img/image-20240117161317487.png)

proxy数据转普通对象侦听

![image-20240117161533163](img/image-20240117161533163.png)

### watchEffect

Effect作用

默认会执行一次编写的代码

代码中的数据发生变化就会再次执行(自动收集依赖)

![image-20240117162651953](img/image-20240117162651953.png)

### hooks

回调函数,钩子

### 修改html标题在vue中

document.title=''

### setup语法糖

组件不用再注册

![image-20240117175221447](img/image-20240117175221447.png)

顶层编写的内容不再需要返回

定义响应式数据

![image-20240117175557000](img/image-20240117175557000.png)

script更推荐放在顶部 

父传子

![image-20240117180011781](img/image-20240117180011781.png)

子传父

![image-20240117180325227](img/image-20240117180325227.png)

用ref使用子组件内的方法

![image-20240117180907412](img/image-20240117180907412.png)