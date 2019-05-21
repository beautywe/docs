# 全局 Page , Component

与全局窗口不一样，我可能需要每一个页面或者每一个组件，都实现一些相同的逻辑。    
例如，每一个页面，都引入 `@beautywe/event` 插件：

```javascript
import { beautywe } from '/npm/index';
import event from '/libs/plugins/event';

const page = new beautywe.BtPage();
page.use(event);

Page(page);
```

每一个页面，都要写这样的代码，感觉很繁琐。    
特别是全局性的逻辑多了话，每次新建页面都要写一次，维护的时候都要改一次，这简直是噩梦。

所以可以这样写：

`/src/pages/helloworld/index.js`:    

```javascript
import MyPage from '../../libs/my-page';

MyPage({
    onLoad() {
        // the demo just for show
        console.log('Wellcome to BeautyWe.js !');
    },
});
```

`/src/libs/my-page.js`:    

```javascript
import { beautywe } from '../npm/index';
import event from '../plugins/event';

const { BtPage } = beautywe;

export default function (wxPage) {
    const myPage = wxPage instanceof BtPage ? wxPage : new BtPage(wxPage);

    // do your global logic for page here
    wxPage.use(event);

    Page(myPage);
}
```

页面的所有全局逻辑，都往 `my-page.js` 里面搁就行了。

!> 自定义组件的全局逻辑，往 `/src/libs/my-component.js` 里面搁，跟 `my-page.js` 同理。

!> 我们同样可以通过 [BeautyWe Cli 提供的快速创建功能](/contents/framework/concept/quick-create.md)，把 page 和 component 这部分的相关代码写好，每次新建页面就不用手动写一遍了。