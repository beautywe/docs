# 编写

BeautyWe 会对 [宿主](contents/core/the-host.md)(App/Page) 进行「可插件化」处理，经过这一步骤，能把宿主多种能力开放给插件。

插件的能力可以这样分类：

1. 扩展宿主数据：Data，对应 `plugin.data`
2. 扩展宿主原生钩子：Native Hook，对应 `plugin.nativeHook`
3. 扩展宿主事件监听钩子：Handler Hook，对应 `plugin.handler`
4. 提供自定义的 API，供宿主调用，对应 `plugin.custeomMethod`

所有 BeautyWe 插件都是一个 object，你可以这样创建一个插件：

```javascript
const myPlugin = {
    // 插件名
    name: 'myPlugin',

    // 存放你的 data，会合并到 theHost.myPlugin.name
    data: {
        name: 'myPlugin',
    },

    // 原生生命周期钩子，会混合到 theHost.onShow
    nativeHook: {
        onShow() {

        },
    },

    // 视图层事件监听，会混合到 theHost.onClick
    handler: {
        onClick(event) {
            // 处理你的逻辑
        },
    },

    // 自定义方法，会合并到 theHost.myPlugin.sayHello
    customMethod: {
        sayHello() {
            console.log('Hello, I am MyPlugin');
        },
    },

    // 插件装载前的钩子
    beforeAttach({ theHost }) {
        console.log(`plugin(myPlugin) will be attaching`, { theHost });
    },

    // 插件装载完的钩子
    attached({ theHost }) {
        console.log(`plugin(myPlugin) was attached`, { theHost });
    },

    // 插件初始化方法，会在宿主启动的时候执行
    initialize({ theHost }) {
        console.log(`plugin(myPlugin) has initialized`, { theHost });
    },
};
```

然后我们就可以使用上面创建的 `myPlugin` 了：

```javascript
const myPage = new BtPage({
    onLoad() {
        this.myPlugin.sayHello();
        // 输出：Hello, I am MyPlugin

        console.log(this.data.myPlugin.pluginName);
        // 输出：My Plugin
    },
});

myPage.use(myPlugin);

Page(myPage);
```

如果你使用 `beautywe-cli` 的话，我们提供了两种快速创建插件的方式：

1. 单文件模式: [beautywe new plugin](contents/cli.md#new-plugin)
2. NPM 项目模式: [beautywe new plugin-module](contents/cli.md#new-plugin-module)
