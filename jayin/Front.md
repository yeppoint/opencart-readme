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
while ($action) {
			$action = $this->execute($action);
}

如何不断只执行？

 

### 如何写中间件？

必须return 一个Action or ? view




