## Introduction
----

BeautyWe 是一套微信小程序的开发范式，它由几部分组成：

* **核心类库** - [**@beautywe/core**](https://www.npmjs.com/package/@beautywe/core)    
    对 App、Page 进行封装抽象，并且提供插件机制

* **插件生态** — [**@beautywe/plugin-xxx**](https://www.npmjs.com/search?q=keywords%3Abeautywe-plugin)    
官方以插件的模式提供了各种解决方案，如「增强存储」、「事件发布订阅」、「状态机」、「Error」、「Logger」等。

* **企业级框架** - [**@beautywe/framework**](https://www.npmjs.com/package/@beautywe/framework)    
    基于 `beautywe/core`，提供一套开箱即用的项目框架，包含开发规范、构建任务、配置、NPM 等解决方案。

* **自动化工具** - [**@beautywe/cli**](https://www.npmjs.com/package/@beautywe/cli)    
    提供「新建应用」、「新建页面」、「新建插件」、「项目构建」等任务的命令行工具，解放双手。

## Usage Example


```
npm i @beautywe/core @beautywe/plugin-event
```

```javascript
import { BtApp } from '@beautywe/core';
import event from '@beautywe/plugin-event';

const myApp = new BtApp({
    // the code as you write for App()
});

myApp.use(event());

App(myApp);
```

之后，你就能使用 `plugin-event` 提供的能力了：

```javascript
const app = getApp();

// now you can listening and trigger an event
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```

# Contact & Support


* 欢迎通过邮箱来跟我联系: huangjerryc@gmail.com
* 欢迎通过 [GitHub issue](https://github.com/beautywe/beautywe/issues) 提交 BUG、以及其他问题
* 欢迎给该项目点个赞 ⭐️ [star on GitHub](https://github.com/beautywe/beautywe) !



# License


This project is licensed under the [MIT license](https://raw.githubusercontent.com/beautywe/beautywe/master/LICENSE).

Copyright (c) JerryC Huang (huangjerryc@gmail.com)