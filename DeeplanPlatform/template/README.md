<p align="center"><a href="http://www.howso.cn/" target="_blank" rel="noopener noreferrer"><img width="100" src="https://gss1.bdstatic.com/-vo3dSag_xI4khGkpoWK1HF6hhy/baike/w%3D268/sign=4d5817734834970a47731729adcbd1c0/1ad5ad6eddc451da6440d3b7bffd5266d016323c.jpg" alt="howso logo"></a></p>
<h2 align="center">Deeplan Platform Template</h2>

# 项目介绍
该项目是为Deeplan平台项目[（svn地址）](https://192.168.0.73/svn/Deeplan%E5%A4%A7%E5%B9%B3%E5%8F%B0/trunk/code/front/platform)定制的Vue模板，旨在封装重复轮子、统一开发规范、力求最佳实践。
>平台项目提供头部、导航栏、单点登录页、项目切换栏（使用iframe引入）。为保证项目开发、部署的灵活性，前端使用[postMessage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)实现跨源通信。建议平台和项目之间仅做必要的沟通，这对平台降耦，提高通用性具有意义。

# 运行打包
```bash
# install dependencies
npm install

# serve with hot reload at localhost:8081
npm run dev

# build for production with minification
npm run build
```

# 开发指南
- Style
  - 语言：[SCSS](https://www.sass.hk/)
  - 连字符：短横线(`-`)
  - 样式库：[定制bootstrap4](https://getbootstrap.com/docs/4.1/getting-started/theming/)
  - 全局样式：`@/styles`文件
  - 局部样式：写于`.vue`的`<style>`，注意避免css覆盖
    - （推荐）使用类名`<页面>-page`包裹，如：用户管理页面`userMng.vue`中，使用`user-mng-page`包裹
    - 添加`scoped`

- [Axios](https://www.kancloud.cn/yunye/axios/234845)

  在`@/axios`文件下
  - apis.js记录接口信息，帮助开发人员减轻调用接口的思维负担，更多得关注业务与交互

    记录方式：
    ```js
    // 显然，const后的命名api不是固定的，而且必须唯一，以保证每条接口信息身份唯一
    export const api = []
    ```
    参数|说明|类型
    -------|-|-
    api[0] |参考axios请求方式配置项method|String
    api[1] |参考axios请求路径配置项url|String
    api[2] |有5个可配置项，详见以下5行|JSON
    load   |请求时是否需要loading层，实际是通过控制全局状态`loadNum`间接控制loading框显隐|Boolean
    param  |接口自动获取全局状态，例：`{ userNick: state => state.userInf.nickName }`，`state`是`$store.state`的形参|JSON
    code   |判断接口调用是否正常的状态码，默认200，空对象`null`表示不需要校验|Number/null
    codeErr|code码校验不通过时的回调|Function
    reject |调用接口抛错时的回调（不要与codeErr混淆）|Function
    api[3] |补充、覆盖index.js中axios实例，参考axios配置项|JSON

  - index.js封装Axios，暴露为全局变量`ax`使用

    使用示例：
    ```js
    // .vue文件
    methods: {
      async apiName => {
        // ax(apiKey, params, apiCfg, axiosCfg)使用示例
        this.userInf = await ax('getUserInf')
      }
    }
    ```
    参数|说明|类型
    --------|-|-
    apiKey  |选用接口，对应apis.js中记录接口信息变量名|String
    params  |接口入参，形如`{ id: 1 }`|JSON
    apiCfg  |完全参考apis.js中记录接口信息配置的api[2]，且优先级更高。存在的意义：处理apis.js接口记录信息可能不包含的特殊情况|JSON
    axiosCfg|完全参考apis.js中记录接口信息配置的api[3]，且优先级更高。存在的意义：同上|JSON

- constant文件

  在项目中，有些值在多个文件中用到，且需要人为的保证值一致。往往修改一个地方，需要找到项目中其他地方，做重复的修改。

  抽取常量的好处在于通过降耦，提高开发效率和质量，且有助于整体理解掌控常量相关的业务。

- [vue-router](https://router.vuejs.org/zh/)

  与一般Vue项目唯一不同的是**路由配置由前端写定的改为动态获取后端的**，没有需要特别关注的，有兴趣可以了解下`afterEach`中有vuex的两个mutation提交，分别控制`route`、清零`loadNum`。

- [Vuex](https://vuex.vuejs.org/zh/guide/)

  在`@/store`文件下
  - state
    - `userInf`（用户信息）
    - `menu`（菜单权限）
    - `permissions`（功能权限）
    - `route`（当前路由）
    - `loadNum`（当前pending状态且需要loading加载框的请求数量）
  - actions
    - 获取应用信息（获取后端的 菜单权限、功能权限）
    - 退出（调用退出接口）

- style文件

  该文件是**全局样式**，回顾上面说过的**局部样式是写在`.vue`文件中的**。

  index.scss被引于webpack入口文件main.js，作为项目唯一引用的样式文件。其自身不写任何样式，只引入
  - 定制bootstrap4样式库
  - _reset.scss重置默认样式
  - global全局样式
  - elemHark组件库element的hark样式

  其中global文件中index.scss用于编写全局样式，及引入同目录细分的样式，如tool.scss（全局工具类）。

  开发人员在写全局样式时、请斟酌写于index.scss中还是新建类似tool.scss的文件进行细分。

- 组件库

  组件库选用我司常用的[Element](http://element-cn.eleme.io/#/zh-CN/component/input)，可能的话，尽量不要引入其他组件库，理由：
  - Element既称为库，是覆盖绝大多数场景所需的组件的，如果有**elem竟然没有这种常用组件**的感觉，也许是没留意，建议仔细查阅官网确认下
  - 有助于针对一个库做样式hark的积累和沿用

- framework/hView文件

  该文件是本模板中封装的组件库，开发人员视项目需求添加、修改，注意保持风格统一、文档完整清晰。
  - 依赖bootstrap@^4.1.3
  - 组件（具体参考组件文件内的`README.md`）
    - h-table
      ```html
      <!-- 示例 -->
      <h-table
        :data="getLongArr(data)"
        :column="column"
      ></h-table>
      ```
    - h-pagination
      ```html
      <!-- 示例 -->
      <h-pagination
        :total="total"
        :current="page"
        @jump="changePage" @changeSize="changeSize"
      ></h-pagination>
      ```
    - h-echarts
      ```html
      <!-- 示例 -->
      <h-echarts :option="option"></h-echarts>
      ```
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
# 开发流程

>基本准备

拷贝模板项目（[svn](https://192.168.0.73/svn/Deeplan%E5%A4%A7%E5%B9%B3%E5%8F%B0/trunk/code/front/tpl)）作为新项目模板（注意不要保留其svn信息），上传至新项目的svn地址。

进入项目根目录后，安装依赖，启动项目
```bash
# install dependencies
npm install

# serve with hot reload at localhost:8081
npm run dev
```

>step1 申请账号

前端开发人员向相关后端申请Deeplan平台账号（要求是**系统管理员**）。登录进**运维管理系统**，检查**角色**是否为**系统管理员**。

>step2 创建新项目

到**应用管理**模块，点击新增按钮新增应用，填写信息如下表
表单|注意
-|-
应用名称|-
应用编码|-
应用LOGO|-
首页地址|到端口号即可，如`http://192.168.10.81:8081`
备注|-

填好点击确认按钮，新增成功会有提示信息。刷新后切换到新应用（此时获取新应用的地址不保证是新建时所填写的地址），联系运维系统相关后端人员，帮新应用所有前端开发**在各自账号下配置对应前端人员的本机开发地址**。再次刷新，确认新应用地址是新应用在本机的开发地址。

>step3 新增菜单

切入运维管理系统的菜单管理模块，点击新增按钮，新增菜单:
表单|注意
-|-
类型|点选菜单
上级菜单|选择全部表示新增菜单为一级菜单；选择其他则新增菜单将嵌套在此上级菜单的`<router-view />`中
名称|-
菜单组件|填入组件路径要求是`@/vue/`的相对路径；为空则组件默认为`<router-view />`
菜单路径|框架设定所有路径都是vue-router的children中的路径，且对应vue-router的path配置，要求参考这两点信息即可
菜单图标|-
备注|-

按要求新增一个菜单后，需要在该菜单上设置至少一个（控制菜单为显示的）功能，这样后端接口逻辑才可能传出该菜单。

操作运维管理系统，赋予相关开发人员账号此菜单权限。

>step4 开始常规开发

刷新页面，确认新增菜单及对应的组件显示正常后，即可开始常规开发。