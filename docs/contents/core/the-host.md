
# 宿主

原生的微信小程序开发框架，给我们提供了三种抽象：
* 应用：App
* 页面：Page
* 组件：Component

**BeautyWe** 对其中两种抽象分别提供了两个类：
* 应用：BtApp
* 页面：BtPage

在 **BeautyWe** 的设计哲学中，它们会被统一称为**「宿主(The Host)」**。    
**BeautyWe** 提供了很多强有力的内容，前提都是基于构建三种宿主的实例来获取这些能力：

```javascript
import { BtApp, BtPage } from '@beautywe/beautywe';

// in app.js
const app = new BtApp({...});
App(app);

// in xxx/page.js
const page = new BtPage({...});
Page(page);

```

**BeautyWe** 绝大部分的能力，被分割成一块块的插件，你可以通过 `theHost.use()` 来选择你喜欢的插件来使用：

```javascript
import { BtApp } from '@beautywe/beautywe'; 
import event from '@beautywe/beautywe-plugin-event';

const app = new BtApp({..});
app.use(event());
App(app);

```

你可以从[《插件》](contents/core/plugin/use.md)来了解如何使用插件，运行原理，以及编写自己的插件。  