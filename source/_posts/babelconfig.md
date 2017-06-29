title: webpack中babel配置
date: 2017-06-28 16:03:49
tags:
---

> Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而在现有的环境执行。这意味着，你可以现在就用ES6编写程序，而不用担心现有环境是否支持。



## 一、babel-loader安装使用

```
npm install babel-loader babel-core babel-preset-env webpack --save-dev
```

or

```
yarn add babel-loader babel-core babel-preset-env webpack --dev
```

webpack config中配置见 https://github.com/babel/babel-loader/tree/v6.4.1

___



## 二、配置文件.babelrc

Babel的配置文件是.babelrc，存放在项目的根目录下。

该文件用来设置转码规则和插件，基本格式如下：

```
{
  "presets": [],
  "plugins": []
}
```

`presets`字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。

```
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

然后，将这些规则加入`.babelrc`

```
{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```

注意，以下所有Babel工具和模块的使用，都必须先写好.babelrc。

___



## 三、babel-core

如果某些代码需要调用Babel的API进行转码，就要使用`babel-core`模块。

安装命令如下：

```
$ npm install babel-core --save-dev
```

一般babel-core都是作为babel-loader的依赖项添加的。

___



## 四、babel-polyfill

Babel默认值转换新的JavaScript句法，而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6在`Array`对象上新增了`Array.from`方法。Babel就不会转码这个方法。如果想让这个方法运行，必须使用`babel-polyfill`，为当前环境提供一个垫片。

安装命令如下：

```
$ npm install --save babel-polyfill
```

然后，在脚本头部，加入如下一行代码。

```
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

Babel默认不转码的API非常多，详细清单可以查看`babel-plugin-transform-runtime`模块的[definitions.js](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js)文件。

___



## 五、与其他工具的配合

许多工具需要Babel进行前置转码，比如ESLint

ESlint用于静态检查代码的语法和风格，安装命令如下：

```
$ npm install --save-dev eslint babel-eslint
```

然后，在项目根目录下，新建一个配置文件`.eslint`，在其中加入`parser`字段。

```
{
  "parser": "babel-eslint",
  "rules": {
    ...
  }
}
```



