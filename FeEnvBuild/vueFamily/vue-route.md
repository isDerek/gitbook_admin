# 3.1.Vue-Route

---

Vue-Route 是路由导航，什么是路由导航，通俗来讲就是讲网站输入的 URL 地址定位到导向某个页面。Vue 路由的默认内容如下图所示。

```
import Vue from 'vue'
import Router from 'vue-router'
import Home from './views/Home.vue'

Vue.use(Router)

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    },
    {
      path: '/about',
      name: 'about',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
    }
  ]
})
```

在这里要对路由进行修改，初步定义路由的页面有两个，登陆页和首页，\* 代表通配符，当访问其它路径的时候默认进入登陆页面。History 模式，取消默认的 Hash 模式。Hash 模式会在 URL 路径后添加个 #，用户只允许改变 # 后的 URL 片段，而 History 给了用户充分的自由，但同时会出现的问题是，若用户刷新页面，History 是实实在在的去请求服务器资源，若没有的到响应会生成 404 错误页面，而 Hash 则不会。

```
const router = new Router({
  mode: 'history', //取消默认的 hash 模式 #
  routes: [
    { path: '/login', name: 'login', component: Login },
    { path: '/home', name: 'home', component: Home },
    { path: '*', name: 'login', component: Login }
  ]
})
```

在此注意 Vue 程序的运行流程,在入口文件 main.js 引入 router 模块，用户就能通过路由导航去访问对应的页面（组件），打开程序入口文件 main.js ，如下图所示

```
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```

正如上图所示，这是程序的入口文件，所以要添加模块可在该文件中进行添加，添加的内容如下:<br>
I.复位 CSS 文件<br>
为了让默认的 CSS 样式清空，避免默认样式影响到了界面 UI。

```
import './assets/styles/reset.css'
```

II.element-ui 文件<br>
element-ui 是网页前端的 UI 库，引入该文件可以使用多种美观的样式组件

```
import Element from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(Element,{size:'small',zIndex:3000});
```

III.axios 库<br>
Axios 是 AJAX 封装的 Http 库，支持 Promise 对象的异步请求

```
import axios from 'axios'
```
