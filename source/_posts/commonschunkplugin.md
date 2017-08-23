title: webpack commonschunkplugin体验
date: 2017-08-23 17:11:20
tags:
---

CommonsChunkPlugin用于抽取公共代码，比如：第三方类库或框架，以及多个入口的公共模块，公共部分会被缓存，所有应用都可以利用缓存内容从而提高性能。

下面通过具体来实现公共代码的提取，并且将公共的第三方库和公共的业务模块分开打包。项目地址：https://github.com/labnize/react-webpack3

## 1.多页应用例子

#### 目录结构如下：

![comchunkplugin1](/img/comchunkplugin1.png)

​          



#### entry配置如下：

![comchunkplugin2](/img/comchunkplugin2.png)

此处有两个入口 app、app1，这两个文件中都引用了模块test1.jsx。

​          

#### CommonsChunkPlugin配置如下：

![comchunkplugin3](/img/comchunkplugin3.png)

**这里name配置为数组，打包时，将符合引用次数(minChunks)的公共业务模块打包到name参数数组的第一个块里，即common。数组中其它的块依次打包(查找entry里的key，没有找到key的则生成一个空的块)，此处只配置公共第三方库，即vendor。runtime可以所有的打包变成你想要的样子，效果见打包结果对比。**

 因为vendor文件中**不拒绝**包含其他文件的文件名，而其他文件的文件名里的hash值是变化的，因此vendor文件内容是变化的——**vendor文件的hash值也会随迭代升级而变化，太不负责任了，并未成功实现缓存。**

需要在wepack config中配置插件new webpack.HashedModuleIdsPlugin( )。具体说明：https://webpack.js.org/guides/caching/         

​          



#### output配置如下：

![comchunkplugin5](/img/comchunkplugin6.png)

webpack配置output时，可以通过可以通过filename模板指定生成的文件名中加上chunkhash值，方便当迭代升级时主动使得浏览器缓存失效。

​          



#### 打包后的文件如下：

![comchunkplugin4](/img/comchunkplugin4.png)

> vendor中放的是第三方库文件
>
> common中放的是main.jsx和main1.jsx共同引用的test1.jsx文件
>
> app和app1分别存放的对应的main.jsx和main1.jsx文件

#### 当main.jsx改变后，打包结果对比如下：

![comchunkplugin5](/img/comchunkplugin5.png)

发现vendor和common的hash值都没有改变，从而成功实现了缓存。**如果不加runtime，则vendor的hash值是变化的。**

官网解释如下：

![comchunkplugin8](/img/comchunkplugin8.png)

链接地址：https://webpack.js.org/guides/caching/

___

## 2.单页应用

单页应用没有多个入口文件，所以不会有公共引用的业务模块，只需将CommonsChunkPlugin配置如下就可以了：

![comchunkplugin7](/img/comchunkplugin7.png)

打包出的文件少了common。