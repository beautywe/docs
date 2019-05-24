# 多环境开发

BeautyWe Framework 支持多环境开发，其中预设了三套策略：
* dev
* test
* prod

我们可以通过命令来运行这三个构建策略：

```shell
beautywe run dev
beautywe run test
beautywe run prod
```

## 三套环境的差异

Beautywe Framework 源码默认在两方面使用了多环境：

* 构建任务（`gulpfile.js/env/...`）
* 全局配置（`src/config/...`）

### 构建任务的差异

| 构建任务 | 说明 |dev | test | prod |
|---|---|:---:|:---:|:---:|
| clean | 清除dist文件 | √ | √ | √ |
| copy | 复制资源文件 | √ | √ | √ |
| scripts | 编译JS文件 | √ | √ | √ |
| sass | 编译scss文件 | √ | √ | √ |
| npm | 编译npm文件 | √ | √ | √ |
| nodejs-power | 编译Node.js文件 | √ | √ | √ |
| watch | 监听文件修改 | √ | | |
| scripts-min | 压缩JS文件 |  |  | √ |
| sass-min | 压缩scss文件 |  |  | √ |
| npm-min | 压缩npm文件 | | | √ |
| image-min | 压缩图片文件 |  |  | √ |
| clean-example | 清除示例页面 | | | √ |

### 全局配置的差异

| 配置 | 说明 |dev | test | prod |
|---|---|:---:|:---:|:---:|
| logger | logger插件的配置,具体参考：[plugin-logger](/remote/plugin-logger.md) | level: debug | level: info | level: warn |

## 全局环境变量

BeautyWe Framework 在两处地方存储了环境变量，以方便在任意的开发过程中，对多环境进行特定的逻辑。

一是，针对运行在 Node.js 环境的代码，如构建任务，环境变量放在：

```javascript
process.env.RUN_ENV
```

二是，针对运行在微信小程序环境的代码，如打包到 `dist` 目录的代码，环境变量放在：

```javascript
import { appInfo } from '/config/index';
appInfo.RUN_ENV;

// or
getApp().config.appInfo.RUN_ENV;
```

## 扩展自定义环境策略

BeautyWe Framework 支持扩展自定义的环境策略。

例如，要扩展一个 `myEnv` 的环境策略：

- Step1：新建 `gulpfile.js/env/myEnv.js` 文件。
- Step2：编写 `myEnv.js` 文件，实现自定义的 gulp 任务，写法可以参考已有的环境策略文件。
- Step3：在需要的地方读取全局环境变量，实现自定义逻辑。
- Step4：执行 `beautywe run myEnv`，运行构建任务。

> 这里要有必要说明 `beautywe run xxx` 命令做了哪些事情：
1. 寻找 `/gulpfile.js/env/xxx.js` 文件，以 gulp 的形式执行它。
2. 注入 `process.env.RUN_ENV = xxx`。