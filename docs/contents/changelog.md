# Changelog

所有 BeuatyWe 值得注意的变更都会记录在这个文件中。

该文档格式参考自 [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
并且该项目遵循 [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.2.0] - 2019-04-03

--------

### New versions of BeautyWe family

- beautywe@2.2.0
- beautywe-framework@0.1.0
- beautywe-cli@0.0.11
- beautywe-plugin-storage@0.1.0
- beautywe-plugin-event@0.1.0
- beautywe-plugin-status@0.1.0
- beautywe-plugin-cache@0.1.0
- beautywe-plugin-listpage@0.1.0

### Added
- 新增插件生命周期钩子：`beforeAttach`, `attached`, `initialize`，[参考：插件的生命周期](/contents/core/plugin/how-to-work.md#插件的生命周期)
- `beautywe-cli` 的「快速创建功能」新增 `Component` 实现
- `beautywe-cli` 的「快速创建功能」支持自定义模板，并且支持独立于 `beautywe-framework` 使用
- `beautywe-framework` 增加「快速创建功能」自定义模板的实现

### Changed
- 插件不再是 `BtPlugin` 的实例，而只是一个直接定义的 `Object` 的实例，[参考：插件编写](/contents/core/plugin/write.md)
- 新的实现插件功能的设计架构，[参考：插件原理](/contents/core/plugin/how-to-work.md)
- 更新所有官方插件，以支持 `beautywe@2.2.0`，涉及到：
    - beautywe-plugin-storage
    - beautywe-plugin-event
    - beautywe-plugin-status
    - beautywe-plugin-cache
    - beautywe-plugin-listpage

### Fixed
- 修复 `onLoad/onLaunch` 与 `onShow` 执行顺序不确定问题。
