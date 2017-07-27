title: Mobx--那些踩过的坑。。
date: 2017-07-25 16:02:52
tags:
---
## 1. Mobx追踪属性访问，而不是值。

也就是说，当对observable中的属性进行拷贝后，如果再来改变这个值，Mobx是不会作出反应的（即不会重新进行render）。下面代码不会重新render。

![mobx1](/img/mobx1.jpg)

​          

需要对对象进行拷贝，才会重新render，如下：

![mobx2](/img/mobx2.jpg)

​          

考虑到减少render次数，提升性能，当observable中的list和total都需要改变时，只让页面render一次。代码如下：

![mobx3](/img/mobx3.jpg)

​          

#### 注意：此处使用扩展运算符或Object.assign对对象进行拷贝，如果只是通过"="进行拷贝，Mobx不会对嵌套的对象进行递归。对比如下：

![mobx4](/img/mobx4.jpg)

​          

![mobx5](/img/mobx5.jpg)

​          

## 2. 传递对象

当通过 observable 传递对象时，只有在把对象转变 observable 时存在的属性才会是可观察的。 稍后添加到对象的属性不会变为可观察的，除非使用 [extendObservable](http://cn.mobx.js.org/refguide/extend-observable.html)。

​          

## 3. 传递数组

请记住无论如何 Array.isArray(observable([])) 都将返回 false ，所以无论何时当你需要传递 observable 数组到外部库时，通过使用 array.slice() 在 observable 数组传递给外部库或者内置方法前创建一份浅拷贝(无论如何这都是最佳实践)总会是一个好主意。 换句话说，Array.isArray(observable([]).slice()) 会返回 true。