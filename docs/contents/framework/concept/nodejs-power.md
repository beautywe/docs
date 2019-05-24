# Node.js Power

Beautywe Framework 的代码有两种运行环境：

1. Node.js 运行环境，如构建任务等。
2. 微信小程序运行环境，如打包到 `dist` 文件夹的代码。

## 运行过程

> Node.js Power 本质是一种静态编译的实现。    
> 把某个文件在 Node.js 环境运行的结果，输出到微信小程序运行环境中，以此来满足特定的需求。

Node.js Power 会把项目中 `src` 目录下类似 `xxx.nodepower.js` 命名的文件，以 Node.js 来运行，    
然后把运行的结果，以「字面量对象」的形式写到 `dist` 目录下对应的同名文件 `xxx.nodepower.js` 文件去。

以 `src/config/index.nodepower.js` 为例：

```javascript
const fs = require('fs');
const path = require('path');

const files = fs.readdirSync(path.join(__dirname));

const result = {};

files
    .filter(name => name !== 'index.js')
    .forEach((name) => {
        Object.assign(result, require(path.join(__dirname, `./${name}`)));
    });

module.exports = result;
```

该文件，经过 Node.js Power 构建之后:

`dist/config/index.nodepower.js`: 

```javascript
module.exports = {
    "appInfo": {
        "version": "0.0.1",
        "env": "test",
        "appid": "wx85fc0d03fb0b224d",
        "name": "beautywe-framework-test-app"
    },
    "logger": {
        "prefix": "BeautyWe",
        "level": "info"
    }
};
```

这就满足了，随意往 `src/config/` 目录中扩展配置文件，都能被自动打包。

Node.js Power 已经被集成到多环境开发的 dev, test, prod 中去。

当然，你可以手动运行这个构建任务：

```shell
$ gulp nodejs-power
```