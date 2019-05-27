# 项目规范

!> 这是一份供参考的项目规范原则，尽管 BeautyWe Framework 会对一些规范进行工具性的预设，但是都是默认关闭的。    
然后，你们的项目可以有自己的 style。

道路千万条，规范第一条。    
规范的终极愿景是：

>「无论多少人写的代码，看起来都像一个人写的」

## 文件与目录

1. 无论新建页面还是组件，目录为组件名或者页面名，而 js,wxml,scss,json 文件统一命名为 index，如 welcome 页面：
    - welcome/index.js
    - welcome/index.wxml
    - welcome/index.scss
    - welcome/index.json

2. 文件和文件夹的命名，全小写，多单词使用 - 链接，如：
    - components/global-view/

> [为什么文件名要小写？](http://www.ruanyifeng.com/blog/2017/02/filename-should-be-lowercase.html)

## 版本号

如果你们没有一套很好的自定义版本号概念，可以使用 [SemVer](https://semver.org/) 规范。

大概：

<主版本号>.<次版本号>.<修订号>

- 主版本号：当你做了不兼容的 API 修改，
- 次版本号：当你做了向下兼容的功能性新增，
- 修订号：当你做了向下兼容的问题修正。

## JS 代码

[「Airbnb JavaScript Style Guide」](https://github.com/airbnb/javascript) 是一套很值得参考的规范，并且配合 [「ESLint」](https://eslint.org/) 能很好地强制规范代码风格。

对于 JS 规范，BeautyWe Framework 预设了以下内容：
1. `.eslintrc`： 基于 Airbnb 的风格，预设了一套适合微信小程序开发的规则，[详情](https://github.com/beautywe/framework/blob/master/templates/app/.eslintrc)。
2. `npm run lint`：对比已被修改的文件，是否符合 eslint 规范。
3. pre-commit validation：监听 git commit hook，检查修改的文件是否符合规范。

**打开 pre-commit validation**:

pre-commit validation 功能是默认关闭的，可以修改 `/.huskyrc.js` 文件打开该功能：

```javascript
module.exports = {
    'hooks': {
        // Eslint validate 
        "pre-commit": "npm run lint",
    },
};
```

!> 注意，如果你是在 `git init` 之前就 `npm i`，[husky](https://github.com/typicode/husky) 会无法正常工作，需要重新 `npm i husky`，详情：[hooks not work if husky installed before git init](https://github.com/typicode/husky/issues/296) 
 
## Git Commit Log

#### Commit log 规范有什么好处？

这里引用两段：

By Conventional Commits: [为什么使用约定式提交](https://www.conventionalcommits.org/zh/v1.0.0-beta.3/#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%BD%BF%E7%94%A8%E7%BA%A6%E5%AE%9A%E5%BC%8F%E6%8F%90%E4%BA%A4)

> 1. 自动化生成 CHANGELOG。
2. 基于提交的类型，自动决定语义化的版本变更。
3. 向同事、公众与其他利益关系者传达变化的性质。
4. 触发构建和部署流程。
5. 让人们探索一个更加结构化的提交历史，以便降低对你的项目做出贡献的难度。

By 阮一峰：[Commit message 的作用](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

> 1. 提供更多的历史信息，方便快速浏览。
2. 可以过滤某些commit（比如文档改动），便于快速查找信息。
3. 可以直接从commit生成Change log。

BeautyWe Framework 对于 git commit log 的规范也做了一些预设：
1. 引入 [commitlint]() ，基于 [config-conventional]() 预设。
2. `npm run cm`：基于 [commitizen](https://github.com/commitizen/cz-cli) 快速创建符合规范的 commit log。    
3. `commit-msg validation`：监听 git commit msg hook，在 `git commit` 的时候，检查 commit log 是否符合规范。

**打开 commit-msg validation**:

commit-msg validation 功能是默认关闭的，可以修改 `/.huskyrc.js` 文件打开该功能：

```javascript
module.exports = {
    'hooks': {
        // Commit msg validate
        "commit-msg": "commitlint -E HUSKY_GIT_PARAMS",
    },
};
```

!> commit-msg validation 依赖 package.json 中的 `commitlint`, `config.commitizen` 字段，如果要使用这个功能，除非你知道自己在干什么，不然请勿删除