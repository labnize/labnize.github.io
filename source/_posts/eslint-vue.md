title: eslint对.vue文件中的template和script进行检查并修复
date: 2017-09-04 18:47:43
tags:
---

项目地址：https://github.com/labnize/vue-vuex-router-element-webpack

### 安装eslint-plugin-vue

```
npm install --save-dev eslint eslint-plugin-vue@3.12
```

**注意：eslint-plugin-vue要求ESlint >=3.18.0 & <= 4.3.0**

此项目因airbnb-base版本要求eslint为3.19.0或4.5.0，所以选择了eslint@3.19.0。

### 配置.eslintrc

```
extends: ['plugin:vue/recommended', 'airbnb-base']
```



某：app.vue

```js
<template>
  <div id="app">
    <layout v-bind=""></layout>
  </div>
</template>

<script>
import Layout from './components/layout';

export default {
  name: 'app'   ,
  components: {
    Layout
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
```

使用命令行进行eslint检查

```
node_modules/.bin/eslint src/app.vue
```



![eslint-vue1](/img/eslint-vue1.png)

可看到报错信息。

### 配置VS code来显示报错提示

```
"eslint.validate": [
        "javascript",
        "javascriptreact",
        "html",
        "vue",
        {"language": "html","autoFix": true},
        {"language": "vue","autoFix": true}
 ],
"javascript.validate.enable": false
```

可看到提示界面如下：

![eslint-vue2](/img/eslint-vue2.png)

### 自动修复eslint报错

以上VS code已配置了保存时自动修复功能

也可使用命令行进行修复

```
node_modules/.bin/eslint --fix src/app.vue
```

