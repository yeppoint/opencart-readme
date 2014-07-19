### Action
主要用来执行controller的方法（默认是index()）

### NOTE:
从构造方法我们得知：主要在解析路由route,生成控制器类$class  

举个例子有url中："route=common/home"  
处理路由在controller/下，因此现拼凑成DIR_APPLICATION/controller/common/home.php  
然后字符串各种处理，生成控制器类$class="Controllercommonhome"

**这就是为什么自己定义的控制器需要这样的格式**
[See Front.md](Front.md)
