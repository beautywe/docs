## Intro

BeautyWe Framework 提供了一套开箱即用的项目框架，他集成了这些功能：

* beautywe
* 使用 NPM 包解决方案
* 全局窗口解决方案
* 一套构建解决方案（js、scss、压缩、多环境等）
* 全局范围的配置信息
* 以及我们认为良好的项目规范（eslint，目录结构等）

## Download
```
npm i @beautywe/cli -g
```

## New Project
```
$ beautywe new app

> appName: my-app
> version: 0.0.1
> appid: 12345678
> 这样可以么:
{
    "appName": "my-app",
    "version": "0.0.1",
    "appid": "12345678"
}
```

回答几个问题之后，会自动生成项目：

```
./my-app
├── package.json
├── gulpfile.js    // 构建任务
├── dist    // 生产代码
└── src    // 源代码
```

## Run
安装依赖包
```
cd ./my-app && npm i
```

运行
```
beautywe run dev
```

用 「微信开发者工具」 打开目录文件夹：
```
${project_dir}/dist
```

然后你会看到这样的欢迎界面：

<div style="display: flex; justify-content:center; margin: 30px 0">
    <video width="375" height="667" controls autoplay>
        <source src="../../assets/videos/welcome.mov" type="video/mp4">
    </video>
</div>

