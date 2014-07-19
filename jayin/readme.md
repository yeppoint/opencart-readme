Registry  
注册器，保存各种键值对

Loader  
加载器，用来加载model,view,controller,language 

MVC(L)模式(L->Language)  

### Directory structure


catalog/ 前端   
admin/ 后端   
system/ 前端后端共用的类，方法(如email helper,database helper,model和控制器的核心定义) ps:一般来说不用改动这部分的代码  
system/download/ 包含了产品的需要下载的信息,更详细点击[这里](http://docs.opencart.com/display/opencart/Downloads)   
image/ 包含了所有图片，图片上传自admin [Image Manager](http://docs.opencart.com/display/opencart/Image+manager)   


**Note**  
1. 如果你在只搞frontend，就不需要动admin/ ,反之亦然  





