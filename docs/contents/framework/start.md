## Download
```
ynpm i @beautywe/beautywe-cli -g
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
cd ./my-app && ynpm i
```

运行
```
beautywe run dev
```

用 「微信开发者工具」 打开目录文件夹：
```
${project_dir}/dist
```

## New Page

### 创建页面

自匹配页面路径
```
$ beautywe new page hello  
// 页面会创建在：/pages/hello/
```

自定义路径：
```
$ beautywe new page member/hello
// 页面会创建在：/pages/member/hello/
```

分包支持（开发中...）：
```
$ beautywe new page subpkg/hello --subpkg
// 页面会创建在：/subpkg/pages/hello/
```

### 配置页面

在 `src/config/routes.js` 中配置该页面：

```javascript
module.exports.routes = {
    hello: 'pages/hello/index',
};
```