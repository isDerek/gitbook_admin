# 3.3.Axios

---

Axios 是基于 Promise 的 HTTP 库。是负责 HTTP 请求的封装类。Axios 最关键是基于 Promise ，意味着这是异步的！Promise 对象可在未来的一段时间里捕获到成功或失败的响应结果。下图就是 Promise 的具体用法。

```
import axios from 'axios'
import { ERR_TYPE, PlugError } from '../utils/PlugError'
import { msgId } from '../utils/toolFunc'
export async function getUserLogin(params) {
  const url = 'api/v1/getUserLogin'
  let resp = await axios({
    method: 'post',
    url: url,
    data: {
      username: params.username,
      password: params.password,
      msgId: msgId
    }
  })
  let respData = resp.data
  // 1 代表在线状态, 校验是否为该会话响应
  if (respData.status === '1' && respData.msgId === msgId) {
    return respData
  } else {
    throw new PlugError(ERR_TYPE.API_RESP_ERR, respData.data.errMsg)
  }
}
```

async-await 是 ES7 新出的语法规范，它是基于 Promise 的语法糖。async 能确保一个带有返回值的函数返回 Promise 的 resolve 值，而 await 是异步等待 JavaScript 运行，直到返回一个 Promise 响应结果。在这列举出一个用户登陆且满足 RESTFUL API 的请求。‘getUserLogin’，将用户登陆当作一种资源，get 代表查询，翻译起来就是，去服务器查询用户登陆状态，若返回资源状态为在线（1），则用户可登陆，若返回资源状态为离线（0），则用户不可登陆，即用户名或密码不正确。<br>
在这里请求的 url 为提供 API 服务器的地址。等待 axios （Promise）返回响应，请求的 HTTP 方法为 POST，POST 的请求将参数放置在了请求的 Body 中，GET 请求将参数放置在了 URL 中，还有 DELETE，PUT 等方法。携带要请求给服务器的数据参数。当服务器返回的响应结果会存放到 data 属性中，在此判断返回的用户状态和 msgId 是否和发出去的时候相一致。在这里对 msgID 作为说明，这是为了保证每次会话的唯一配对特性。
