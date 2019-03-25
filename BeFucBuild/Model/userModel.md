# 7.3.1.用户模型

---

后台系统服务器用户模型，在这个模型中专门去管理用户相关的业务数据处理，如用户的登陆、登出、注册。以下是控制器的入口函数，在这里可以看出由于做了 AOP 的校验层和异常处理层，这里用非常简短干净的代码就实现了用户模块的登出操作，先检查用户登出的参数是否有效，如果有效就进行数据库的操作，若数据库操作出现异常则抛出异常给前端。否则返回相应的数据

```
  // 用户退出登陆
  public function putUserLogout(){
      (new UserLogout())->goCheck();
      $user = (new UserModel())->putUserLogout();
      if(!$user){
          throw new UserMissExcepiton(['msg'=>'用户名不存在']);
      }
      return $user;
  }
```

下面是在用户模型中的数据库操作，首先获取指定的参数：用户名和 msgId，查询用户名是否存在，更新 msgID，若用户名存在，用户表的状态更新为离线状态，返回用户表的信息给前端

```
    // 用户退出
    public function putUserLogout(){
        $request = new Request;
        $params = $request->only(['username','msgId']);
        $username = $params['username'];
        $msgId = $params['msgId'];
        $user = (new self)->where('username','=',$username)->find();
        $user->save(['msgId'=>$msgId],['username'=> $username]);
        $user->save(['status'=>0],['username'=>$username]);
        return $user;
    }
```
