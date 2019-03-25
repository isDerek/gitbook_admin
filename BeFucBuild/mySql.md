# 7.1.数据库设计

---

管控系统涉及为提供路灯厂商的监测控制。以上思路大致将数据库划分为 3 部分：厂商、设备、用户。为什么厂商不是用户，在这里需要进行说明，厂商指的的群的概念，用户指的是个人的概念，这两个元素不具有共性。用户模块在所有的数据库都是比较独立的一部分。<br>
用户表的参数:<br>
id:表的主键，自增保持着唯一特性<br>
username:用户名<br>
password:密码<br>
confirmPassword:确认密码<br>
status:用户在线状态<br>
scope:用户权限<br>
token:用户会话加密配对<br>
phone:用户手机<br>
msgId:会话唯一配对 ID<br>
create_time:表参数创建时间<br>
update_time:表参数更新时间<br>
delete_time:表参数删除时间(软删除)<br>
设备注册表的参数:<br>
id:表的主键，自增保持着唯一特性<br>
device_id:设备编号<br>
version_id:版本编号<br>
manufacturer_id:厂商编号<br>
device_addr:设备运行地址<br>
device_mac:设备 MAC 地址<br>
msgId:会话唯一配对 ID<br>
create_time:表参数创建时间<br>
update_time:表参数更新时间<br>
delete_time:表参数删除时间(软删除)<br>
设备状态表的参数:<br>
id:表的主键，自增保持着唯一特性<br>
device_id:设备编号<br>
mac_id:设备 MAC 地址<br>
device_addr:设备地址<br>
ip_address:设备网络 IP 地址<br>
vendor_id:厂商编号<br>
status:设备在线状态<br>
time_start:设备开始运行时间<br>
time_stop:设备停止运行时间<br>
msgId:会话唯一配对 ID<br>
create_time:表参数创建时间<br>
update_time:表参数更新时间<br>
delete_time:表参数删除时间(软删除)<br>
厂商信息表:<br>
id:表的主键，自增保持着唯一特性<br>
order_id:厂商编号<br>
notify_address:厂商推送地址<br>
manufacturer_name:厂商名称<br>
msgId:会话唯一配对 ID<br>
create_time:表参数创建时间<br>
update_time:表参数更新时间<br>
delete_time:表参数删除时间(软删除)<br>
