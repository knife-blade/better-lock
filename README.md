# nicelock

## 1.介绍
nicelock：一个注解，即可使用Java的分布式锁。（基于Redisson，稳定！）

## 2.快速使用

### 1.引入依赖
```xml
<dependency>
    <groupId>com.suchtool</groupId>
    <artifactId>nicelock-spring-boot-starter</artifactId>
    <version>{newest-version}</version>
</dependency>
```

### 2.配置Redis
本组件基于Redisson，要添加Redis相关配置，比如：
```
spring:
  redis:
    host: 127.0.0.1
    port: 6379
    password: 222333
```

### 3.使用
```
@NiceLock(keys = {"#user.id", "#orderNo"})
public String createOrder(User user, String orderNo) {
    System.out.println("创建订单");
    return "success";
}
```

## 3.详细配置

### 1.执行顺序
默认情况下，本组件在@Transactional之前执行。你可以指定本组件的执行顺序，在SpringBoot的启动类上加如下注解即可：
```
@EnableNiceLock(order = 1)
```
比如：
```
package com.knife.example;

import com.suchtool.nicelock.annotation.EnableNiceLock;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableNiceLock(order = 1)
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```

### 2.配置大全
支持yml等配置方式。

| 配置  | 描述  |  默认值 |
| ------------ | ------------ | ------------ |
| suchtool.nicelock.keyPrefix  | 存到Redis里的key的前缀  | nicelock |

