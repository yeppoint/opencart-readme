1. ./index.php为入口
    1.1 加载配置文件config.php，各种常量
    1.2 加载startup.php，引入各种必要的文件(./system/engine ,./system/library)

2. 整体流程

    2.1 创建Registry对象

    2.2 注册所有公共类

    2.3 创建Front类对象，作为请求分发器（Dispatcher）

    2.4 根据用户请求（url）创建控制器对象及其动作。
        ```php

            在Front类私有函数execute($action)中如下语句

            $controller = new $class($this->registry); //创建控制器
        ```

    2.5 控制器加载相应的模型，如
        ```php
            $this->load->model('design/layout');(注意前后的模型，/ 线前面是模型下的文件目录名后面是目录下的文件名，也是模型对象)

            该语句将创建相应的model对象。(相当NEW对像，加载进模型后就可以使用了,一般处理复杂程序或需要重用时就会建模型，每个模型是一个类)
         ```

        如：  
        ```php
            $this->load->model('user/user');//加载后模型类名$this->文件目录->文件名(文件目录是指model下的目录名)

            $this->model_user_user->getTotalUsersByEmail($this->request->post['email'])
        ```

 

    2.6 控制器获取模板，绘制（提取数据并启用output buffer）到页面输出区output中
            ```php
                $this->render();
            ```

    2.7 最后Response对象把输出区的数据（页面）echo返回给用户
     如：
        ```php
            if (file_exists(DIR_TEMPLATE . $this->config->get('config_template') . '/template/product/product.tpl')) {

            $this->template = $this->config->get('config_template') . '/template/product/product.tpl';

            } else {

            $this->template = 'default/template/product/product.tpl';

            }

            $this->children = array(

                'common/column_left',

                'common/column_right',

                'common/content_top',

                'common/content_bottom',

                'common/footer',

                'common/header'

            );
            
            $this->response->setOutput($this->render());
        ```


