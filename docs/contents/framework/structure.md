# App Structure

```json
./
├── dist  // 通过构建的代码，真正在微信小程序环境运行的代码
├── gulpfile.js  // 构建任务
│   ├── config
│   │   └── index.js  // 构建任务的相关配置，能在这里修改各个构建任务的行为。
│   ├── env  // 多环境构建支持，目前支持三套预算策略
│   │   ├── dev.js
│   │   ├── prod.js
│   │   └── test.js
│   ├── clean-example.js  // 清除 example pages 文件
│   ├── clean.js  // 清除 dist 文件
│   ├── copy.js  // 拷贝文件
│   ├── image-min.js  // 图片压缩
│   ├── nodejs-power.js  // 编译 xxx.nodepower.js 文件
│   ├── npm.js  // 编译 npm
│   ├── sass-min.js  // 压缩 scss 文件
│   ├── sass.js  // 编译 scss 文件
│   ├── scripts-min.js  // 压缩 js 文件
│   ├── scripts.js  // 编译 js 文件
│   ├── watch.js  // 监听文件变化并且执行相对编译任务
│   └── index.js  // gulp 入口文件
├── .eslintrc  // 预设的 eslint 配置，使用 airbnb js 规范为基础
├── .gitignore  // 预设的 git ignore 规则
├── package.json
└── src  // 源码目录
    ├── app.js
    ├── app.json
    ├── app.scss
    ├── assets  // 资源文件夹，存放图片、公共样式等
    │   ├── images
    │   │   └── logo.png
    │   └── style
    │       ├── animate.scss
    │       ├── mixin.scss
    │       └── reset.scss
    ├── components  // 全局 UI 组件库
    │   ├── global-view  // 内置组件，全局窗口
    │   ├── copyright   // 内置组件，copyright
    │   └── loading  // 内置组件，loading
    ├── config  // 全局配置
    │   ├── app-info.js  // `getApp().config.appInfo` 来源，包含了应用相关的信息
    │   ├── logger.js  // `getApp().config.logger` 来源，控制了 plugin/logger 的行为
    │   ├── index.js   // 入口文件
    │   └── index.nodepower.js  // 通过Node.js Power，让 config 下所有文件具有 Node.js 能力的中间文件
    ├── examples  // examples 分包，专门用来进行组件、插件的可视化展示
    │   ├── libs
    │   │   └── menu-info.nodepower.js  // 通过Node.js Power, 让Home页面的菜单能动态展示
    │   └── pages  // 
    │       ├── home  // 主页，能跳转到 ./menu 下的展示页面
    │       └── menu  // 菜单页面
    │           ├── comps  // UI 组件类
    │           │   ├── copyright  // 内置组件 copyrig 的示例
    │           │   └── loading  // 内置组件 loading 的示例
    │           └── plugin  // 插件类
    │               ├── event  // event 插件展示
    │               └── listpage  // listpage 插件展示
    ├── libs  // 用来存放全局的公共代码
    │   ├── my-app.js  // app 全局代码，由 app.js 引入
    │   ├── my-comp.js  // component 全局代码，由每一个 component 引入
    │   ├── my-page.js  // page 全局代码，由每一个 page 引入
    │   ├── plugins  // 项目级的 BeautyWe Plugins
    │   │   ├── event.js  // 事件发布/订阅
    │   │   ├── logger.js  // 日志
    │   │   └── storage.js  // 增强存储
    │   ├── utils  // 工具类，里面的函数，应当保持幂等
    │   │   └── helper.js
    │   └── wxs  // 全局的 wxs
    ├── npm
    │   └── index.js  // npm 依赖包的入口文件，由 webpack 打包到 dist/npm/index.js
    ├── pages  // 主包页面
    │   └── welcome  // BeautyWe Framework 欢迎页面，可以删除
    └── project.config.json  // 提供给微信小程序开发 IDE 的项目配置文件
```
