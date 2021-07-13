### 微服务工程介绍
- 本工程是微服务的提供者，就是主要对数据库进行操作，一个庞大的工程有许多的微服务提供者，本例只是一个例子
- 服务的提供者都要注册要微服务注册中心(Eureka),并且对压力大的服务提供者还要配置在多个
- 服务器，全部都要注册到微服务注册中心(Eureka)，微服务的消费者根据负载均衡算法选择最优的
- 服务进行访问即负载均衡(参考微服务消费者中如何实现负载均衡)
### 如何实现微服务的提供者并注册到微服务注册中心
- （1）导入jar,查看pom中 微服务相关
- 注意;目前已经将配置文件 统一管理
    - 具休查看 项目microServiceConfigServer 、microServiceConfigClient是如何配置的
- （2）编辑配置文件，查看application.yml文件中的 eureka 内容
- （5）在启动类上加相关注解，查看启动类
- 根据步骤一步步看，其中都有注解说明
### 本工程提供了哪些服务
#### mybatis连接数据库，数据源Druid配置
- (1)导入jar，查看pom中  'mybatis 启动器'、'数据源'
- (2)添加mybatis配置文件：mybatis/mybatis.cfg.xml，和对应表的xml文件如microServiceChildModuleProductProvider 的mybatis/mapper/ProductMapper.xml 
- 、com.example.fs.mapper.ProductMapper
- (3)启动类加上扫描Mapper接口的注解，查看启动类
- (4)编辑系统配置文件，查看其中  mybatis   、 spring.datasource相关配置
#### 目前主要对product实体类，进行了查找数据库查找操作，功能待添加。。。