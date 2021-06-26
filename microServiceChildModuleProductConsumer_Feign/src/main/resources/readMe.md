### 工程介绍
- 工程是微服务的消费者：作用就是从服务注册中心调用服务提供者的接口服务，
- 工程采用Feign方式调用服务提供者的接口及实现负载均衡，当调用服务失败时采用熔断器机制
- 关于熔断器：
    - 微服务中服务与服务间通常有依赖关系，用户调商品、商品高库存，库存高订单，
    - 一旦一个服务挂了，可能出现线程阻塞，导致线程阻塞
    - 和响应时间过长或不可用，此时如果有大量的请求涌入，容器的线程资源会被消耗完毕，
    - 导致服务瘫痪，这就是服务故障的“雪崩效应”
    - Feign 集成了熔断器 Hystrix 方便的解决了问题，当服务挂时，会返回一个自定义的信息
    - 说明：由于Feign比较 Ribbon 更方便，所以在Ribbon的工程里没有熔断器代码示例，具体如何使用可查看梦学谷的pdf文件
- 具体实现如下：
### 如何实现服务调用与负载均衡和熔断器
- （1）导入jar,查看pom中 微服务相关
- 注意;目前已经将配置文件 统一管理
    - 具休查看 项目microServiceConfigServer 、microServiceConfigClient是如何配置的
- （2）编辑配置文件，查看application.yml文件中的 eureka 内容和feign内容
- （3）编写接口，查看com.example.fs.service.ProductClientService
- （4）建一个controller进行调用，查看com.example.fs.controller.ProductFeignController_Consumer
- （5）在启动类上加相关注解，查看启动类
- ，其中都有注解说明根据步骤一步步看