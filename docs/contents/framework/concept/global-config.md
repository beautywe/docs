# Global Config

在 `src/config/` 目录中，可以存放各种全局的配置文件，并且支持以 Node.js 的方式运行。（得益于 [Node.js Power 特性](/contents/framework/concept/nodejs-power.md)）。

如 `src/config/logger.js`:

```javascript
const env = process.env.RUN_ENV || 'dev';

const logger = Object.assign({
    prefix: 'BeautyWe',
    level: 'debug',
}, {
    // 开发环境的配置
    dev: {
        level: 'debug',
    },
    // 测试环境的配置
    test: {
        level: 'info',
    },
    // 线上环境的配置
    prod: {
        level: 'warn',
    },
}[env] || {});

module.exports.logger = logger;
```

然后我们可以这样读取到 config 内容：

```javascript
import { logger } from '/config/index';

// logger.level 会根据环境不同而不同。
```

Beautywe Framework 默认会把 config 集成到 `getApp()` 的示例中：

```javascript
getApp().config;
```