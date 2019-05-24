
# Quick Start

## 下载

把 [beautywe.min.js](https://unpkg.com/@beautywe/core@1.0.0/dist/beautywe.min.js) 文件拷贝到你的项目中，然后引入 BeautyWe：

```javascript
import beautywe from './beautywe.min.js';
```

## 使用

**for app**
```javascript
import { BtApp } from './beautywe.min.js';

// 构建 BtApp 实例
const myApp = new BtApp({
  onLaunch() {
    console.log('on app run');
  }
});

// 使用原生的 App 方法
App(myApp);
```

**for page**
```javascript
import { BtPage } from './beautywe.min.js';

// 构建 BtPage 实例
const myPage = new BtPage({
  onLoad() {
    console.log('on page run');
  }
});

// 使用原生的 Page 方法
Page(myPage);
```

## 使用插件


### 外部插件
```javascript
import event from '@beautywe/plugin-event';

// using event plugin
myApp.use(event());

// now you can listen and trigger an event
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```

> 更多的第三方插件：[npm beautywe plugins](https://www.npmjs.com/search?q=keywords:beautywe-plugin)

### 自定义插件
```javascript
myApp.use({
  onLoad() {
    console.log('my plugin run');
  },
});
```

> 如何编写插件：[插件 - 编写](contents/core/plugin/write.md)


