# 7.3.3.设备模型

---

获取设备页面的所有设备信息的基本流程如下，检查传递进来的查询设备信息参数是否有效，无效则抛出异常，有效则进行数据库的查询工作，返回查询的所有设备响应信息给前端

```
    // 获取注册设备页面所有设备信息
    public function getAllDeviceRegisterInfo(){
        (new AllDeviceRegisterInfo())->goCheck();
        $device = (new DeviceInfoModel())->getAllDeviceInfo();
        return $device;
    }
```

以下是查询设备信息的业务处理，获取前端的查询设备参数，查询所有设备信息，若找到设备则返回响应信息给前端，没有则抛出没找到设备信息异常

```
    // 获取注册设备页面的所有设备信息
    public function getAllDeviceInfo(){
        $request = new Request;
        $params = $request->only(['msgId']);
        $msgId = $params['msgId'];
        $allDeviceInfo = (new self)->order('device_id asc')->select();
        if(!$allDeviceInfo){
            throw new DeviceExistException(['msg'=>'没找到设备信息']);
        }
        foreach ($allDeviceInfo as $data){
            $data->save(['msgId'=>$msgId]);
        }
        return $allDeviceInfo;
    }
```
