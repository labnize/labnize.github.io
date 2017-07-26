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

#### 注意：此处使用扩展运算符或Object.assign对对象进行拷贝，如果只是通过‘=’进行拷贝，Mobx不会对嵌套的对象进行递归。对比如下：

![mobx4](/img/mobx4.jpg)

​          

![mobx5](/img/mobx5.jpg)