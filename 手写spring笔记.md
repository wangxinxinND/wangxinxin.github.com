整体思路：
  1.配置阶段
    web.xml:DispatchServlet 由spring提供
    init-param classpath:appication.xml  contextConfigLoaction
    url-pattern /*
    spring 配置很多url, struts 配置一个controller, sprngMVC-一个controller多个url
    
    
    
  2.初始化,启动阶段
     init 加载spring的配置文件
     IOC初始化 声明一个IOC容器  Map<String,Object>
     scan-package 配置一个包扫描路径,扫描到相关的类
     实例化  将扫描到的相关类,利用反射机制实例化,并且保存到IOC容器之中
     依赖注入 DI  自动给IOC容器中的对象,需要自动赋值的属性赋值

​	SpringMVC : HandlderMapping	将url对应的一个Method 将这样的关系保存起来, 暂时理解为Map<String, Method>



  3.运行阶段,等待请求

    doGet/doPost request,response
    从HandlerMapping  通过request获得url,然后再去获得HandlerMapping
    invoker  反射调用Method
    response.write()

