//create Front Controller
$controller = new Front($registry);

//the functions
public function addPreAction($pre_action);
public function dispath($action,$error);
public function execute($action);

其中dispath()->execute();

由方法可见，Front用于分发Action 然后执行Action

在./index.php中，有这么几行
```php
    // Maintenance Mode
    $controller->addPreAction(new Action('common/maintenance'));

    // SEO URL's
    $controller->addPreAction(new Action('common/seo_url'));

    //you middleware
    $controller->addPreAction(new Action('..middleware...'));

    .....

    // Dispatch
    $controller->dispatch($action, new Action('error/not_found'));
```

由此可见，如要要做更多的预处理，可以这里(dispatch()之前)添加你自己的中间件(Action..)

### 工作流程
调用dispatch($action, $error) 后
现执行$result = $this->execute($pre_action);

后执行自定义的一个$action
```php
    while ($action) {
	    action = $this->execute($action);
    }
```

如何不断只执行？
Action可以执行后返回一个Action,这样就可以链式执行

### 如何写中间件？
直接上例子：
1. 在/controller/common中加入一中间件Middleware.php
2. 在Middleware.php中
```php
//注意，由于文件目录在/controller/commoncommon.php/，加入一中间件Middleware类的命名方式必须是Controllercommonmiddleware
//否则无法自动加载到该类
class Controllercommonmiddleware extends Controller{
	public function index(){
		echo "Hello ,this is MiddleWare!";
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

3. 在./index.php中
```php
// Front Controller
$controller = new Front($registry);

//add  middleware
$controller->addPreAction(new Action('common/middleware'));

```





