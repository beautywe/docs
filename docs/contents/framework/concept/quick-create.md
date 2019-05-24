# 快速创建

得益于自 `@beautywe/cli` 的快速创建功能，在开发过程中支持以下文件的快速创建：
* 快速创建 Page
* 快速创建 Component
* 快速创建 BeautyWe Plugin

## 创建 Page

![new page](../../../assets/svg/new-page.svg)

功能：

* 自动生成 index.js, index.wxml, index.scss, index.json 文件
* 自动写入路由到 app.json 文件

模式：

```shell
# 主包页面
beautywe new page <path|name>

# 分包页面
beautywe new page --subpkg <subPackageName> <path|name>
```

例子：

```shell
# 主包页面，页面名称，创建到：/src/pages/helloworld
beautywe new page hellowold

# 主包页面，相对路径，创建到: /src/pages/goods/foods
beautywe new page goods/foods

# 主包页面，绝对路径，创建到: /goods/foods
beautywe new page /goods/foods

# 分包页面，页面名称，创建到：/src/goods/pages/foods
beautywe new page --subpkg goods foods

# 分包页面，相对路径，创建到：/src/goods/pages/foods/cookie
beautywe new page --subpkg goods foods/cookie
```

## 创建 Component

![new component](../../../assets/svg/new-component.svg)

功能：

* 自动生成 index.js, index.wxml, index.scss, index.json 文件

模式：

```shell
beautywe new component <name>
```

例子：

```shell
# 插件名称，创建到：/src/components/dialog
beautywe new component dialog

# 相对路径，创建到：/src/components/dialog/red
beautywe new component dialog/red

# 绝对路径，创建到：/dialog/red
beautywe new component /dialog/red
```


## 创建 BeautyWe Plugin

![new plugin](../../../assets/svg/new-plugin.svg)

功能：

* 自动生成插件 js 文件

模式：

```shell
beautywe new plugin <name>
```

例子：

```shell
# 组件名称，创建到：/src/libs/plugins/log.js
beautywe new plugin log
```

## 自定义模板

在 `./.templates` 目录中，存放着快速创建命令的创建模板：

```shell
$ tree .templates

.templates
├── component
│   ├── index.js
│   ├── index.json
│   ├── index.scss
│   └── index.wxml
├── page
│   ├── index.js
│   ├── index.json
│   ├── index.scss
│   └── index.wxml
└── plugin
    └── index.js
```

可以修改里面的模板，来满足项目级别的自定义模板创建。

详情看：[BeautyWe Cli - tempaltes](remote/cli.md#templates)

## 配置

在 `./.beautywerc` 中，有针对快速创建命令的默认配置：

```shell
$ cat .beautywerc 

{
    "templates": {
        "component": {
            "source": ".templates/component",
            "defaultOutput": "components"
        },
        "page": {
            "source": ".templates/page",
            "defaultOutput": "pages"
        },
        "plugin": {
            "source": ".templates/plugin",
            "defaultOutput": "libs/plugins"
        }
    },
    "distDir": "dist",
    "appDir": "src",
    "writeRouteAfterCreated": true
}
```

详情看：[BeautyWe Cli - beautywerc](remote/cli.md#beautywerc)