title: Webpack打包编译进度显示
date: 2017-07-17 13:22:18
tags:
---

## 1. 配置命令行选项

```bash
webpack --progress
```

​          

## 2. ProgressPlugin插件

```js
new webpack.ProgressPlugin(function handler(percentage, msg) {
  console.log((percentage.toFixed(2) * 100) + '%', msg);
})
```

​          

## 3. progress-bar-webpack-plugin插件

![progress-bar](/img/progress-bar.gif)

安装：https://www.npmjs.com/package/progress-bar-webpack-plugin

配置：

```js
new ProgressBarPlugin({
    format: '  build [:bar] :percent (:elapsed seconds)',
    clear: false, 
    width: 60
  })
```



