# vue 前端项目技术选型
- 主架构：vue, vue-router, vuex
- UI框架：element-ui
- 开发工具：vue-devtools, vue-loader
- 插件库： vee-validate, v-charts
- 代码检测修复： ESLint

# 1. 架构选型演进
1. 如果页面比较简单，可以只用 vue
2. 如果需要本地路由功能，比如在单页面应用（SPA）中维持多个页面，并且可以本地控制路由跳转逻辑，这时就需要搭配使用 vue-router
3. 一般稍复杂的页面都会遇到一些问题：组件之间的通信问题（比如 A 组件想要改变 B 组件的数据）、跨组件数据储存与共享问题（比如多页面购物车数据存储）。vue 本身并不能很好的解决这个问题，需要搭配使用 vuex

# 2. UI 框架选型
使用一个现成的 UI 框架，可以少写很多代码。

目前比较推荐的是：

- element-ui：我司很多项目在用的、饿了么出品的UI 框架
- iView: 阿里百度等大公司在用、主要服务于 PC 界面的中后台产品

# 3. 开发工具

## 3.1 vue-devtools
专门针对 vue 组件开发的 chrome 开发者工具插件，就像开发者工具的 Elements 一样，可以查看整个页面的 vue 组件树和每个组件的 data，并且可以动态的更改 data，然后会更新 UI 到应用上。

## 3.2 vue-loader
加载 .vue 单文件组件的 webpack loader。

# 4. 插件库
一些很实用的插件库：

- vee-validate：表单校验组件，可自定义校验规则
- v-charts：echarts 基于Vue封装的echarts组件，使用方便

# 5.代码检测修复
ESLint 文档非常详细，具备代码风格检查，自定义插件扩展功能。

优点：

- 默认规则里面包含了JSLint和JSHint的规则，易于迁移
- 可配置为警告和错误两个等级，或者直接禁用掉
- 可以自定义规则
- 可以根据错误定位到对应的规则


