# 7.后端服务器功能模块

---

后端服务器主要包含功能：参数校验、异常响应、数据库的增删改查（设备表、用户表、厂商表）
后端服务器实质上就是对数据库进行操作的地方。如何有效的对数据库操作管理。在前端传过来的数据需进行参数校验，当参数不符合校验标准时响应异常给前端，若参数校验通过，但由于数据库或其它的原因无法响应也必须向前端传递异常响应。
