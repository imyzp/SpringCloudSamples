### 项目介绍
SpringCloudSamples是建立一个空的工程
### 项目内容
这个空的工程里面保存的都是一个个module工程，即所谓的微服务相关的工程（microService）

我们知道微服务是提供某个具体特定业务的，多个微服务提供了各种各样和业务。许多业务之间有相互关联的数据，
如商品库存业务、商品订单业务，
那么微服务之间就需要一个连接的桥梁，这个桥梁就叫做- 微服务注册中心，微服务在注册中心里可以暴露自己的
接口服务，这样其它微服务就可以调用接口，处理关联的数据。

微服务注册中心为微服务提供了沟通的桥梁，那么它的稳定性就要得到保证，假如它挂了，那么业务之间的关联
不就出现问题了，所以一般注册中心都设置集群，一台挂了还有其它台可以用。

许许多多的微服务，每个微服务都有自己的配置文件，如端口等。假如其中一个微服务的配置文件配置错误了，那么就可能导致
其它微服务也要停掉重新启动服务，假如有很多服务都要重新启动的话，那就会非常麻烦了。那么就有个功能解决了这个问题
-- 微服务配置文件管理中心 ，将所有微服务的配置文件放到管理中心里，当有一个微服务需要更改配置文件时，就不需要重
启动微服务，只要向这个配置文件管理中心发送一个命令，所有关联和微服务都会重新加载配置文件即可。

我们知道许许多多的微服务提供了不同的功能，那么一个页面里有订单信息、商品库存信息，这两个假如位于不同的微服务里，
那么我们可以有一个---消费者微服务，这个微服务专门调用其它微服务的接口。页面专门写在这个消费者微服务里，其它微服务
只提供服务接口---提供者微服务

一个微服务可能出现非常多的用户访问造成其压力大，我们可以通过--微服务压力监控平台  ，来实时查看每个 微服务的压力
，如果有的微服务压力太大，可以对它进行集群配置，减缓压力

微服务之间的配置不同如端口，就会造成url上不一致，我们需要一个统一的路由器，相当于访问其它微服务时先通过这个路由器
在调用其它微服务，我们只要在这个路由器里将url统一就行，还可以做一些校验如登录校验，我们称为--微服务路由


不同的微服务之间，难免会有一些公共的代码，如工具类等。这样就可以有一个工程叫做-----公共类工程，有用到公共服务的，只要在
maven里导入它即可，它是不需要启动的，所以它不算一个微服务，只是将公共代码抽出来做成一个jar包。（microServiceChildModuleCommon）

还有一个就是不同微服务工程里，会用到许多相同的jar包，我们可以有一个叫做工程----公共jar包工程，其它工程只要继承它，这样
就不要重复写jar包了。（microServiceFatherModule）

### 项目启动步骤
#### 1、启动微服务配置文件管理中心
启动 microServiceConfigServer ，是管理所有工程的配置文件的,所有工程都要通过它获取配置。所以这个工程必须最先启动
它是如何管理所有工程配置文件的，具体看它的readMe说明。其它工程又是如何通过它来获取配置的 
可以参考事例工程 microServiceConfigClient 具体查看
其中的readMe说明。
#### 2、启动微服务注册中心
启动 microServiceEurekaServerFirst、microServiceEurekaServerSecond，这两个工程都是微服务注册中心，
两个功能一样，都是提供微
服务之间交流的平台即微服务通过它可以互相访问调用。两个相当于做到了简单的集群配置。
#### 3、启动提供者微服务
启动 microServiceChildModuleProductProvider ，是具体业务的服务提供者，相当于淘宝里有订单和商品，
那么它就是订单服务或者商品服务。真实项目会
有许许多多这样的服务，这一个作为事例。
#### 4、启动消费者微服务
启动 microServiceChildModuleProductConsumer_Feign或者microServiceChildModuleProductConsumer_Ribbon
 是用于调用服务提供者的工程，可以称为服务的消费者,两者作用是一样，我们选择其中一个就好。
 我们知道一个淘宝页面可能都要展示订单信息和商品信息，而信息同时位于两个不同的服务提供者。
 可以将它理解为页面展示工程。这两个工程不同之处，在于使用技术不同，其中Feign相对简单。
#### 5、启动微服务压力监控平台
启动 microServiceChildModuleHystrixDashboard，是对调用服务的压力进行检测。
它是以折线图等可视化展示一个服务被调用的压力。在实际中如果发现某个服务
压力特别大，可以增加其部署的服务器即集群，减缓压力。
#### 6、启动微服务路由
启动 microServiceZuulGateWay ,是对外部访问时统一路口作用，因为不同的服务可能就有不同的访问端口，
这样地址就不统一，它就是使调用的地址形式达到统一，
相当于一个路由器，访问时通过它在去调用不同的服务。它还有一个作用就是调用时做一些校验如登录校验。

