title: webpack CommonsChunkPlugin体验
date: 2017-08-17 13:58:24
tags:
---

CommonsChunkPlugin用于抽取公共代码，比如：第三方类库或框架，以及多个入口的公共模块，公共部分会被缓存，所有应用都可以利用缓存内容从而提高性能。

下面通过一个例子来实现公共代码的提取，并且将公共的第三方库和公共的业务模块分开打包。

#### 目录结构如下：

![comchunkplugin1](/img/comchunkplugin1.png)

​          



#### entry配置如下：

![comchunkplugin2](/img/comchunkplugin2.png)

此处有两个入口 app、app1，这两个文件中都引用了模块test2.jsx。

​          



#### CommonsChunkPlugin配置如下：

![comchunkplugin3](/img/comchunkplugin3.png)

**这里name配置为数组，打包时，将符合引用次数(minChunks)的公共业务模块打包到name参数数组的第一个块里，即common。数组后面的快依次打包(查找entry里的key，没有找到key的则生成一个空的块)，此处只配置公共第三方库，即vendors。**

​          



#### 打包后的文件如下：

![comchunkplugin4](/img/comchunkplugin4.png)