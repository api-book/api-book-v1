# api-book
一个简易的纯前端api笔记本，默认使用浏览器IndexedDB作为临时数据库，通过导出为json作为静态存档。  
可基于vuex接入任何你喜欢的后端服务。  
【Demo】 http://iruxu.com/notebook 

## 安装
1. 确保你已安装[node.js](https://nodejs.org/en/)
2. 直接下载或clone/fork本项目
3. 执行下方命令进行依赖包安装

```
npm install
```

## 本地运行
默认将在localhost:8083打开本地服务。
```
npx vue-cli-service serve
```

## 编译打包
默认将输出在```docs```目录下，可在GitHub Pages中设置其作为主页。
```
npx vue-cli-service build
```

## 配置说明
如对样式与脚本等无特殊要求，可只关注```/public```目录的相关设定。

### index.html文件
默认无需修改，可以在底部根据需要插入你的**统计代码**。

### custom.json文件
+ *publicPath* : 线上访问根目录
+ *lang* : 指定使用lang文件夹下对应的语言文件
+ *editDevonly* : 编辑模式是否仅本地环境可用,当没有开启时,不会使用indexedDB
+ *exportDevonly* : 导出按钮是否仅本地环境可用
+ *dots* : 预设的dot颜色列表,某些时候为了区分某些特别的api的时效性

### setting.json文件
+ *meta* : 用于设置head的标题、关键词、描述
+ *header* : 用于设置页头标题 与 观众模式下显示的github按钮链接（设置为你该项目的github地址）。
+ *menu* : 上方菜单设置，可作为左侧菜单分组，亦可作为外链。
+ *nav* : 左侧导航设置，可分配到指定分组，可指定是否仅本地开发模式可见（方便用于一些自用未写完的）。
+ *footer* : 底部信息的设置项。

### notes目录
数据存档原理：
1. 是否开启编辑? 是 -> 跳转至第2步
2. 浏览器indexedDB中是否有该路由同名数据，对比时间戳，询问是否使用?
y -> 使用浏览器indexedDB中内容作为数据库
n -> 使用本地notes/*.json中内容作为数据库，并覆盖indexedDB同名路由内容
3. 数据变更时，更新indexedDB，并更新时间戳。
  
通常来说，当你需要频繁地更新笔记时，默认所有笔记都将存在浏览器该域名下的indexedDB数据库中。
故如询问是否使用本地indexedDB，请总是回复“y”。
当你需要做存档时，请使用【导出】功能，并保存至```/public/notes```目录下。
当你更换环境前，总是记得需要手动【导出】，indexedDB可能会因浏览器数据不完全受控而影响，但本地的json文件总是最可靠的存档。

## 使用指南

### 基本使用
+ 查看模式下，点击各个项进行查看与折叠展开  
+ 编辑模式下，点击各个项进行编辑与删除，同时可见“增加”相关的功能  
+ 任意模式下，直接拖动各个项，可直接排序（不包括跨级拖动）  
+ 其中，在编辑模式下，双击列排序柄可进行删除列操作  

### 内容编辑
描述与内容区支持markdown语法。
主要语法说明如下：
```markdown
# 标题
*斜体*
**粗体**
***加粗斜体***
~~删除线~~
__下划线__


[链接](http://url)

![图片描述](文件路径.jpg =100x80)
注意：内容中本地图片路径暂时没做处理，请引用图床图片或绝对路径。

> 引用内容

- 无序列表
+ 无序列表
* 无序列表

1. 有序列表
2. 有序列表
3. 有序列表

todolist
- [x] This task is done
- [ ] This is still pending

表格
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

`代码`
---- 水平线

```
