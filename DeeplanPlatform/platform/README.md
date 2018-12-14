# 项目描述
- 提供头部、导航栏
- 单点登录页、项目切换栏（iframe引入项目）

# 运行打包
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

# 开发指南
- Style
  - 语言：[SCSS](https://www.sass.hk/)
  - 连字符： `-`
  - 样式库：[定制bootstrap4](https://getbootstrap.com/docs/4.1/getting-started/theming/)
  - 全局样式： `@/styles` 文件
  - 局部样式：写于 `.vue` 的 `<style>` ，注意避免css覆盖
    - （推荐）使用类名`<页面>-page`包裹，如：

      用户管理页面 `userMng.vue` 中，使用 `user-mng-page` 包裹

      系统管理页面 `sysMng.vue` 中，使用 `sys-mng-page` 包裹
    - 添加 `scoped`

- [Axios](https://www.kancloud.cn/yunye/axios/234845)

  在 `@/axios` 文件下

  - `apis.js`

    >集中管理接口路径、请求方式等信息；帮助开发人员减轻调用接口的思维负担，更多关注业务及交互。具体参考注释

  - `index.js`

    >封装 `Axios`， 暴露为全局变量 `ax` 使用，具体参考注释
    ```js
    //使用示例
    methods: {
      async apiName => {
        this.userInf = await ax('getUserInf')
      }
    }
    ```

- [vue-router](https://router.vuejs.org/zh/)

  `vue-router` 没有需要关注的，有兴趣可以了解以下两点：

  - beforeEach的路由拦截，如有优化的建议，请联系相关前端小伙伴

  - afterEach中有两个vuex的mutation提交，控制 `route`，清零 `loadNum`

- [Vuex](https://vuex.vuejs.org/zh/guide/)

  在 `@/store` 文件下，有：

  - 包含退出的 `actions`

  - 全局状态

    `userInf` （用户信息）

    `loadNum` （当前状态为pending且需要loading加载框的请求数量）

    `route` （当前路由）

- `style` 文件

  `index.scss` 在 `webpack` 入口文件 `main.js` 中作为项目样式引入，其自身不写任何样式，只引入样式库、`reset`、项目全局样式。

  `global` 文件中 `index.scss` 写全局样式，也用于引入同目录其他细分的样式文件，如 `tool.scss` 用于编写工具类，前端开发写全局样式时请斟酌写于 `index.scss` 中还是新建 `scss`文件进行细分

- `constant` 文件

  记录vuex等常量。目的是降低耦合，便于修改和维护

- 组件库

  组件库使用[Element](http://element-cn.eleme.io/#/zh-CN/component/input)