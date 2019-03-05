# 使用

[Class BtApp]()、[Class BtPage]() 都继承自 [Class Host]() 。    
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

// use event plugin
app.use(event());

// 之后便能使用该插件提供的功能
myApp.event.on('hello', (msg) => console.log(msg));
myApp.event.trigger('hello', 'I am jc');
```