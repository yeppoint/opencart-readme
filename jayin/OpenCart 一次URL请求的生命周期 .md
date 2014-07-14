[source link](http://blog.csdn.net/sadfishsc/article/details/7263748)

一份完整的OpenCart源码中包含着3个子系统，分别是：前台购物网站catalog、后台管理员工具admin、以及系统安装工具install。三者都分别只有一个入口，如下：

catalog:          http://<host_name>/index.php（根目录下的index.php）

admin:             http://<host_name>/admin/index.php

install:              http://<host_name>/install/index.php

3个子系统虽然在具体实现上各有不同，但是其原理都是一样的。下面以catalog为例描述OpenCart中处理URL请求的生命周期。

 

catalog的URL格式通常如下：

http://<host_name>/index.php?route=<route>(&...)

参数route如果不存在，则在index.php的处理中会将它自动置为common/home。（admin的URL格式与catalog大同小异，只是还必须有另一个参数token，否则会自动跳转到common/login。）

进入index.php后，首先会导入根目录下的配置文件config.php，检查是否已经配置：若无，则会跳转到install/index.php，开始系统安装。系统安装分4步，分别是：

1.      同意许可（step_1.php）

2.      检查环境（step_2.php）

3.      将SQL导入数据库，配置根目录和admin目录下的config.php文件（step_3.php）

4.      显示其余两个子系统的入口（step_4.php）

config.php文件正常配置的情况下，index.php将初始化所有system/engine和system/library目录下的对象，并将这些对象的实例存到Registry对象的实例$registry中。$registry在除了Action外的驱动对象（system/engine下的对象）中都有备份，目的是当从index.php跳转到真正的controller的时候这些对象的信息不会丢失。特别需要说明的是，URL请求的信息将被保存到Request对象的实例，如POST/GET参数将以key=>value的形式保存到公有成员post/get数组中。

初始化全部完成后，URL中的route参数将会被Action对象解析，Action的实例由控制层（controller）的管理器Front对象进行处理，跳转到相应的controller中。

OpenCart基于MVC(+L)架构，catalog/controller路径才是前台网站真正的控制层。Action对象会将route参数解析成准确的controller文件（即控制层类）、调用的函数以及所需的参数，然后Front对象调用相应PHP文件中的函数，并传入参数。以route=common/home为例，Action定位到catalog/controller/common/home.php文件，调用的函数为index()，无参数，然后Front根据这些信息进行跳转。（解析和跳转的详情参见Action和Front。）

进入到controller文件之后，主要会进行如下的操作：

1.      检查是否传入参数（POST或GET），若有则优先进行处理

2.      从language目录下的对应文件中读出所需的常量字符串（使用保存在Controller对象中的Language对象，controller层的所有类都继承自Controller。）

3.      调用model目录下的对应文件中的类访问数据库，获取所需的数据

4.      所有需要输出的数据都保存到data数组中

5.      通过template指向view目录下对应tpl模板文件，通过children数组指向需要一同输出的controller（一般是页面的头部header和尾部footer）

6.      调用Controller对象的render函数对data和view层模板进行组装，然后通过Response对象的setOutput函数输出，返回结果

 

OpenCart中比较复杂的操作，如字符串的拆解、URL的组装、数据的分解和组装、页面的生成等都封装在system目录下的对象中，所以MVC层次上的操作比较程式化，也比较简单。

 

另外，虽然admin和catalog一样都是通过Action和Front来跳转到真正的controller，但是由于admin/config.php和config.php文件中配置的路径不同，因而二者的控制层不会相互冲突。

