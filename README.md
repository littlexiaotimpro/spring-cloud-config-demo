# spring-cloud-config-demo

spring-cloud-demo 项目的配置中心配置存放仓库

### 分布式配置中心

主要分为配置服务端和客户端

提供服务端注册中心、服务提供端、及客户端公共配置，对分布式项目提供多环境配置

### 配置步骤

#### 创建module

cloud-config-server

本质上配置中心也是一个服务提供者

#### 添加依赖

```xml
<!-- 配置中心服务端 -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
<!-- Spring Cloud eureka 客户端 -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

#### 修改application.yml

```yaml
server:
  port: #服务端口号
spring:
  application:
    name: cloud-config-server #应用名称
  cloud:
    config:
      server:
        git: #配置存储配置信息的Git仓库
          uri: https://github.com/littlexiaotimpro/spring-cloud-config-demo.git
          username: # Git仓库用户名
          password: # Git仓库密码
          clone-on-start: true #开启启动时直接从git获取配置
eureka:
  client:
    service-url:
      # Eureka 服务注册中心地址
      defaultZone: http://localhost:8001/eureka/
```

#### 添加启动类

```java
/**
 * 通过添加 EnableConfigServer 注解启用配置
 */
@EnableConfigServer
@EnableDiscoveryClient
@SpringBootApplication
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```



