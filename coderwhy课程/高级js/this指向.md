### 指向window

![image-20230810215518032](../../../assests/image-20230810215518032.png)

严格模型下，独立调用的函数this指向undefined

## 显示绑定this

### call

```js
函数.call(要绑定this的对象，参数1，参数2)
foo.call(obj，25,3)
```

### apply

```js
函数.apply(要绑定this的对象,[参数1，参数2])
foo.apply(obj,[25,3])
```

### bind

新函数绑定函数的this

不用每次调用是都去绑定函数的this

![image-20230814132031380](../../../assests/image-20230814132031380.png)

### this的优先级

默认绑定<隐式绑定<显示绑定

call和apply<bind

new的优先级高于bind，不能和call和apply一起使用

### 箭头函数

![image-20230813230206644](../../../assests/image-20230813230206644.png)

#### 箭头函数的this

this向上层作用域查找this，箭头函数自身没有this

箭头函数也不能绑定this

