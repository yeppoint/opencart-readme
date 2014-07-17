### controller
对数据处理，渲染模板

### 如何写一个Controller
直接上例子：
1. 在/controller/common中加入一中间件Middleware.php，那么类名就是"ControllerCommonMiddleware" (不区分大小写，但请遵循这个命名规则)
2. 在Middleware.php中
```php
//继承Controller
class ControllerCommonMiddleware extends Controller{
	public function index(){
        //$this->language /model /view 各种逻辑处理
        
        //$this->response->setOutput($this->view->load($template,$data))
        //一般不用return ，可以做些校验，例如是否登录

        //如果要链式执行Action,这里是继续执行Controllercommonmiddleware.hello()
        //return new Acition（"common/middleware/hello")
        //
        //return $this->load->.....
	}

    public function hello(){
        echo "Hello world";
    }
}
```

