title: Antd字体图标本地化
date: 2017-09-05 15:38:01
tags:
---

> antd图标默认托管在http://iconfont.cn/， 默认公网可访问。如需本地部署，可参考[示例](https://github.com/ant-design/antd-init/tree/master/examples/local-iconfont)。

以上是antd官网推荐方法，但亲测后发现有坑，打包后字体图标文件并没有成功打包。

经过一番尝试，得出以下解决方案：

### antd主题配置

```js

'@icon-url': `"${path.relative('./~/antd/lib/style/*', './res/iconfont/iconfont')}"`
```

此处得是相对路径。

___



### webpack配置

```
{
        test: /\.(woff|woff2|eot|ttf)$/,
        use: ['url-loader?limit=1&name=iconfont/[name].[hash:8].[ext]']
}
```

将字体图标打包到iconfont文件夹中。