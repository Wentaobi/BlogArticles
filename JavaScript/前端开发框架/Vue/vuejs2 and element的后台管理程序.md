## 示例一：[admin template based on vuejs2 and element](https://github.com/taylorchen709/vue-admin)
* demo: [https://taylorchen709.github.io/vue-admin/](https://taylorchen709.github.io/vue-admin/)
### To start
This is a project template for [vue-cli](https://github.com/vuejs/vue-cli)
```shell
# install dependencies
npm install

# serve with hot reload at localhost:8081
npm run dev

# build for production with minification
npm run build
```
### Theme
You can change theme by
* 1.Generate theme packages by https://elementui.github.io/theme-preview/#/
* 2.Put theme packages in src/assets/theme/
* 3.Edit src/main.js
```javascript
import 'element-ui/lib/theme-default/index.css'
to
import './assets/theme/your-theme/index.css'
```
* 4.Edit src/styles/vars.scss
## 示例二：[a vue project for admin](https://github.com/jerry9022/LitAdmin)
* 一个基于vue2.x编写的后端管理项目
* 这是一个用vuejs2.0和element-ui 2.x搭建的后台管理界面。 演示地址：[http://lit.ipyro.cn](http://lit.ipyro.cn)
* 源码地址：[https://github.com/jerry9022/LitAdmin](https://github.com/jerry9022/LitAdmin)
### 相关技术：
* [vuejs2.0](http://vuejs.org/)：一套构建用户界面的渐进式JavaScript框架，易用、灵活、高效。
* [element-ui](http://element.eleme.io/)：一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的组件库。
* [vue-router](http://router.vuejs.org/zh-cn/index.html)：前端路由，用Vue.js + vue-router 创建单页应用(SPA)非常简单。
* [axios](https://www.npmjs.com/package/axios): 基于 Promise 的 HTTP 请求客户端，可同时在浏览器和 node.js 中使用。
* [mock.js](http://mockjs.com/): 生成随机数据，拦截 Ajax 请求,让前端攻城师独立于后端进行开发。
