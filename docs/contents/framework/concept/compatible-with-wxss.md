# scss 与 wxss 的兼容

wxss 与 scss 都支持 `@import` 命令，如果简单进行 scss 构建，会造成冗余。

例如有以下 scss 文件：

```css
/* fn.scss */
.container {
    background: '#fff'
}

/* a.scss */
@import "./fn.scss"
.my-class {
    color: red;
}

/* b.scss */
@import "./fn.scss"
.my-class {
    color: blue;
}
```

那么通过直接的 sass 构建结果会这样：

```css
/* fn.scss */
.container {
    background: '#fff'
}

/* a.scss */
.container {
    background: '#fff'
}

.my-class {
    font: red;
}

/* b.scss */
.container {
    background: '#fff'
}

.my-class {
    font: blue;
}
```

既然 wxss 是支持 `@import` 命令的，那么这样的构建结果，就会造成冗余。

Beautywe Framework 通过 `gulp sass` 任务，遇到 `@import` 命令，会默认跳过，不进行 sass 的编译。

如果遇到需要编译的文件，如:
1. 通常存放变量的 ```@import "style/global-variable.scss"```
2. 集合方法的 ```@import "style/mixin.scss"```    
...

可以在 `gulpfile.js/config/index.js` 中注册这些文件：

```javascript
conf.sass = {
    whiteListForImport: [
        'style/mixin.scss',
        'style/global-variable.scss'
    ],
};
```

那么这些文件在 sass 构建的过程中就会被编译。