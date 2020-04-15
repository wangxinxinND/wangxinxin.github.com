整体思路：
  1.配置阶段
    web.xml:DispatchServlet 由spring提供
    init-param classpath:appication.xml  contextConfigLoaction
    url-pattern /*
    //spring 配置很多url, struts 配置一个controller, sprngMVC-一个controller多个url
    
    
    
  2.初始化,启动阶段
     init 加载spring的配置文件,从配置文件中读取类,类之间的关系
     IOC初始化 声明一个IOC容器  Map<String,Object>
     scan-package 配置一个包扫描路径,扫描到相关的类,放到list中
     实例化  将扫描到的相关类,利用反射机制实例化,并且保存到IOC容器之中
        不是所有的类都要实例化,只有加了注解的类,才会实例化
        遍历所有扫描到的类,有注解/配置的的,进行初始化
     依赖注入 DI  自动给IOC容器中的对象,需要自动赋值的属性赋值
        根据Autowired注解或者属性配置,从IOC的bean容器中取出相关的实例,进行赋值,完成注入
        循环依赖问题:
          实例化后对象保存在容器中,其他类保存一个引用时.A依赖B,A实例化存到IOC容器中,再给A注入依赖的B.
          若B未实例化,则实例化B存到IOC容器中,此时B又依赖了A,执行属性注入,从IOC容器中找A实例,注入返回注入完成的B
        

​	SpringMVC : HandlderMapping	将url对应的一个Method 将这样的关系保存起来, 暂时理解为Map<String, Method>
      将RequestMapping注解的方法url编译成正则,封装成Handler对象,
      Handler对象包含(方法的对象,url正则,对应的方法)保存在list中



  3.运行阶段,等待请求
    doGet/doPost request,response
    从HandlerMapping  通过request获得url,然后再去获得HandlerMapping
    invoker  反射调用Method
    response.write()
    
   String.replaceAll("/+","/") 正则表达式替换  多个/替换为一个/
   
Aop: 
  1.原理:
    将复杂的需求分解成不同的方面,将公共的功能集中解决
    采用代理机制组装起来运行,在不改变原有程序的基础上对待吗进行增强处理,增加新的功能
    预编译/运行期
  
  连接点:正常可能要增强的方法
  切点:表达式告诉springAop 哪些地方需要增强,就是查询条件
  target目标对象
  织入  增强方法增强到指定位置
  切面 抽象概念,由增强方法和切点构成的面(两点连接成线,线组成面)
    
  
 增强运行时间:  bean生命周期的 后处理beanPostProcess
   
