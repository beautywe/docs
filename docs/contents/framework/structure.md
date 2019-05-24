# App Structure

## .templates

存放用于 `beautywe new ` 命令的自定义模板库，包含：

* .templates/component/
* .templates/page/
* .templates/plugin/

## /dist

通过构建任务，从 `/src` 构建代码到 `/dist`。    
从 「微信开发者工具」读取的应当是 `/dist` 文件夹。

## /src

整个项目的核心源码所在，通过构建任务，会构建到 `/dist` 去

### /assets

这里应该存放全局性的图片、样式等资源文件。

#### /assets/images

图片放这里

#### /style

全局样式放这里，并且会在 `./app.scss` 中引入这里的代码

### /libs

全局性的公用库都会放到这里。

#### /container

提供了「全局窗口」的实现，本质是一个「自定义组件」。    
所有页面都需要引入该组件，并且作为最高层的组件：

pages/xxx/index.json
```json
{
    "usingComponents": {
        "container": "/libs/container/index"
    }
}
```

pages/xxx/index.wxml
```javascript
<container>
    <!-- 本页面代码 -->
</container>
```

通过这样的方式，我们就能在 `container` 组件中编写全局范围的业务了，比如全局性的弹窗、loading、copyright 等。

#### /plugins

自定义的 BeautyWe 插件，都会放到这里来，关于插件的内容请看：[《插件》](contents/core/plugin/use.md)

#### /utils

项目级的工具类库放这里

#### /wxs

项目级的 wxs 文件放这里

#### my-page.js

为了提供所有页面的共有逻辑实现手段，所有页面应当使用 `MyPage()` 替代原生的 `Page()`

pages/xxx/index.js
```javascript
import MyPage from '../../libs/my-page.js';

MyPage({
    // ...
})
```

然后，你就能通过修改 `my-page.js` 文件，来达到编写页面的全局性业务逻辑了。

比如，我们要所有页面都使用 `beautywe-plugin-listpage` 插件：

my-page.js
```javascript
import { beautywe, listpagePlugin } from '../npm/index';

const { BtPage } = beautywe;

export default function (wxPage) {
    const myPage = new BtPage(wxPage);
    myPage.use(listpagePlugin({
        // ...
    }))
    Page(myPage);
}

```

#### my-comp.js

为了提供所有组件的共有逻辑实现手段，所有自定义组件应当使用 `MyComponent()` 替代原生的 `Component()`

components/xxx/index.js
```javascript
import MyComponent from '../libs/my-comp.js';

MyComponent({
    // ...
})
```

然后，你就能通过修改 `my-comp.js` 文件，来达到编写自定义组件的全局性业务逻辑了。

## /gulpfile.js

beautywe-framework 提供了工程化所需要的常用的构建任务，所有实现都是基于 Gulp.js 来实现的，更多 Gulp.js 内容参考：[Gulp.js](https://gulpjs.com/)

### /env

在实际的项目开发中，我们通常会区分好几种环境，并且不同环境的构建流是有差异性的。     
在 beautywe-framework 中，内置了三种环境的开发流：
* **开发环境**：集成了 js编译、sass编译、json编译、npm编译、watch 等构建任务
* **测试环境**：在开发环境基础上去掉 watch 构建任务
* **发布构建**：在测试环境基础上，增加了代码压缩等任务

当然，你可以自行配置适合你项目的环境构建流：

新建 /gulpfile.js/env/my-pipline.js

```javascript
module.exports = {

    // 暴露 fn 出去，就能声明一个 my-pipline gulp task 了。
    fn: gulp.series(
        // ...
    ),
};
```

然后使用 `gulp my-pipline` 或者 `beautywe run my-pipline` 就能运行自定义的任务了。

### /config

#### index.js

该文件是存放的是所有构建任务的配置信息的地方，你可以参考某一个构建任务的源码来修改某一项配置。

### clean.js

清除文件与文件夹

通过修改 `gulpfile.js/config/index` 的 `conf.clean` 来进行配置

### copy.js

拷贝文件与文件夹

通过修改 `gulpfile.js/config/index` 的 `conf.copy` 来进行配置

### image-min.js

压缩图片

通过修改 `gulpfile.js/config/index` 的 `conf.imageMin` 来进行配置

### index.js

构建任务的主入口文件，负责把 `gulpfile.js/` 目录中的构建任务给加载到 gulp 中

### json-compile.js

#### 可编程的 json 文件 {docsify-ignore}

在微信小程序中存在三种 json 文件：
* app.json
* page.json
* component.json

我们希望能给 json 文件提供可编程的能力。    
例如实现开发一套组件示例页面，只在开发和测试环境中可用，在发布构建的时候，能清理掉这部分路由。
如果 `app.json` 能可编程化的话，就更好了。

src/app-json.js
```javascript
const _ = require('lodash');
const config = require('./config');

module.exports = {
    pages: _.values(config.routes),
    window: {
        backgroundTextStyle: 'light',
        navigationBarBackgroundColor: '#fff',
        navigationBarTitleText: 'BeautyWe App',
        navigationBarTextStyle: 'black',
    },
};
```

代码执行环境是 Node.js （所以这里你能使用所有 Node.js 的能力），最后会构建出 `dist/app.json`

#### 可 import 的 json 文件 {docsify-ignore}

在微信小程序中，由于不支持像 Node.js 那样 import 一个 json 文件：

```javascript
// 微信小程序不支持这种引入
import config from 'config.json';
```

在实际的项目开发中，会有把配置信息统一放到一块地方管理的述求。    
所以我们通过把 json 文件编译成 CommonJS 的 js 文件，来达到这种目的。    
例如：

`src/config/index.js` 转换成 `dist/config/index.js`

```javascript
module.exports = {
    "version": "0.0.1",
    "env": "development",
    "appid": "wx6740f8a0f88af0df",
    "name": "beautywe-framework-test-app",
    "routes": {
        "home": "pages/home/index"
    }
};
```

然后我们在小程序代码中，就能 import 这个配置文件了：

```javascript
import config from './config/index';
```

#### 内置的 json-compile 规则 {docsify-ignore}

beautywe-framework 对于 json 内置了默认的构建规则：
1. 构建 `src/config/index.js` 文件到 `dist/config/index.js`
2. 构建 `src/app-json.js` 文件到 `dist/app.json`

当然，你可以通过修改 `gulpfile.js/config/index.js` 中的 `conf.jsonCompile` 来修改或增加自己的构建逻辑

### npm.js

npm task，使得你能够使用 node_modules 的库。    
它的工作流程主要是把 `src/npm/index.js` 通过 webpack 打包到 `dist/npm/index.js` 中去。

src/npm/index.js
```javascript
import beautywe from '@beautywe/core';

module.exports = {
    beautywe,
};
```

dist/npm/index.js
```javascript
// webpack bundled code
```

这种实现方式的主要考虑：
1. 实现简单
2. 统一管理 npm 的引入，应当谨慎引入第三方库，并且时刻关注代码量（由于微信小程序 4M 代码限制）
3. 能够更简单直接的关注 npm 包的总体大小：`$ ll dist/npm/index.js`

### sass-min.js

在 `gulp sass` 的基础上，增加样式压缩的构建。

### sass.js

提供 scss 编译功能，默认规则是：项目中 `*.scss` 文件转换到 `*.wxss`.

当然，你可以通过修改 `gulpfile.js/config/index.js` 中的 `conf.sass` 来进行配置

### scripts-min.js

在 `gulp scripts` 的基础上增加代码压缩（uglify）的构建。

### scripts.js

通过 babel 转换 js 文件。

当然，你可以通过修改 `gulpfile.js/config/index.js` 中的 `conf.scripts` 来进行配置

### watch.js

开发模式使用，对项目中的文件进行监控，修改后实时构建。

## /pages

项目页面存放这里

## app-json.js

会通过 `gulp json-compile` 构建任务，构建到 `dist/app.json`。
在该文件中，你可以尽情的使用 Node.js 的所有能力。

具体说明看：[gulpfile.js/json-compile.js - 可编程的 json 文件](#可编程的-json-文件)

## app.js

小程序的入口文件

## app.scss

小程序的全局性样式文件，支持 scss 预发，通过构建任务 `gulp sass` 构建到 `dist/app.wxss`

## project.config.json

给 微信开发者工具 看的项目配置工具，由于我们已经实现了 js 的 to ES5 转换，所以 IDE 不用再重复构建。
否则可能导致不可预测的错误。

## .eslintrc

BeautyWe Framework 集成了 [eslint](https://eslint.org/) ，并且使用 [airbnb](https://github.com/airbnb/javascript) 为基础的 js 编写规范。

## .gitignore

是的，BeautyWe Framework 也内置了默认的 git ignore 规则