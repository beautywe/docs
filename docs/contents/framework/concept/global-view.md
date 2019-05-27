# 全局窗口

我们都知道微信小程序是「单窗口」的交互平台，一个页面对应一个窗口。    
而在业务开发中，往往会有诸如这种述求：

1. 自定义的 toast 样式
2. 页面底部 copyright
3. 全局的 loading 样式
4. 全局的悬浮控件    
......

稍微不优雅的实现可以是分别做成独立的组件，然后每一个页面都引入进来。    
这种做法，我们会有很多的重复代码，并且每次新建页面，都要引入一遍，后期维护也会很繁琐。

而「全局窗口」的概念是：**希望所有页面之上有一块地方，全局性的逻辑和交互，可以往里面搁。**

## global-view 组件

这是一个自定义组件，源码在 `/src/components/global-view`.

每个页面的 wxml 只需要在顶层包一层：

```html
<global-view id="global-view">
    ...
</global-view>
```

需要全局实现的交互、样式、组件，只需要维护这个组件就足够了。

!> `id="global-view"` 一定要加上，方便页面层获取到该组件的实例，与组件进行通讯。

## 获取全局窗口实例

BeautyWe Framework，提供了快速获取全局窗口实例的方法，方便与组件进行通讯。

```javascript
import { getGlobalView } from '/libs/utils/helper';

const globalView = getGlobalView();

// 调用全局窗口方法，展示全局性的 loading
globalView.showLoading();
```

## Quickly Created

我很懒，每创建一个页面写一句 `<global-view id="global-view"> ... </global-view>` ，都会觉得很繁琐。

所以，可以通过 [BeautyWe Cli 提供的快速创建功能](/contents/framework/concept/quick-create.md)，快速创建页面：

```shell
$ beautywe new page helloworld
```

其中生成的页面，就已经引入了 `<global-view>` 代码了

页面的模板代码在：`/.templates/page`