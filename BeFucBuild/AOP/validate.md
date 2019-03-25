# 7.2.1.校验层

---

AOP 编程的一种具体实现，用一个校验基类去继承 TP5 的校验类，并为该类添加公有方法，该方法的作用是捕捉 Http 请求的所有参数,并将调用 TP5 的校验类分支 check 方法进行校验判断，若符合该分支的校验规则则返回成功，若不符合则跑出参数异常响应信息。

```
use app\lib\exception\ParameterException;
use think\Validate;

class BaseValidate extends Validate
{
    public function goCheck()
    {
        // 获取 http 传入的参数
        // 对这些参数做校验
        $params = input('');
        // this 指的是 validate ，因为继承在 validate 里面
        $result = $this->batch()->check($params);
        if (!$result) {

            $e = new ParameterException([
                'msg' => $this->error
            ]);
            throw $e;
        } else {
            return true;
        }
    }
}
```

校验基类写好后，创建任意校验类去继承校验基类，实质上是继承 gocheck 方法，并重载校验类的校验规则。业务函数只需要调用该类的 gocheck 方法即可，这就相当于在参数要往数据库传递的过程中进行拦截检查。这就是切面编程的精髓。使得代码更加的高内聚、低耦合。

```
class AllManufacturerInfo extends BaseValidate
{
    protected $rule = [
        'msgId' => 'require'
    ];
}
```
