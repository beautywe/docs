# Changelog

所有 BeuatyWe 值得注意的变更都会记录在这个文件中。

该文档格式参考自 [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
并且该项目遵循 [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

-----
## Release #002 - 2019.05.27
> For details:  [Release #002](https://github.com/orgs/beautywe/projects/3)

### Added

* 新增 eslint 校验，[详情](/contents/framework/concept/specification.md#js-代码)
* 新增 git commit log 校验，[详情](/contents/framework/concept/specification.md#git-commit-log)

### Release Versions
- [@beautywe/framework v1.0.4](https://www.npmjs.com/package/@beautywe/framework/v/1.0.4)

-----
## Release #001 - 2019.05.26
> For details:  [Release #001](https://github.com/orgs/beautywe/projects/1)

### Added

* plugin-listpage 新增 autoLoadFirstPage 配置参数，支持自动加载第一页数据。[详情](https://github.com/beautywe/plugin-listpage#%E6%89%8B%E5%8A%A8%E5%8A%A0%E8%BD%BD%E7%AC%AC%E4%B8%80%E9%A1%B5%E6%95%B0%E6%8D%AE)
* 新增 plugin-logger 插件。[详情](https://github.com/beautywe/plugin-logger)
* Framework 新增 example pages 支持。[详情](/contents/framework/concept/example-pages)
* Framework 新增全局窗口。[详情](/contents/framework/concept/global-view)
* Framework 新增 Node.js Power 特性。[详情](/contents/framework/concept/nodejs-power)
* Framework 集成 plugin-listpage。[详情](/remote/plugin-listpage)
* Framework 集成 plugin-logger。[详情](/remote/plugin-logger)
* Framework 新增欢迎界面
* Framework 新增内置 UI 组件：loading，copyright
* Cli 自定填充 `RUN_ENV` 变量到 `process.env`
* Cli 新增模板参数 `relativeToAppDir`。[详情](https://github.com/beautywe/cli#%E6%A8%A1%E6%9D%BF%E5%8F%82%E6%95%B0)
* Cli `new page` 支持自动更新 app.json，并且支持分包。[详情](https://github.com/beautywe/cli#new-page)

### Changed

* Framework 调整多环境开发支持。[详情](/contents/framework/concept/multi-env)
* Core initialize 执行时机放置到 deepBind 之后
* Core 补全单元测试，覆盖率达到 97%

### Removed

* Framework 移除 json-compile 构建任务，由 nodejs-power 代替。

### Release Versions
- [@beautywe/core v1.0.0](https://www.npmjs.com/package/@beautywe/core/v/1.0.0)
- [@beautywe/cli v1.0.3](https://www.npmjs.com/package/@beautywe/cli/v/1.0.3)
- [@beautywe/framework v1.0.3](https://www.npmjs.com/package/@beautywe/framework/v/1.0.3)
- [@beautywe/plugin-storage v1.0.0](https://www.npmjs.com/package/@beautywe/plugin-storage/v/1.0.0)
- [@beautywe/plugin-listpage v1.0.1](https://www.npmjs.com/package/@beautywe/plugin-listpage/v/1.0.1)
- [@beautywe/plugin-status v1.0.0](https://www.npmjs.com/package/@beautywe/plugin-status/v/1.0.0)
- [@beautywe/plugin-event v1.0.0](https://www.npmjs.com/package/@beautywe/plugin-event/v/1.0.0)
- [@beautywe/plugin-cache v1.0.0](https://www.npmjs.com/package/@beautywe/plugin-cache/v/1.0.0)
- [@beautywe/plugin-logger v1.0.0](https://www.npmjs.com/package/@beautywe/plugin-logger/v/1.0.0)


-----
## Release #000 - 2019.05.01

💥💥💥 The Bing Bang !!!     
💥💥💥 The Bing Bang !!!     
💥💥💥 The Bing Bang !!!    

### Release Versions
- [@beautywe/core v0.0.10](https://www.npmjs.com/package/@beautywe/core/v/0.0.10)
- [@beautywe/cli v0.0.5](https://www.npmjs.com/package/@beautywe/cli/v/0.0.5)
- [@beautywe/framework v0.0.3](https://www.npmjs.com/package/@beautywe/framework/v/0.0.3)
- [@beautywe/plugin-storage v0.0.2](https://www.npmjs.com/package/@beautywe/plugin-storage/v/0.0.2)
- [@beautywe/plugin-listpage v0.0.2](https://www.npmjs.com/package/@beautywe/plugin-listpage/v/0.0.2)
- [@beautywe/plugin-status v0.0.2](https://www.npmjs.com/package/@beautywe/plugin-status/v/0.0.2)
- [@beautywe/plugin-event v0.0.3](https://www.npmjs.com/package/@beautywe/plugin-event/v/0.0.3)
- [@beautywe/plugin-cache v0.0.2](https://www.npmjs.com/package/@beautywe/plugin-cache/v/0.0.2)

