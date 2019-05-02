# 使用

`Class BtApp`、`Class BtPage` 都继承自 `Class Host` 。    
而 **Host.prototype.use** 方法实现了插件的注册。

```javascript
import event from '@beautywe/plugin-event';
import beautywe from '@beautywe/core';

// in app.js
const myApp = new beautywe.BtApp();
App(myApp);

// in xxx/page.js
const myPage = new beautywe.BtPage({...});
Page(myPage);

// use event plugin
app.use(event());

// 之后便能使用该插件提供的功能
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```