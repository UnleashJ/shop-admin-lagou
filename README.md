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

# 基本配置
## 配置模块路径别名
在 `vite.config.ts` 中配置路径别名，这样项目中就可以使用`@/`导入`src/`目录下的模块 。

这样配置后，项目运行虽然没有问题，但是ts校验仍然会报错找不到相应的模块，需要在`tsconfig.json`中添加相应的配置。



## 配置scss全局变量

```js
... vite.config.ts
css: {
    preprocessorOptions: {
        scss: {
            additionalData: `@import "@/styles/variables.scss";`
        }
    }
}
...
```



### 配置axios

通过`axios.create`创建出来的实例 request不支持泛型。虽然get post put等请求方法支持响应数据泛型，可后端可能又对数据进行包装，导致我们访问的数据比较麻烦，所以我们封装一个支持泛型的request。

```typescript
export default async <T = any> (config: AxiosRequestConfig) => {
  const res = await request(config)
  return res.data.data as T
}

```



## [环境变量和模式](https://vitejs.cn/guide/env-and-mode.html)

查看Vite官网进行配置。

智能提示，可以在 `src` 目录下创建一个 `env.d.ts` 文件，接着按下面这样增加 `ImportMetaEnv` 的定义。

```typescript
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_API_BASEURL: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}

```



## 跨域解决方案

### 在接口服务器开启`CORS`

一般生产上线的代码会使用CORS。

```js
// 响应头
access-control-allow-credentials: true
access-control-allow-headers: Authorization, Content-Type, If-Match, If-Modified-Since, If-None-Match, If-Unmodified-Since, X-Requested-With, Form-type
access-control-allow-methods: GET,POST,PATCH,PUT,DELETE,OPTIONS,DELETE
access-control-allow-origin: http://127.0.0.1:5173
```

### 服务器代理

