
## Step1: 下载
```
npm i @beautywe/core
```

## Step2: 引入

### Options 1: 拷贝 beautywe.min.js 到项目中

你可以把 `node_modules/@beautywe/core/beautywe.min.js` 文件拷贝到你的项目中，然后像这样来使用 BeautyWe：

```javascript
import beautywe from './beautywe.min.js';
```

### Options 2: 使用 BeautyWe Framework 的 NPM 功能

在我们的 [**Beautywe Framework**](contents/framework/introduce.md) 中有集成 NPM 的解决方案，在该方案下，你可能会像这样引入 BeautyWe：

```javascript
import { beautywe } from './npm/index';
```

### Options 3: 使用小程序自带的 NPM 功能

从小程序基础库版本 2.2.1 或以上、及开发者工具 1.02.1808300 或以上开始，小程序支持使用 npm 安装第三方包。

详情看微信小程序官方文档：[npm 支持](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html?search-key=npm)


## Step3: 改造 app.js

```javascript
import { beautywe } from './libs/npm/index';

// 构建 BtApp 实例
const myApp = new beautywe.BtApp({
  onLaunch() {
    console.log('on app run');
  }
});

// 使用原生的 App 方法
App(myApp);

```

## Step4: 使用插件能力

```javascript
import event from '@beautywe/plugin-event';

// using event plugin
myApp.use(event());

// now you can listen and trigger an event
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```

更多的插件看：[npm beautywe plugins](https://www.npmjs.com/search?q=keywords:beautywe-plugin)

