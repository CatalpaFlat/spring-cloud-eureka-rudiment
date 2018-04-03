# spring-cloud-eureka-rudiment
> Spring Cloud 基于Eureka实现分布式“服务注册与发现”——入门

## 1.引入配置

```xml
    <dependencyManagement>
        <dependencies>
            <!--spring-cloud-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Dalston.SR4</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <dependencies>
        <!--eureka server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-eureka-server</artifactId>
        </dependency>
    </dependencies>
    
```

## 2. 配置服务注册

```yaml
server:
  port: 8881

eureka:
  instance:
    hostname: 127.0.0.1
  client:
    registerWithEureka: false
    fetchRegistry: false
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```

```java
@EnableEurekaServer
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## 3. 配置服务发现


```yaml
server:
  port: 8882

eureka:
  instance:
    hostname: 127.0.0.1
  client:
    serviceUrl:
      defaultZone: http://${eureka.instance.hostname}:8881/eureka/
```

```java
@EnableEurekaClient
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
