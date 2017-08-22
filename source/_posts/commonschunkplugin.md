title: webpack CommonsChunkPlugin体验
date: 2017-08-22 18:58:24
tags:
---

CommonsChunkPlugin用于抽取公共代码，比如：第三方类库或框架，以及多个入口的公共模块，公共部分会被缓存，所有应用都可以利用缓存内容从而提高性能。

下面通过一个例子来实现公共代码的提取，并且将公共的第三方库和公共的业务模块分开打包。项目地址：https://github.com/labnize/react-webpack3

#### 目录结构如下：

![comchunkplugin1](/img/comchunkplugin1.png)

​          



#### entry配置如下：

![comchunkplugin2](/img/comchunkplugin2.png)

此处有两个入口 app、app1，这两个文件中都引用了模块test2.jsx。

​          



#### CommonsChunkPlugin配置如下：

![comchunkplugin3](/img/comchunkplugin3.png)

**这里name配置为数组，打包时，将符合引用次数(minChunks)的公共业务模块打包到name参数数组的第二个块里，即common。数组中其它的块依次打包(查找entry里的key，没有找到key的则生成一个空的块)，此处只配置公共第三方库，即vendor。**

​          



#### 打包后的文件如下：

![comchunkplugin4](/img/comchunkplugin4.png)

​          

#### webpack配置output时，可以通过可以通过filename模板指定生成的文件名中加上hash值，方便当迭代升级时主动使得浏览器缓存失效。

#### output配置如下：

![comchunkplugin5](/img/comchunkplugin5.png)

因为vendor文件中**不拒绝**包含其他文件的文件名，而其他文件的文件名里的hash值是变化的，因此vendor文件内容是变化的——**vendor文件的hash值也会随迭代升级而变化，太不负责任了，并未成功实现缓存。**

​        



#### 解决办法：

在配置中添加new webpack.HashedModuleIdsPlugin( )。具体说明：https://webpack.js.org/guides/caching/

**注意：使用该插件时，CommonsChunkPlugin中name配置中，vendor必须放在common前面**。

​        

#### 打包后的文件对比：

![comchunkplugin6](/img/comchunkplugin6.png)

可以看出vendor包的hash值没有变化，这样第三方库成功实现了缓存。