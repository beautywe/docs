# 插件

## 使用

[Class BtApp]()、[Class BtPage]()、[Class BtComponent]() 都继承自 [Class Host]() 。    
而 **Host.prototype.use** 方法实现了插件的注册。

```javascript
import event from '@youzan/beautywe-plugin-event';
import BeautyWe from '@youzan/beautywe';

// in app.js
const theHost = new BeautyWe.BtApp();
App(page);

// in xxx/page.js
const theHost = new BeautyWe.BtPage({...});
Page(page);

// in xxx/component.js
const theHost = new BeautyWe.BtComponent({...});
Component(component);

// use event plugin
app.use(event());

// 之后便能使用该插件提供的功能
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```

## 编写

所有 BeautyWe 插件都是 [BtPlugin]() 的实例，你可以这样创建一个插件：

```javascript
import BeautyWe from '@youzan/beautywe';
const myPlugin = BeautyWe.BtPlugin({
    name: 'myPlugin',

    // 存放插件的 data，会合并到 theHost.myPlugin.data
    data: {
        pluginName: 'My Plugin',
    },

    // 自定义方法，会合并到 theHost.myPlugin.sayHello
    customMethod: {
        say() {
            console.log(`Hello, I am ${this.data.myPlugin.pluginName}`);
        },
    },

    // 原生生命周期钩子，会混合到 theHost.onLoad
    nativeHook: {
        onLoad() {
            console.log('catch onLoad on myPlugin');
        },
    },

    // 视图层事件监听，会混合到 theHost.onClick
    handler: {
        onClick() {
            console.log('catch onClick event on myPlugin');
        },
    },
});
```

然后我们就可以使用 `myPlugin` 了：

```javascript
const page = new BtPage({
    onLoad() {
        this.myPlugin.say();
        // 输出：Hello, I am My Plugin

        console.log(this.data.myPlugin.pluginName);
        // 输出：My Plugin
    },
});

app.use(myPlugin);

Page(app);
```

如果你使用 [beautywe-framework]() 的话，我们还提供了两种快速创建插件的方式：

1. 单文件模式
2. 项目模式

详情请看：[《BeautyWe Framework - new plugin》]()

## 原理

插件的实现，是通过「混合(mixin)」，在 [宿主](contents/concept/the-host.md) 上进行扩展实现的。    
混合的过程会分为四部分：

* 数据: Data
* 自定义方法：Custom Method
* 原生钩子：Native Hook
* 事件处理：Handler

下面会一一讲解这四种混合方式的实现过程。

### 数据 Data
每个插件，在宿主的 data 中，都会有一个专有的命名空间：

```javascript
import event from '@youzan/beautywe-plugin-event';
import BeautyWe from '@youzan/beautywe';

// in app.js
const theHost = new BeautyWe.BtApp();
App(page);

// in xxx/page.js
const theHost = new BeautyWe.BtPage({...});
Page(page);

// in xxx/component.js
const theHost = new BeautyWe.BtComponent({...});
Component(component);

// use event plugin
app.use(event());

// 提供给插件使用的命名空间
theHost.data.event;
```

该功能，主要用于满足某些插件功能需要与视图层进行交互的场景。

### 自定义方法 Custom Method

### 原生钩子 Custom Hook

### 事件处理 Handler

## 其他
1. 命名冲突
2. 依赖检测
3. getApp in app lifecycle