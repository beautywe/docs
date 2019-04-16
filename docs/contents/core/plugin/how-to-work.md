# 原理

## 设计

## 混合


插件的是通过混合(mixin)，在[宿主](contents/core/the-host.md)上进行扩展实现的。    
混合的过程分四部分：

* 数据: Data
* 自定义方法：Custom Method
* 原生钩子：Native Hook
* 事件处理：Handler

四种混合的实现都是不一样的，下面会一一讲解这四种混合方式的实现过程。

### 数据 Data
每个插件，在宿主的 data 中，都会有一个专有的命名空间：

```javascript
import event from '@beautywe/beautywe-plugin-event';
import BeautyWe from '@beautywe/beautywe';

// in app.js
const theHost = new BeautyWe.BtApp();
App(page);

// in xxx/page.js
const theHost = new BeautyWe.BtPage({...});
Page(page);

// use event plugin
app.use(event());

// 提供给插件使用的命名空间
theHost.data.event;
```

该功能，主要用于满足某些插件功能需要与视图层进行交互的场景。

### 原生钩子 Native Hook

在 BeautyWe 中，你可以在插件中处理宿主的生命周期回调函数：

```javascript
const myPlugin = {
    nativeHook: {
        onLaunch(options) {
            // do your logic
        },
        onLoad() {
            // do your logic
        },
    }
};
```

并且支持多个插件与页面之间共同监听同一个生命周期钩子：

```javascript
const pluginA = {
    nativeHook: {
        onShow: onShowForPluginA(options) {
            // do your logic
            console.log('onShow on pluginA');
        },
    }
};

const pluginB = {
    nativeHook: {
        onShow: onShowForPluginB(options) {
            // do your logic
            console.log('onShow on pluginB');
        },
    }
});

const app = new BeautyWe.BtApp({
    onShow: originOnShow(options) {
        // do your logic
        console.log('onShow on the host');
    },
};

app.use([pluginA, pluginB]);

App(app);

// 当页面被载入，调用 app.onShow() 时，会是这样的输出：
// onShow on the host
// onShow on pluginA
// onShow on pluginB
```

甚至还支持以返回 Promise 的形式来对执行过程异步化

```javascript
const pluginA = {
    nativeHook: {
        onShow: onShowForPluginA(options) {
            // do your logic
            console.log('onShow on pluginA');
        },
    }
});

const pluginB = {
    nativeHook: {
        onShow: onShowForPluginB(options) {
            // do your logic
            console.log('onShow on pluginB');
        },
    }
});

const app = new BeautyWe.BtApp({
    onShow: originOnShow(options) {
        // do your logic

        return Promise
            .resolve()
            .then(() => console.log('fetching data'))
            .then(() => xxxAPI.fetch())
            .then(() => console.log('fetching data done'))
            .then(() => console.log('onShow on the host'))
    },
});

app.use([pluginA, pluginB]);

App(app);

// 当页面被载入，调用 app.onShow() 时，会是这样的输出：
// fetching data
// fetching data done
// onShow on the host
// onShow on pluginA
// onShow on pluginB
```


`plugin.nativeHook` 支持识别的钩子函数有：
``` javascript

// app
const APP_NATIVE_HOOKS = [
    'onLaunch',
    'onShow',
    'onHide',
    'onPageNotFound',
];

// page
const PAGE_NATIVE_HOOKS = [
    'onLoad',
    'onShow',
    'onReady',
    'onHide',
    'onUnload',
    'onPullDownRefresh',
    'onReachBottom',
    'onPageScroll',
    'onResize',
    'onTabItemTap',
];
```

### 事件处理 Handler

为满足插件可以实现与视图层的交互逻辑封装，除了给与插件 data 的能力，还需要给予事件处理的能力。    
你可以在插件中这样实现事件的监听：

```javascript
const pluginA = {
    handler: {
        onBtnClick(e) {
            // do your logic
        },
    }
};

const pluginB = {
    handler: {
        onBtnClick(e) {
            // do your logic
        },
    }
};

const page = new BeautyWe.BtPage({
    onBtnClick(e) {
        // do your logic
    },
});

// 多个插件和宿主都能实现同一个事件函数，实现原理与 Native Hook 一致。
page.use([pluginA, pluginB]);

Page(page);
```

### 自定义方法 Custom Method

custom method 是能让插件给用户提供一系列 API 的方式：

```javascript
const myPlugin = {
    name: 'myPlugin',
    data: {
        name: 'myPlugin',
    },
    customMethod: {
        hello() {
            // this 指向的是当前宿主实例
            console.log(`Hello, I am ${this.data.myPlugin.name}`);
        },
        international: {
            bonjour() {
                // this 依然指向的是当前宿主实例
                console.log(`Bonjour, je suis ${this.data.myPlugin.name}`);
            },

            nihao() {
                // this 依然指向的是当前宿主实例
                console.log(`你好, 我是 ${this.data.myPlugin.name}`);
            }
        }
    }
};

const page = new BeautyWe.BtPage({
    onLoad() {
        // 输出：Hello, I am myPlugin
        this.myPlugin.hello();
    }
});

page.use(myPlugin);

Page(page);
```

custom method 混合的大概过程如下：
1. 以插件名，在 page 增加一块命名空间：`page.myPlugin = {}`;
2. 按照 `customMethod` 的树桩结构，把函数绑定到 `page.myPlugin` 上面；

## 生命周期

* beforeAttach
* attached
* initialize