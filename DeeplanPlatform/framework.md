# 前端框架服务功能

- Style

    根据公司的样式标准，完成一套样式及其说明，可以简化前端人员样式上的工作。

    建议定制bootstrap，在其基础上做修改和补充。由于前端对bootstrap较熟悉，定制和使用起来比较得心应手。

- 封装请求

    公司Vue项目请求接口基本使用Axios，Axios是一个基于 promise 的 HTTP 库，特征有：

    * 支持 Promise API
    * 拦截请求和响应
    * 转换请求数据和响应数据

    根据接口规范，可以封装查询参数的解析和字符串化，如使用qs包(文档查询npm)。

    将接口信息记录以一定格式记录在某类文件中，在请求时自动获取和设置相关参数，简化前端调用接口的工作。

    规范接口code码含义，在请求中拦截处理“未登录”等情况。

- webpack配置

    公司项目基本使用webpack打包，但应该没人敢说把webpack研究透彻了，所以建议维护一套稳定的配置，将经过多次使用经得起推敲的配置封装起来，并注释详细说明。

- 代码检查

    根据公司前端代码检查规范，可以使用工具代替一部分人工检查，高效可靠，部分检查规则可以自动修复。
    JavaScript检测工具如：JSLint、JSHint、JSCS、ESLint：

    工具|描述
    -|-
    JSLint|古老，不可配置，不可扩展，不可禁用许多特性的校验
    JSHint|可配置的JSLint版本
    JSCS|代码样式检查，只捕获与代码格式化相关的问题，而不是潜在的bug或错误。已经与 ESLint 合并
    ESLint(推荐)|易于扩展，可自定义规则，可以插件形式安装更多的规则

- 组件库

    Vue项目要大量使用组件，使用比较多的组件库是Element。但是：

    - 样式不一致，解决：

        - 简单粗暴地写样式覆盖

        - 根据官方自定义主题的三个方案修改scss变量值

        - 更深度的修改需要修改element-ui\packages\theme-chalk\src里的scss文件

    - 有时需要手动封装其他功能的组件，但问题是如何组织编写样式及文档，以满足持续维护的目的。

    前端需要提供一套好用可维护、有可阅读性高的文档的组件库，存在的问题需要大家一起来商讨方案解决。
