
## Step1: 下载
```
ynpm i @youzan/beautywe
```

## Step2: 引入

### Options 1: 拷贝 beautywe.min.js 到项目中

你可以把 `node_modules/@youzan/beautywe/beautywe.min.js` 文件拷贝到你的项目中，然后像这样来使用 BeautyWe：

```javascript
import BeautyWe from './beautywe.min.js';
```

### Options 2: 使用 BeautyWe Framework 的 NPM 功能

在我们的 **Beautywe Framework** 中有集成 NPM 的解决方案，在该方案下，你可能会像这样引入 BeautyWe：

```javascript
import { BeautyWe } from './libs/npm/index';
```

更多 NPM 的使用方法，请参考：[《 BeautyWe FrameWork - 构建 - NPM 》]()

## Step3: 改造 app.js

```javascript
import { BeautyWe } from './libs/npm/index';

// 构建 BtApp 实例
const myApp = new BeautyWe.BtApp({
  onLaunch() {
    console.log('on app run');
  }
});

// 使用原生的 App 方法
App(myApp);

```

## Step4: 使用插件能力

```javascript
import event from '@youzan/beautywe-plugin-event';

// using event plugin
myApp.use(event());

// now you can listen and trigger an event
myApp.on('hello', (msg) => console.log(msg));
myApp.trigger('hello', 'I am jc');
```

更多的官方插件看：《官方插件》

