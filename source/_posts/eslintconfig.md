title: eslint配置
date: 2017-06-18 23:15:02
tags:
---
##  安装、配置

```
$ npm install eslint --save-dev
```

在项目根目录下新建.eslintrc进行配置

可参考

https://github.com/eslint/eslint

http://eslint.cn/docs/user-guide/configuring

___



## 规则

rules可以到[Llist of available rules ](http://eslint.org/docs/rules/)进行查询。

规则的错误等级有三种：

- "off" 或者 0：关闭规则。
- "warn" 或者 1：打开规则，并且作为一个警告（不影响exit code）。
- "error" 或者 2：打开规则，并且作为一个错误（exit code将会是1）。

___



## 指定全局变量

可以在配置文件或注释中指定额外的全局变量，`false`表明变量只读：

注释：

```
/* global var1, var2 */
/* global var1:false, var2:false */
```

JSON:

```
{
  "globals": {
      "var1": true,
      "var2": false
  }
}
```

___



附上一份个人目前正在使用的配置:

```
"devDependencies": {
    "eslint": "^3.19.0",
    "eslint-config-airbnb": "^15.0.1",
    "eslint-plugin-import": "^2.3.0",
    "eslint-plugin-jsx-a11y": "^5.0.3",
    "eslint-plugin-react": "^7.1.0"
    }
```



```
{
  "extends": "airbnb",
  "parser": "babel-eslint",
  "env": {
    "browser" : true
  },
  "rules": {
    "quotes": [2, "single"],
    "semi": 2,
    "max-len": [1, 120, 2],
    "arrow-body-style": [1, "as-needed"],
    "comma-dangle": [2, "never"],
    "no-debugger": 2,
    "no-console": 2,
    "object-curly-spacing": [2, "always"],
    "no-undef": [1],
    "new-cap": 1,
    "no-param-reassign": 2,
    "import/no-extraneous-dependencies": 0,
    "import/no-unresolved": 0,
    "import/extensions": 0
  }
}
```

