## Intro

BeautyWe Framework 作为一套开箱即用的项目框架，他提供了这些功能：

* BeautyWe Core
* NPM 支持
* 全局窗口
* 全局 Page，Component
* 全局配置文件
* 多环境开发
* Example Pages
* 正常项目需要的标配：ES2015+,sass,uglify,watch 等
* 以及我们认为良好的项目规范（eslint，commit log，目录结构等）

## Download
```shell
npm i @beautywe/cli -g
```

## New Project
```shell
$ beautywe new app
```

回答几个问题之后，会自动生成项目：

![new app](../../../assets/svg/new-app.svg)

> [详细的项目结构](/contents/framework/structure.md)

## Run
安装依赖包
```shell
cd ./my-app && npm i
```

运行
```shell
beautywe run dev
```

用 「微信开发者工具」 打开目录文件夹：
```shell
${project_dir}/dist
```

然后你会看到这样的欢迎界面：

<div style="display: flex; justify-content:center; margin: 30px 0">
    <video width="375" height="667" controls autoplay>
        <source src="../../assets/videos/welcome.mov" type="video/mp4">
    </video>
</div>

