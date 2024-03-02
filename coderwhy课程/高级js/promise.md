### es5之前处理异步的代码

![image-20230813153640191](../../../assests/image-20230813153640191.png)

### promise基本代码结果

resolve多次调用只相当于调用了一次

resolve和reject都调用了，只有前面的生效，因为状态确定下来就不能再改变了

![image-20230813155758917](../../../assests/image-20230813155758917.png)

### promise的三种状态

pending待定状态

fulfilled成功态或resolved

rejected失败态

### Executor

promise中会`立即执行`的回调函数

![image-20230813170454822](../../../assests/image-20230813170454822.png)

### 了解部分

resolve中传入promise

![image-20230813171427417](../../../assests/image-20230813171427417.png)

## then方法

### 多次调用

![image-20230813172009378](../../../assests/image-20230813172009378.png)

### uncatch报错

多次调用catch也都会执行 7

![image-20230813172308436](../../../assests/image-20230813172308436.png)

### then方法的返回值

默认返回值

![image-20240218163854860](img/image-20240218163854860.png)

* 返回一个普通值

then方法的返回值`也是一个promise`

这个promise的决议结果由返回值决定

![image-20230813173904090](../../../assests/image-20230813173904090.png)

* 返回自定义的promise

![image-20230813174457772](../../../assests/image-20230813174457772.png)

* thenable

![image-20230813174820910](../../../assests/image-20230813174820910.png)

### catch

promise链式调用时reject，会就近执行catch

![image-20230813184501003](../../../assests/image-20230813184501003.png)

抛出异常会中断函数

![image-20230813185055409](../../../assests/image-20230813185055409.png)

### finally

es9新增        

不论是执行then还是执行catch，finally中的回调函数`都会执行 `   

![image-20230813185935651](../../../assests/image-20230813185935651.png)

## 类方法

### resolve

相当于new Promise并且立即执行resolve

![image-20230813230306980](../../../assests/image-20230813230306980.png)

### reject方法

相当于new Promise并且立即执行reject

![image-20230813230649525](../../../assests/image-20230813230649525.png)

### all方法

多个promise一起等待结果，只有`都resolve`才执行.then()

并传递数据到一个数组中

如果有一个reject了，就会执行catch()

使用场景，当要获得多个网络请求时可以使用

![image-20230813231200267](../../../assests/image-20230813231200267.png)

![image-20230813231447668](../../../assests/image-20230813231447668.png)

### allSettled

成功或者失败都能获得`所有的结果`

es11（es2020）

![image-20230813232618090](../../../assests/image-20230813232618090.png)

![image-20230813232419055](../../../assests/image-20230813232419055.png)

### race方法

`先有结果`的就会先获得数据

不论结果是成功还是失败

![image-20230813232837249](../../../assests/image-20230813232837249.png)

### any方法

es12的方法

如果有成功的，`先成功的`结果会给.then，先有失败的结果会被舍弃

![image-20230813233258491](../../../assests/image-20230813233258491.png)

如果`都失败了`，就会执行.catch,只会给下列的信息

![image-20230813233239311](../../../assests/image-20230813233239311.png)