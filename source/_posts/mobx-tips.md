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