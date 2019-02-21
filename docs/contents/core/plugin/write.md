# 编写

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

然后我们就可以使用上面创建的 `myPlugin` 了：

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

如果你使用 [beautywe-cli]() 的话，我们提供了两种快速创建插件的方式：

1. 单文件模式
2. NPM 项目模式

## 单文件模式

```
$ beautywe new plugin <name> [dir]
```

运行下面命令

```
$ beautywe new plugin my-plugin

[beautywe] › ▶  start     创建插件：my-plugin
[beautywe] › ✔  success   生成文件：/my-plugin.js
[beautywe] › ☒  complete  创建插件完成
```

就会在当前目录创建 `./my-plugin.js`: 

```javascript
import { beautywe } from '../../npm/index';
const { BtPlugin } = beautywe;

module.exports = function plugin(options) {
    // 这里可以通过 options 做可配置化逻辑。

    return new BtPlugin({
        name: 'my-plugin',

        // 存放你的 data，会合并到 theHost.my-plugin.name
        data: {
            name: 'my-plugin',
        },

        // 原生生命周期钩子，会混合到 theHost.onShow
        nativeHook: {
            onShow() {

            },
        },

        // 视图层事件监听，会混合到 theHost.onClick
        handler: {
            onClick(e) {

            },
        },

        // 自定义方法，会合并到 theHost.my-plugin.sayHello
        customMethod: {
            sayHello() {
                console.log('Hello!');
            },
        },
    });
};
```

## NPM 项目模式

```
$ beautywe new plugin-module
```

运行命令，回答几个问题，就能快速创建一个 NPM 插件模块：

```
$ beautywe new plugin-module

? pluginName: my-plugin
? moduleName: @youzan/beautywe-plugin-my-plugin
? desc: Just my plugin
? version: 0.0.1
? 这样可以么: 
{
    "pluginName": "my-plugin",
    "moduleName": "@youzan/beautywe-plugin-my-plugin",
    "desc": "Just my plugin",
    "version": "0.0.1"
}
 Yes
[beautywe] › ▶  start     开始创建插件模块：@youzan/beautywe-plugin-my-plugin
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/.babelrc
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/.eslintignore
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/.eslintrc
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/.npmignore.disable
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/README.md
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/package.json
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/src/plugin.js
[beautywe] › ✔  success   生成文件：/beautywe-plugin-my-plugin/test/plugin.test.js
[beautywe] › ✔  success   插件模块已创建完成
```

项目中集成了 **eslint 规范**、**commit 规范**、**单元测试**、**测试覆盖率** 等内容，你只需编写最关键的插件代码

更多的 beautywe-cli 介绍见：[《beautywe-cli》]()
