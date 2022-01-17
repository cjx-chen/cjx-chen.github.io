---
title: 【SpringBoot】跨域(CORS)支持：注解@CrossOrigin
date:  2022-01-17 12:28:34
img: https://img-blog.csdnimg.cn/img_convert/174788b2ec1d828d85a0a7ac65bea2cd.png
categories: 
- Java
tags:
- Java
- SpringBoot
- 报错解决方法
---

## 跨域(CORS)支持
出于安全原因，浏览器禁止Ajax调用驻留在当前原点之外的资源。

跨源资源共享（CORS）是由大多数浏览器实现的W3C规范，允许您灵活地指定什么样的跨域请求被授权，而不是使用一些不太安全和不太强大的策略，如IFRAME或JSONP。

Spring Framework 4.2 GA为CORS提供了第一类支持，使您比通常的基于过滤器的解决方案更容易和更强大地配置它。所以springMVC的版本要在4.2或以上版本才支持`@CrossOrigin`

## 使用方法
**controller 配置 CORS**

### controller方法的CORS配置
你可以向`@RequestMapping`注解处理程序方法添加一个`@CrossOrigin`注解，以便启用CORS（默认情况下，`@CrossOrigin`允许在`@RequestMapping`注解中指定的所有源和HTTP方法）：

```java
@RestController
@RequestMapping("/account")
public class AccountController {
 
    @CrossOrigin
    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }
 
    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
```

其中`@CrossOrigin`中的2个参数：

- origins：允许可访问的域列表
- maxAge：准备响应前的缓存持续的最大时间（以秒为单位）。

### 为整个controller启用`@CrossOrigin`

```java
@CrossOrigin(origins = "http://domain2.com", maxAge = 3600)
@RestController
@RequestMapping("/account")
public class AccountController {
 
    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }
 
    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
```

在这个例子中，对于`retrieve()`和`remove()`处理方法都启用了跨域支持，还可以看到如何使用`@CrossOrigin`属性定制CORS配置。

### 同时使用controller和方法级别的CORS配置
Spring将合并两个注释属性以创建合并的CORS配置

```java
@CrossOrigin(maxAge = 3600)
@RestController
@RequestMapping("/account")
public class AccountController {
 
    @CrossOrigin(origins = "http://domain2.com")
    @GetMapping("/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }
 
    @DeleteMapping("/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
```