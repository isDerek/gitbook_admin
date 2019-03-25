# 3.2.Vuex

---

Vuex 是状态管理模块，为了对项目的状态进行管理，例如 API 的请求捕捉，用户状态的管理等。
Vuex 分为 State(状态)、Mutations（变化）、Action (异步行为)
在项目中，通过 Vuex 分别对用户模块、设备模块、厂商模块进行管理，同时请求数据的 RESTFUL API 也由 Vuex 进行分配管理。需要注意的是，当项目中引入 Vuex，当在外部页面调用想改变 state 时，都必须提交 (commit) mutation 来进行改变。且 Vuex 是具备响应特性的，当 store 中的 state 发送变化，页面绑定有相关 state 的时候触发页面的更新。默认生成的 store 文件修改如下，将用户模块、设备状态、厂商模块、设备注册模块都引入进库里。

```
import Vue from 'vue'
import Vuex from 'vuex'
import deviceStatus from './modules/devicecontrol/deviceStatus'
import manufacturerInfo from './modules/basicinfo/manufacturerInfo'
import deviceRegister from './modules/devicecontrol/deviceRegister'
import deviceVersionInfo from './modules/devicecontrol/deviceVersionInfo'
import user from './modules/user/user'
Vue.use(Vuex)

export default new Vuex.Store({
  modules: {
        deviceStatus,
        manufacturerInfo,
        deviceRegister,
        user
  }
})
```

模块内容使用说明，模块分为 4 部分：<br>
I.state 状态，<br>
保存该模块的状态信息；<br>
II.action 方法<br>
供外部调用的模块方法，在这里模块方法为 testAPI，方法内部调用从外部引入的 axios API 请求，再将该请求封装成 Promise 对象，供外部异步捕获 Promise 的两种响应状态 resolve 和 reject。 resolve 一般为成功响应，reject 一般为异常响应。<br>
III.mutations 变化<br>
想要改变模块中的状态，只能通过 commit mutations 去更新模块状态<br>
IIII.export 外界接口<br>
提供一个供外界调用文件的接口，该接口包含的内容有 state、mutations、actions。 namespace：true，表示该模块有专属命名，不嵌入到入口仓库文件中。调用时必须声明出该模块命名

```
import { testAPI } from '../../../api/testAPI'

const state = {
  deviceStatus: []
}

const actions = {
  testAPI({ commit }, data) {
    return new Promise((resolve, reject) => {
      testAPI(data)
        .then(res => {
          resolve()
        })
        .catch(() => {
          reject()
        })
    })
  }
}

const mutations = {
  [STATUS_EVENT.CHECK_ALL_DEVICE_STATUS](state, data) {
    state.deviceStatus = Object.assign([], state.deviceStatus, data)
  }
}
export default {
  namespaced: true,
  state,
  actions,
  mutations
}
```
