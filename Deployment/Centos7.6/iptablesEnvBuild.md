# 8.2.6.iptables 防火墙

---

###关闭默认 firewall

```
service firewalld stop
#禁止firewall开机启动
systemctl disable firewalld.service
```

###安装 iptables 防火墙

```
yum install iptables-services
```

###编辑 iptables 防火墙配置

```
vi /etc/sysconfig/iptables
```

###设置防火墙开机启动

```
service iptables start #开启
systemctl enable iptables.service #设置防火墙开机启动
```
