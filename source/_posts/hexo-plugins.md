title: hexo安装插件
date: 2016-01-20 10:48:27
tags:
---
## sitemap插件

1. 可以将你站点地图提交给搜索引擎，文件路径public/sitemap.xml；
2. 安装
```
$ cnpm install hexo-generator-sitemap --save
```
3. 启用，修改Hexo/_config.yml，增加以下内容
```
# Extensions
Plugins:
- hexo-generator-sitemap
#sitemap
sitemap:
  path: sitemap.xml
```
4. 使用方法
(1) 访问 http://localhost:4000/sitemap.xml，即可看到站点地图。
(2) 将它显示在页面中
    修改themes/landscape下的_config.yml，在menu节点下添加下面的内容：
    ```
    menu:
    Home: /
    Archives: /archives
    Rss: /atom.xml
    Sitemap: /sitemap.xml
    ```

## feed插件
1. Rss的生成插件，你可以在配置显示你站点的Rss，文件路径public/atom.xml；
2. 安装
```
$ cnpm install hexo-generator-feed --save
```
3. 启用，修改Hexo/_config.yml，增加以下内容
```
# Extensions
Plugins:
- hexo-generator-feed
- hexo-generator-sitemap
#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20
```
4. 使用方法参加sitemap插件部分。
