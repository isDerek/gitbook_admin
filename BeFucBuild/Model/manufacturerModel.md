# 7.3.2.厂商模型

---

注册厂商信息的基本流程如下，检查传递进来的厂商信息参数是否有效，无效则抛出异常，有效则创建厂商信息进数据库表中，返回注册好的厂商响应信息给前端

```
    // 注册厂商信息
    public function postManufacturerInfo(){
      (new ManufacturerInfoRegister())->goCheck();
      $manufacturerInfo = (new ManufacturerInfoModel())->postManufacturerInfo();
      return $manufacturerInfo;
  }
```

以下是创建厂商信息的业务处理，获取前端的厂商注册参数，查询该厂商是否被注册，若被注册返回厂商已存在，若没有则返回新注册的厂商信息给前端

```
   // 创建厂商信息
    public function postManufacturerInfo(){
        $request = new Request;
        $params = $request->only(['notifyAddress','msgId','manufacturerName','manufacturerID']);
        $notifyAddress = $params['notifyAddress'];
        $msgId = $params['msgId'];
        $manufacturerID = $params['manufacturerID'];
        $manufacturerName = $params['manufacturerName'];
        $manufacturerByName = (new self)->where('manufacturer_name','=',$manufacturerName)->find();
        $manufacturerByID = (new self)->where('order_id','=',$manufacturerID)->find();
        if(!$manufacturerByName && !$manufacturerByID){
            $newManufacturer = (new self)->data([
                'manufacturer_name' => $manufacturerName,
                'notify_address' => $notifyAddress,
                'order_id' => $manufacturerID,
                'msgId' => $msgId
            ]);
            $newManufacturer->save();
            return $newManufacturer;
        }
        throw new ManufacturerExistException();
```
