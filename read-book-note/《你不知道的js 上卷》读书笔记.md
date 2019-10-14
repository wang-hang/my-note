# 你不知道的js 上卷读书笔记

## 问题  

1. instanceof的原理是什么？

## 笔记  

### this相关

#### 四种绑定

```js

function foo(){}

// 1. 默认绑定  this指向全局对象 在严格模式下是undefined
foo()

// 2. 隐式绑定 this指向obj

var obj = {foo}
obj.foo()

// 3. 显示绑定  this指向传入的this

foo.call(oThis)
foo.apply(oThis)
foo.bind(oThis)

// 4. new绑定  this指向创建出来的对象

var bar = new foo()

```

#### 四种绑定优先级

new > 显示绑定 > 隐式绑定 > 默认绑定

#### 其他  

1. 空对象的创建方式 Object.create(null) 与 {} 的区别， 前者创建的对象没有 prototype  

2. 使用bind call apply时需要忽略this时最好 传入空对象 Object.create(null)  而不是null  因为传入null时会this会应用默认绑定

### 对象

#### 类型相关  

1. 为什么typeof null === 'object' ?
  因为js中的数据类型在底层都是用二进制表示，前三位为0的都表示为object，而null的值是全0  所以 。。。
  
#### 对象属性  

1. ```key in obj``` 与 ```obj.hasOwnProperty(key)``` 的区别是， 前者会访问原型链 后者只会访问obj的直接属性

2. 遍历对象的两个方法 ```for in``` 与 ```for of``` 区别是 for  in遍历的是属性名  for of 遍历的是对象属性的值
