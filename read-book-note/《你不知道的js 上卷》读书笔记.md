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

#### 四种绑定的优先级

new > 显示绑定 > 隐式绑定 > 默认绑定

#### 其他  

1. 空对象的创建方式 Object.create(null) 与 {} 的区别， 前者创建的对象没有 prototype  

2. 使用bind call apply时需要忽略this时, 最好传入空对象 ```Object.create(null)```  而不是```null```  因为传入null时会this会应用默认绑定

### 对象

#### 类型相关  

1. 为什么typeof null === 'object' ?
  因为js中的数据类型在底层都是用二进制表示，前三位为0的都表示为object，而null的值是全0  所以 。。。
  
#### 对象属性  

1. ```key in obj``` 与 ```obj.hasOwnProperty(key)``` 的区别是， 前者会访问原型链 后者只会访问obj的直接属性

2. 遍历对象的两个方法 ```for in``` 与 ```for of``` 区别是 for  in遍历的是属性名  for of 遍历的是对象属性的值

### 原型

### 原型链

1. 原型链查找的终点是Object.prototype
2. 属性设置和屏蔽```myObject.foo = 'bar'```, 如果foo属性不存在与myObject的直接属性上 = 的行为会有些不同
  a. foo属性 非只读（writable:true）会在myObject的属性上添加一个新foo属性
  b. foo属性 只读（writable:false） 复制语句会被忽略
  c. foo属性是原型上的setter foo不会被添加到myObjec中
