### loader.view($template, $data = array())

    ob_start() - 打开输出控制缓冲
    ob_get_contents() - 返回输出缓冲区的内容
    ob_end_clean() - 清空（擦除）缓冲区并关闭输出缓冲
    trigger_error() - 产生一个用户级别的 error/warning/notice 信息
    headers_list() - Returns a list of response headers sent (or ready to send)
    header() - 发送一个自定义的http报文 for a more detailed discussion of the matters involved.

* 先注入key-value($data),然后加载模板


### Loader.model($model)
加载model.注意的是：他这里对model的注册(入到)全局$register中
Opencart做了字符串处理，访问的时候$register->xx_yy_zz

举个例子：
在model/catalog/information.php
生成"model_catalog_information"
对应的$class =>ModelCatalogInfomation
//注入
$register.set("model_catalog_information",new )  
//访问
$this->model_catalog_information  
  






