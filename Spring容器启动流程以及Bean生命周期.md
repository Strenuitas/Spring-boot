一：Spring Boot 启动
    1.SpringApplication.run(Application.class,args)
      ·Spring Boot 创建Spring Application 对象
      ·初始化Spring容器
    2.准备环境
      ·读取配置文件 yml/properties
      ·加载@Configuration配置类,创建配置类的对象，然后找到里面方法用@Bean标记的方法，将方法返回的对象注册到容器中
      ·初始化环境变量，系统属性
二：扫描和注册Bean
    1.扫描组件
      ·扫描主类所在包及子包
      ·扫描一下注解：
        · @Component(通用)
        · @Service(业务层)
        · @Repository(持久层)
        · @Controller/@RestController(控制层)
        · 其他自定义Bean
    2.生成BeanDefinition
      ·Spring将扫描的类转换为BeanDefinition对象
      ·BeanDefinition是Spring内部的数据结构，记录：
        · 类类型
        · 是否懒加载
        · 作用于(Singleton/Protorype)
        · 构造器/属性依赖信息
    3.注册Bean到容器
        ·所有BeanDefinition被注册到容器的BeanFactory
        ·容器管理Bean的创建、依赖注入、生命周期
三：Bean实例化和依赖注入
    1.实例化Bean
      ·Spring根据BeanDefinition调用构造器生成对象
      ·如果使用@RequiredArgsConstructor + final 字段，构造器注入自动完成
    2.依赖注入(DI)
      ·Spring自动注入依赖Bean:
        · Controller注入Service
        · Service注入Mapper
      ·注入方式：
        · 构造器注入
        · 字段注入(Autowired)
        · Setter注入
    3.属性填充
      ·注入 @Value注解的配置值
      ·注入 @ConfigurationProperties对象
四：初始化回调和Aware接口
    1.如果Bean实现了Aware接口，Spring会回调
      ·Bean


五：Bean就绪并可用
    ·完成依赖注入和初始化后，Bean被标记为就绪状态
    ·对Controller Service Mapper来说：
        Controller：对外提供HTTP接口，接收HTTP请求
        Service：提供业务方法
        Mapper：执行数据库操作
    ·Spring容器管理整个Bean生命周期
