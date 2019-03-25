# 6.3.2.数据库模型

---

TP5 操作数据库有 DB 访问以及 ORM 模型操作两种形式。DB 是以原声 MySql 语句进行访问，而 ORM 是封装起来的 MySql 请求，本质都是一样的。通过 ORM 去操作数据库更显便捷。TP5 框架连接数据库，在 config/database 文件，写入对应的数据库参数即可。在这里使用的是 MySql 数据库。

```
    // 数据库类型
    'type'            => 'mysql',
    // 服务器地址
    'hostname'        => 'xxxxxx',
    // 数据库名
    'database'        => 'xxxx',
    // 用户名
    'username'        => 'xxxx',
    // 密码
    'password'        => 'xxxx',
    // 端口
    'hostport'        => 'xxxxx',
```

在使用 ORAM 模型操作数据库时，类名要为数据库表名，且继承 TP5 的 Model 类即可

```
use think\Model;
// 数据库表明为 DeviceInfo
class DeviceInfo extends Model
{

}
```
