# 8.2.2.MySql 环境

---

###安装 MySQL5.7\* 源

```
wget http://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm // 下载mysql yum源
rpm -ivh mysql57-community-release-el7-11.noarch.rpm // 安装yum源
```

###安装 MySQL

```
yum install mysql-community-server
```

###启动 MySQL

```
systemctl start mysqld.service
#运行以下命令查看 MySQL 运行状态
systemctl status mysqld.service
```

###查看一下初始密码

```
grep "password" /var/log/mysqld.log
```

![initPassword](../../imgs/Release/mysql/initPassword.png) ###登录 MySQL

```
mysql -uroot -p
# 用户名:root 密码:你查看的初始密码（P/tUrijZo5au）
```

###修改密码

```
ALTER USER 'root'@'localhost' IDENTIFIED BY '密码'
```

**mysql 默认安装了密码安全检查插件(validate_password),默认密码检查策略要求密码必须包含：大小写字幕、数字和特殊符号，并且长度不能少于 8 位。否则会提示 ERROR 1819(HY000):Your password does not satisfy the current policy requirements**

###数据库授权

```
#数据库默认没有授权，只支持本地访问，以下命令允许 root 用户远程访问
#%: 允许所有 IP 访问，你可以指定 IP 进行访问
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFID BY '密码' WITH GRANT OPTION;
#命令生效
FLUSH PRIVILEGES;
```

### 设置自启动

```
systemctl enable musqld
```
