title: webpack打包html中图片
date: 2017-08-15 09:19:40
tags:
---

## 1. 通过javascript引入图片

```
//ES2016
import imgUrl from 'path/to/xxxx.png';

//CommonJS
var imgUrl = require('path/to/xxxx.png');
```

js:

```
imgTempl = '<img src="'+imgUrl+'" />';
document.body.innerHTML = imgTempl;
```

react

```
render() {
    return (<img src={imgUrl} />);
}
```

---

## 2. 通过html-withimg-loader打包

```
$ npm install html-withimg-loader --save-dev
```

webpack.config.js添加配置

```
module: {
　　loaders: [
　　　　{
　　　　　　test: /\.html$/,
　　　　　　loader: 'html-withimg-loader'
　　　　}
　　]
}
```

img中src的路径必须为相对路径

```
render() {
    return (<img src='./images/bg.jpg' />);
}
```

