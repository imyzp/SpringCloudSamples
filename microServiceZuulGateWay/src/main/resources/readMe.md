## 项目介绍
- 本项目主要两个功能：请求路由，校验过滤
    - 请求路由：对外部请求转发到具体微服务实例上，是实现外部访问统一路口的基础
    - 校验过滤：是对请求过程进行干预，通常做一些校验功能等。
- 原理;项目需要注册到微服务注册中心Eureka,并且从中获取其他微服务。以后访问微服务都是通过本项目跳转后获得。
### 配置步骤
#### 请求路由
- pom中添加  zuul路由网关依赖
- 添加启动类 
- 添加配置文件 application.yml
#### 校验过滤
- 查看 com.example.fs.filter.MyLoginZuulFilter