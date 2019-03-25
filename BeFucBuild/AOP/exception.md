# 7.2.2.异常处理层

---

AOP 编程的一种具体实现，用一个异常基类去继承 TP5 的异常类，并为该类添加公有方法，该方法的的主要作用是用一个异常类去重载 TP5 异常类的 render 方法。该方法在每次异常发生中会捕捉异常进行处理。若该异常属于自定义的基类异常则将自定义的异常类的参数提取出来，并将请求异常的 Url 地址提取出来一并返回给前端。若该异常不属于自定义异常则返回默认异常参数给前端。注意要使用自定义的异常类则需要到 config\app.php 文件中进行修改。路径为你新建的 ExceptionHandler 路径。

```
    // 异常处理handle类 留空使用 \think\exception\Handle
    'exception_handle'       => 'app\lib\exception\ExceptionHandler',
```

```
use Exception;
use think\exception\Handle;
class ExceptionHandler extends Handle
{
    private $code;
    private $msg;
    private $errorCode;
    // 需要返回客户端当前请求的 URL 路径
    public function render(Exception $e)
    {
        if($e instanceof BaseException){
            //如果是自定义的异常
            $this->code = $e->code;
            $this->msg = $e->msg;
            $this->errorCode = $e->errorCode;
        }else{
            if(config('app_debug')){
                //return default error page
                return parent::render($e);
            }else {
                $this->code = 500;
                $this->msg = 'server error';
                $this->errorCode = 999;
                $this->recordErrorLog($e);
            }
        }
        $request = new Request;
        $result = [
            'msg' => $this->msg,
            'errorCode' => $this->errorCode,
            'request_url' => $request->url()
        ];
        return json($result,$this->code);
}
```

基类异常去继承 TP5 的异常类，注意，该异常类的 render 方法已经被重载了。通过构造函数将参数进行判断，将外部调用的异常参数写进 TP5 的异常类的参数中。

```
use think\Exception;
class BaseException extends Exception
{
    //HTTP 状态码
    public $code = 400;
    //错误具体信息
    public $msg = 'param error';
    //自定义的错误码
    public $errorCode = 10000;
    public function __construct($params = [])
    {
        if(!is_array($params)){
            throw new Exception('参数必须是数组');
        }
        if(array_key_exists('code',$params)){
            $this->code = $params['code'];
        }
        if(array_key_exists('msg',$params))
        {
            $this->msg = $params['msg'];
        }
        if(array_key_exists('code',$params))
        {
            $this->errorCode = $params['errorCode'];
        }
    }
```

自定义一个异常类，自定义异常参数重载父类的异常参数，调用该类声明的异常，则可以返回一个自定义的异常消息给前端。

```
class DeviceExistException extends BaseException
{
    public $code = 200;
    public $msg = '该设备编号已存在';
    public $errorCode = 10000;
}
```
