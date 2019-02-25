# BeautyWe CLI

## 介绍

beautywe-cli 提供了以下功能：
1. 创建
    1. 快速创建应用
    2. 快速创建页面
    3. 快速创建插件
2. 运行
    1. 开发环境构建
    2. 测试环境构建
    3. 打包发布构建

## 安装

```
$ ynpm i @youzan/beautywe-cli
```

## new 命令

### `new app`
```
$ beautywe new app
```

通过回答几个预设的问题，就能创建一个应用。    
该应用基于 beautywe-framework 构建，具体该框架的文档参考：[BeautyWe Framework](contents/framework/introduce.md)

### `new page`

```
$ beautywe page <name|path>
```

快速创建页面，创建的页面包含以下四个文件：

1. xxx/index.js
2. xxx/index.json
3. xxx/index.scss
4. xxx/index.wxml

**<name|path> 逻辑**：
 1. 如果name只提供页面名称（例如name: 'myPage'），则最终生成的目录是 `{defaultRoot}/myPage` ({project}为app.json所在目录)。
 1. 如果name是相对路径（例如name: 'path/myPage'），则最终生成的目录是 `{defaultRoot}/path/myPage`。
 1. 如果name是绝对路径（例如name: '/some/path/myPage'），则最终生成的目录是 `{project}/some/path/myPage`。
 1. 如果name只填写了路径（例如name: '/some/path/'），则当做 '/some/path' 处理。

### `new plugin`

```
$ beautywe new plugin <name> [dir]
```

快速创建一个插件文件

**name**

插件名，默认是命令执行的当前文件夹。

**dir**

可选项，可以指定插件文件生成的文件夹

### `new plugin-module`

```
$ beautywe new plugin-module
```

快速创建一个，集成了 **eslint 规范**、**commit 规范**、**单元测试**、**测试覆盖率** 等内容，你只需编写最关键的插件代码


## run 命令

run 命令底层是调用了 gulp 任务。    
该命令的适用范围是用来适配 beautywe-framework 的

`beautywe run dev` = `gulp dev`

