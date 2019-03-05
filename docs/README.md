# BeautyWe

![version](https://badgen.net/badge/cnpm/2.1.2/red)
![downloads](https://badgen.net/badge/downloads/3)

> 一套轻量的微信小程序开发范式

BeautyWe 是一套开发范式，它由几部分组成：

* **核心类库** - `@youzan/beautywe`    
    对 App、Page 进行封装抽象，并且提供插件机制

* **企业级框架** - `@youzan/beautywe-framework`    
    基于 `@youzan/beautywe`，集成基本的官方插件，以及提供开发规范、构建任务、配置、NPM 等解决方案。

* **自动化工具** - `@youzan/beautywe-cli`    
    提供「新建应用」、「新建页面」、「新建插件」、「项目构建」等任务的命令行工具，能自动化的就不手动。
    
* **插件化的解决方案** — `@youzan/beautywe-plugin-xxx`    
    官方以插件的模式提供了各种解决方案，如「增强存储」、「事件发布订阅」、「状态机」、「Redux」、「Error」、「Logger」等。