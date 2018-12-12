# 功能
- 组件
- 指令

# 依赖
- bootstrap@^4.1.3

# 使用
该组件库从**运维管理平台**衍生，开发人员视项目需求使用、弃用、添加及修改（注意保持风格统一、文档完整清晰）。
>弃用应删除组件文件夹，以及默认在main.js中的引用代码
- 组件
  - [h-table](./table.md)
  - [h-pagination](./pagination.md)
  - [h-echarts](./echarts.md)
- 指令
  - clickoutside
  - resize
- 引入
  ```js
  import Vue from 'vue'

  // ~代指相对路径
  import hView from '~/hView'

  // hView中组件的前缀默认为 h，可通过options配置，如配置前缀为 hso，则：
  Vue.use(hView, { prefix: 'hso' })
  ```