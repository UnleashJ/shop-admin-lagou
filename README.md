# 代码规范与`ESLint`
## 安装与初始化

```shell
npm install eslint --save-dev
```

初始化 `ESLint` 配置，并根据提示进行选择，生成配置文件

```
npx eslint --init
```

详细配置可参考[vue-eslint-plugin](https://eslint.vuejs.org/)



## 配置 git commit hook

使用[lint-staged](https://github.com/okonet/lint-staged#readme)与[Husky](https://github.com/typicode/husky)在代码提交前（`git commit` 前），进行`ESLint`的规范校验。



## [vite-plugin-eslint](https://github.com/gxmari007/vite-plugin-eslint) 
安装`vite-plugin-eslint`插件，在`vite.config.ts`中进行配置（详见官网）。在开发和构建时，当`ESLint`检测出代码规范问题，可以在控制台中和浏览器页面中显示出来。



## git commit 提交规范

- [commitlint](https://github.com/conventional-changelog/commitlint)：验证 git commit 日志是否符合规范
- [Commitizen](https://github.com/commitizen/cz-cli)：辅助编写符合 git commit 规范的工具

commitlint Add hook

```shell
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "\${1}"'
```

