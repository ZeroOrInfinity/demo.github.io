# UMS (user manage scaffolding) 用户管理脚手架: 

![UMS](https://img.shields.io/badge/UMS-2.2.1-green.svg)
![JDK](https://img.shields.io/badge/JDK-1.8+-green.svg)
![Maven](https://img.shields.io/badge/Maven-3.6.3-green.svg)
![MySQL](https://img.shields.io/badge/MySQL-5.7.27-green.svg)
![Redis](https://img.shields.io/badge/Redis-5.0.3-green.svg)
![SpringBoot](https://img.shields.io/badge/SpringBoot-2.3.4-green.svg)
![SpringSecurity](https://img.shields.io/badge/SpringSecurity-5.4.1-green.svg)
![SpringSession](https://img.shields.io/badge/SpringSession-2.3.1-green.svg)
![JustAuth](https://img.shields.io/badge/JustAuth-1.15.9-green.svg)
![license](https://img.shields.io/badge/license-MIT-yellow.svg)

用户管理脚手架集成：用户密码登录、手机登录、支持所有 JustAuth 支持的第三方授权登录、验证码、基于 RBAC 的访问权限控制功能, 支持多租户、JWT、SLF4J-MDC、签到等功能。
通过配置文件与实现 **用户服务, 短信发送服务, 获取角色权限服务** 三个 API 接口就可以实现上述功能，实现快速开发，只需要专注于业务逻辑。


User management scaffolding, integration: User password login, mobile login, OAuth2 login(Based on JustAuth), 
Support multi-tenancy, jwt , validate code(image, sms, sliderCode), RBAC, SLF4J-MDC, sign etc...

![ums-arch](doc/ums-arch.png)
------
## 一、`UMS 功能列表(UMS feature list)`：

  - 验证码（图片，短信, 滑块）校验功能(validate code(image, SMS, slider) verification function).
  - 手机登录功能，登录后自动注册, 支持多租户(Mobile login function, automatic registration after login, Support multi-tenancy).
  - 支持所有 JustAuth 支持的第三方授权登录，登录后自动注册 或 绑定 或 创建临时用户([TemporaryUser](https://github.com/ZeroOrInfinity/UMS/blob/master/src/main/java/top/dcenter/ums/security/core/oauth/userdetails/TemporaryUser.java))(OAuth2 login and auto signUp and auto binding).
      - 支持定时刷新 accessToken, 支持分布式定时任务(Support timing refresh accessToken, support distributed timing tasks).
      - 支持第三方授权登录的用户信息表与 token 信息表的缓存功能(Support the caching function of user table and token table by OAuth2 login).
      - 支持第三方绑定(binding)与解绑(unbinding)及查询接口.
  - 访问权限控制功能, 支持多租户(Access control function, support multi tenancy).
  - 简化 session、remember me、csrf、cors等配置(Simplify session、remember me、csrf cors etc configuration).
  - 根据设置的响应方式（JSON 与 REDIRECT）返回 json 或 html 数据.
  - 签到功能(sign).
  - 支持基于 SLF4J MDC 机制的日志链路追踪功能.
  - JWT 创建(通过接口自定义 Claims, 通过配置设置算法等), 校验(通过接口自定义校验规则), 刷新(自动刷新, 直接拒绝, 通过 refreshToken 刷新), 刷新的 JWT 使旧 jwt
   失效引发的并发访问问题及黑名单.
  
## 模块功能 

  | **模块**   | **功能**                                                         |
  | ------ | ------------------------------------------------------------ |
  | [commons](https://github.com/ZeroOrInfinity/UMS/tree/master/commons)   | 通用组件模块 |
  | [ums](https://github.com/ZeroOrInfinity/UMS/tree/master/ums-spring-boot-starter)   | 集成 commons/core/vc/mdc/oauth/rbac/jwt 模块 |
  | [core](https://github.com/ZeroOrInfinity/UMS/tree/master/core)   | 用户名密码登录/手机登录且自动注册/签到/简化HttpSecurity(session、remember me、csrf、跨域等)配置/session redis 缓存/可配置的响应方式(JSON 与 REDIRECT)返回 json 或 html 数据, 集成 jwt/mdc 模块 |
  | [vc](https://github.com/ZeroOrInfinity/UMS/tree/master/vc)   | 验证码, 集成 mdc 模块 |
  | [mdc](https://github.com/ZeroOrInfinity/UMS/tree/master/mdc)   | 基于 SLF4J MDC 机制的日志链路追踪功能 |
  | [oauth](https://github.com/ZeroOrInfinity/UMS/tree/master/oauth)   | OAuth2 login by JustAuth, 集成 jwt/mdc 模块 |
  | [rbac](https://github.com/ZeroOrInfinity/UMS/tree/master/rbac)   | 基于角色的访问权限控制,支持多租户, 集成 mdc 模块 |
  | [jwt](https://github.com/ZeroOrInfinity/UMS/tree/master/jwt)   | JWT 功能, 集成 mdc 模块 |
  | [demo](https://github.com/ZeroOrInfinity/UMS/tree/master/demo)   | basic-example/basic-detail-example/permission-example/quickStart/session-detail-example/validate-codi-example/justAuth-security-oauth2-example/tenant-example/jwt-example |

### demo 演示功能  

  | **demo**                   | **演示功能**                                                     |
  | ---------------------- | ------------------------------------------------------------ |
  | [basic-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-example)         | 基本功能: 最简单的配置                             |
  | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example)   | 基本功能详细的配置: 含anonymous/session简单配置/rememberMe/csrf/跨域/登录路由/签到, 不包含session详细配置/验证码/手机登录/权限. |
  | [permission-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/permission-example)     | 基于 RBAC 的权限功能设置                          |
  | [quickStart](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/quickStart)             | 快速开始示例                                                 |
  | [multi-tenancy-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/tenant-example)             | 多租户注册与登录示例                                                 |  
  | [justAuth-security-oauth2-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/justAuth-security-oauth2-example)             | 第三方授权登录详细示例, MDC 日志链路追踪配置                                                |
  | [session-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/session-detail-example) | session 与 session 缓存详细配置                   |
  | [validate-code-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/validate-code-example)  | 基本功能: 验证码(含滑块验证码), 手机登录配置  |
  | [jwt-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/jwt-example)  | JWT 功能示例  |

### [Github 更新日志(UpdatedLog)](https://github.com/ZeroOrInfinity/UMS/blob/master/UpdatedLog.md) | [Gitee 更新日志](https://gitee.com/pcore/UMS/blob/master/UpdatedLog.md)

### [Github 文档地址](https://github.com/ZeroOrInfinity/UMS/wiki) | [Gitee 文档地址](https://gitee.com/pcore/UMS/wikis/pages)

### 登录流程
![ums-arch](doc/登录流程.png)

### JWT 流程图
![ums-arch](doc/纯jwt流程图.png)
![ums-arch](doc/jwt-session流程图.png)

### 微信群：UMS 添加微信(z56133)备注(UMS) 
![weixin](doc/weixin.png)
------
## 二、`maven`：
```xml
<dependency>
    <groupId>top.dcenter</groupId>
    <artifactId>ums-spring-boot-starter</artifactId>
    <version>[2.2.0,)</version>
</dependency>
```
------
## 三、`TODO List`:
- 1. 拆分微服务, OAuth2 authenticate server
------
## 四、`快速开始(Quick Start)`：
### 1. 添加依赖(Add Dependency):
```xml
<!-- 用户管理脚手架(ums) -->
<dependency>
    <groupId>top.dcenter</groupId>
    <artifactId>ums-spring-boot-starter</artifactId>
    <version>[2.2.0,)</version>
</dependency>

```
### 2. config:  
```yaml
server:
  port: 9090

spring:
  profiles:
    active: dev
  # mysql
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://127.0.0.1:3306/ums?useSSL=false&useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull&serverTimezone=Asia/Shanghai
    username: root
    password: 123456

  # session 简单配置
  session:
    # session 存储模式设置, 要导入相应的 spring-session 类的依赖, 默认为 none, 分布式应用把 session 放入 redis 等中间件
    store-type: none
    # session 过期时间
    timeout: PT300s

  # thymeleaf
  thymeleaf:
    encoding: utf-8
    prefix: classpath:/templates/
    suffix: .htm
    servlet:
      content-type: text/html;charset=UTF-8


# ums core
ums:
  # ================ 第三方授权登录相关配置 ================
  oauth:
    # 是否支持第三方授权登录功能, 默认: true
    enabled: true
    # 第三方服务商: providerId
    github:
      # 根据是否有设置 clientId 来动态加载相应 JustAuth 的 AuthXxxRequest
      client-id: 4d4ee00e82f669f2ea8d
      client-secret: 953ddbe871a08d6924053531e89ecc01d87195a8
    gitee:
      client-id: dcc38c801ee88f43cfc1d5c52ec579751c12610c37b87428331bd6694056648e
      client-secret: e60a110a2f6e7c930c2d416f802bec6061e19bfa0ceb0df9f6b182b05d8f5a58
    # 第三方登录授权登录 url 前缀, 不包含 ServletContextPath，默认为 /auth2/authorization.
    auth-login-url-prefix: /auth2/authorization
    # 第三方登录回调处理 url 前缀 ，也就是 RedirectUrl 的前缀, 不包含 ServletContextPath，默认为 /auth2/login.
    redirect-url-prefix: /auth2/login
    # 第三方登录回调的域名, 例如：http://localhost 默认为 "http://127.0.0.1"，
    # redirectUrl 直接由 {domain}/{servletContextPath}/{redirectUrlPrefix}/{providerId}(ums.oauth.[qq/gitee/weibo])组成
    domain: http://localhost:9090
    proxy:
      # 用于国内代理(HttpClient)超时, 默认 PT3S
      timeout: PT3S
      # 用于国外网站代理(HttpClient)超时, 默认 PT15S
      foreign-timeout: PT150S

  # RBAC 权限访问控制
  rbac:
    # ========= 放行权限 ==========
    # 权限表达式, 当 enableRestfulApi=true 且没有 @EnableGlobalMethodSecurity 注释时生效, 默认为 hasPermission(request, authentication).
    # hasPermission 表达式默认实现为 UriAuthoritiesPermissionEvaluator, 想自定义逻辑, 实现 PermissionEvaluator 即可替换.
    # String accessExp = "hasPermission(request, authentication)";
    # // 配置等效与
    # httpSecurity.authorizeRequests().anyRequest().access(hasPermission(request, authentication));
    restful-access-exp: permitAll()
    # 是否支持 restful Api (前后端交互接口的风格; 如: 查询(GET),添加(POST),修改(PUT),删除(DELETE)), 默认: true.
    # 当 {@code enableRestfulApi=false} 时 {@code accessExp} 权限表达式生效,
    # 当 {@code enableRestfulApi=true} 时 {@code restfulAccessExp} 权限表达式生效.
    enable-restful-api: true
  
  client:
    # ===================
    # 一级域名(不包括二级域名) 例如:
    #       domain: www.example.com -> topDomain: example.com
    #       domain: www.example.com.cn -> topDomain: example.com.cn
    #       domain: aaa.bbb.example.net -> topDomain: example.net
    # 测试时用的 IP 或 localhost 直接原样设置就行.
    # 在应用启动时通过 SecurityAutoConfiguration 自动注入 MvcUtil 字段 topDomain 中. 如在设置跨域 cookie 时可以通过 MvcUtil.getTopDomain() 方法获取.
    topDomain: localhost
    # ================ 密码登录, session, remember-me, csrf等配置 ================
    # 设置登录后返回格式(REDIRECT 与 JSON): 默认 JSON
    login-process-type: redirect
    # 登录页(必须自己实现)
    login-page: /login
    # 登录失败页(必须自己实现)
    failure-url: /login
    # 登录成功页(必须自己实现)
    success-url: /
    # 设置登出 url, 默认为 /logout
    logout-url: /logout
    # 设置登出后跳转的 url(必须自己实现), 默认为 /login
    logout-success-url: /login
    # 不需要认证的静态资源 urls, 例如: /resources/**, /static/**
    ignoring-urls:
      - /static/**
    # 不需要认证的 uri(可以带 HttpMethod 后缀; 用:隔开), 例如: /user/** 或 /user/**:post, 默认为 空 Set.
    permit-urls:
      - /hello:GET
      - /login
    # 设置登录时用户名的 request 参数名称, 默认为 username
    usernameParameter: username
    # 设置登录时用户密码的 request 参数名称, 默认为 password
    passwordParameter: password

  # ================ 验证码配置 ================
  # 同一个 uri 由多种验证码同时配置, **优先级**如下:
  #  `SMS > CUSTOMIZE > SELECTION > TRACK > SLIDER > IMAGE`
  codes:
    # 图片验证码
    image:
      # 设置需要图片验证码认证的 uri(必须是非 GET 请求)，多个 uri 用 “-” 或 ","号分开支持通配符，如：/hello,/user/*；默认为 /authentication/form
      auth-urls:
        - /authentication/form
      request-param-image-code-name: imageCode
    # 短信验证码
    sms:
      # 设置需要短信验证码认证的 uri(必须是非 GET 请求)，多个 uri 用 “，”号分开支持通配符，如：/hello,/user/*；默认为 /authentication/form
      auth-urls:
        - /authentication/mobile
      request-param-mobile-name: mobile
      request-param-sms-code-name: smsCode

  # ================ 手机登录配置 ================
  mobile:
    login:
      # 手机验证码登录是否开启, 默认 false，
      # 手机验证码登录开启后 必须配置 ums.codes.sms.auth-urls=/authentication/mobile
      sms-code-login-is-open: true
      # 手机验证码登录请求处理url, 默认 /authentication/mobile
      login-processing-url-mobile: /authentication/mobile

  # ================ 签到配置 ================
  sign:
    # redis key(String) 转 byte[] 转换时所用的 charset, 默认: StandardCharsets.UTF_8
    charset: UTF-8
    # 用于 redis 签到 key 前缀，默认为： u:sign:
    sign-key-prefix: 'u:sign:'
    # 用于 redis 总签到 key 前缀，默认为： total:sign:
    total-sign-key-prefix: 'total:sign:'
    # 获取最近几天的签到情况, 不能大于 28 天, 默认为 7 天
    last-few-days: 7
    # 用户签到 redis key TTL, 默认: 二个月 , 单位: 秒
    total-expired: 5356800
    # 用户签到统计 redis key TTL, 默认: 二个月 , 单位: 秒
    user-expired: 2678400


---
spring:
  profiles: dev
  mvc:
    throw-exception-if-no-handler-found: true
  thymeleaf:
    cache: false

#debug: true

server:
  port: 9090
  servlet:
    context-path: /demo
```
### 3. 实现(implement) UmsUserDetailsService 接口等:
#### UserDetailsService.java
```java
package top.dcenter.ums.security.core.demo.service;

import com.fasterxml.jackson.databind.DeserializationFeature;
import com.fasterxml.jackson.databind.ObjectMapper;
import lombok.extern.slf4j.Slf4j;
import me.zhyd.oauth.model.AuthUser;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.AuthorityUtils;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserCache;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;
import org.springframework.web.context.request.ServletWebRequest;
import top.dcenter.ums.security.common.enums.ErrorCodeEnum;
import top.dcenter.ums.security.core.api.service.UmsUserDetailsService;
import top.dcenter.ums.security.core.exception.RegisterUserFailureException;
import top.dcenter.ums.security.core.exception.UserNotExistException;

import java.util.List;

/**
 *  用户密码与手机短信登录与注册服务：<br><br>
 *  1. 用于第三方登录与手机短信登录逻辑。<br><br>
 *  2. 用于用户密码登录逻辑。<br><br>
 *  3. 用户注册逻辑。<br><br>
 * @author YongWu zheng
 * @version V1.0  Created by 2020/9/20 11:06
 */
@Service
@Slf4j
public class UserDetailsServiceImpl implements UmsUserDetailsService {

    /**
     * 用户名
     */
    public static final String PARAM_USERNAME = "username";

    /**
     * 密码
     */
    public static final String PARAM_PASSWORD = "password";

    private final ObjectMapper objectMapper;

    private final JdbcTemplate jdbcTemplate;

    @SuppressWarnings("SpringJavaAutowiredFieldsWarningInspection")
    @Autowired(required = false)
    private UserCache userCache;
    /**
     * 用于密码加解密
     */
    @SuppressWarnings("SpringJavaAutowiredFieldsWarningInspection")
    @Autowired
    private PasswordEncoder passwordEncoder;

    public UserDetailsServiceImpl(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
        this.objectMapper = new ObjectMapper();
        objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
    }

    @SuppressWarnings("AlibabaUndefineMagicConstant")
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

        try
        {
            // 从缓存中查询用户信息:
            // 从缓存中查询用户信息
            if (this.userCache != null)
            {
                UserDetails userDetails = this.userCache.getUserFromCache(username);
                if (userDetails != null)
                {
                    return userDetails;
                }
            }
            // 根据用户名获取用户信息

            // 获取用户信息逻辑。。。
            // ...

            // 示例：只是从用户登录日志表中提取的信息，
            log.info("Demo ======>: 登录用户名：{}, 登录成功", username);
            return new User(username,
                            passwordEncoder.encode("admin"),
                            true,
                            true,
                            true,
                            true,
                            AuthorityUtils.commaSeparatedStringToAuthorityList("ROLE_VISIT, ROLE_USER"));

        }
        catch (Exception e)
        {
            String msg = String.format("Demo ======>: 登录用户名：%s, 登录失败: %s", username, e.getMessage());
            log.error(msg, e);
            throw new UserNotExistException(ErrorCodeEnum.QUERY_USER_INFO_ERROR, e, username);
        }
    }


    @Override
    public UserDetails registerUser(String mobile) throws RegisterUserFailureException {

        if (mobile == null)
        {
            throw new RegisterUserFailureException(ErrorCodeEnum.MOBILE_NOT_EMPTY, null);
        }

        // 用户信息持久化逻辑。。。
        // ...

        log.info("Demo ======>: 手机短信登录用户 {}：注册成功", mobile);

        User user = new User(mobile,
                             passwordEncoder.encode("admin"),
                             true,
                             true,
                             true,
                             true,
                             AuthorityUtils.commaSeparatedStringToAuthorityList("ROLE_VISIT, ROLE_USER")
        );

        // 把用户信息存入缓存
        if (userCache != null)
        {
            userCache.putUserInCache(user);
        }

        return user;
    }

    @Override
    public UserDetails registerUser(ServletWebRequest request) throws RegisterUserFailureException {

        String username = getValueOfRequest(request, PARAM_USERNAME, ErrorCodeEnum.USERNAME_NOT_EMPTY);
        String password = getValueOfRequest(request, PARAM_PASSWORD, ErrorCodeEnum.PASSWORD_NOT_EMPTY);
        // ...

        // UserInfo userInfo = getUserInfo(request)

        // 用户信息持久化逻辑。。。
        // ...

        String encodedPassword = passwordEncoder.encode(password);

        log.info("Demo ======>: 用户名：{}, 注册成功", username);
        User user = new User(username,
                             encodedPassword,
                             true,
                             true,
                             true,
                             true,
                             AuthorityUtils.commaSeparatedStringToAuthorityList("ROLE_VISIT, ROLE_USER")
        );

        // 把用户信息存入缓存
        if (userCache != null)
        {
            userCache.putUserInCache(user);
        }

        return user;

    }

    @Override
    public UserDetails registerUser(AuthUser authUser, String username, String defaultAuthority) throws RegisterUserFailureException {

        // 第三方授权登录不需要密码, 这里随便设置的, 生成环境按自己的逻辑
        String encodedPassword = passwordEncoder.encode(authUser.getUuid());

        List<GrantedAuthority> grantedAuthorities = AuthorityUtils.commaSeparatedStringToAuthorityList(defaultAuthority);

        // ... 用户注册逻辑

        log.info("Demo ======>: 用户名：{}, 注册成功", username);

        // @formatter:off
        UserDetails user = User.builder()
                               .username(username)
                               .password(encodedPassword)
                               .disabled(false)
                               .accountExpired(false)
                               .accountLocked(false)
                               .credentialsExpired(false)
                               .authorities(grantedAuthorities)
                               .build();
        // @formatter:off

        // 把用户信息存入缓存
        if (userCache != null)
        {
            userCache.putUserInCache(user);
        }

        return user;
    }

    @Override
    public UserDetails loadUserByUserId(String userId) throws UsernameNotFoundException {
        UserDetails userDetails = loadUserByUsername(userId);
        User.withUserDetails(userDetails);
        return User.withUserDetails(userDetails).build();
    }

    @Override
    public List<Boolean> existedByUserIds(String... userIds) throws UsernameNotFoundException {
        // ... 在本地账户上查询 userIds 是否已被使用
        return List.of(true, false, false);
    }

    private String getValueOfRequest(ServletWebRequest request, String paramName, ErrorCodeEnum usernameNotEmpty) throws RegisterUserFailureException {
        String result = request.getParameter(paramName);
        if (result == null)
        {
            throw new RegisterUserFailureException(usernameNotEmpty, request.getSessionId());
        }
        return result;
    }
}

```

#### UserController.java
```java
package top.dcenter.ums.security.core.demo.controller;

import lombok.extern.slf4j.Slf4j;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import top.dcenter.ums.security.core.permission.config.EnableUriAuthorize;

import java.util.HashMap;
import java.util.Map;

/**
 *
 * @author YongWu zheng
 * @version V1.0  Created by 2020/9/20 20:04
 */
@Controller
@Slf4j
@EnableUriAuthorize()
public class UserController {

    @GetMapping("/login")
    public String login() {
        return "login";
    }

    @GetMapping("/")
    public String index(@AuthenticationPrincipal UserDetails userDetails, Model model) {
        if (userDetails != null)
        {
            model.addAttribute("username", userDetails.getUsername());
            model.addAttribute("roles", userDetails.getAuthorities());
        }
        else
        {
            model.addAttribute("username", "anonymous");
            model.addAttribute("roles", "ROLE_VISIT");
        }
        return "index";
    }

    @GetMapping("/me")
    @ResponseBody
    public Object getCurrentUser(@AuthenticationPrincipal UserDetails userDetails, Authentication authentication) {
        
        Map<String, Object> map = new HashMap<>(16);
        map.put("authenticationHolder", SecurityContextHolder.getContext().getAuthentication());
        map.put("userDetails", userDetails);
        map.put("authentication", authentication);
        return map;
    }

}
```
  
### 4. 前端页面 :
#### login.htm: 放在 classpath:/templates/
```html
<!DOCTYPE html>
<html xmlns:th="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>登录</title>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/jquery@1.11.1/dist/jquery.min.js"></script>

</head>
<body>
<h2>登录页面</h2>
<h3>表单登录</h3>
<h5>如果短信验证码与图片验证码同时配置时，优先使用短信验证码，图片验证码失效</h5>
<!-- 通过 th:action 的方式支持 csrf 或者 添加隐藏域<input type="hidden" th:name="${_csrf.parameterName}" th:value="${_csrf.token}"/> -->
<form id="reg-form" th:action="@{/authentication/form}" method="post">
    <table>
        <tr>
            <td>用户名：</td>
            <td><input type="text" name="username" value="admin" ><p style="color: #ff0000"
                                                                     id="error-name"></p></td>
        </tr>
        <tr>
            <td>密码：</td>
            <td><input type="password" name="password" value="admin"></td>
        </tr>
        <tr>
            <td>图形验证码：</td>
            <td>
                <input type="text" name="imageCode">
                <img class="img" th:src="@{/code/image}" style="width: 67px; height: 23px">
            </td>
        </tr>
        <tr>
            <td ><input type="checkbox" name="rememberMe" checked="true">记住我</input></td>
            <td><p style="color: #ff0000" id="error-code"></p></td>
        </tr>
        <tr>
            <td ><button id="btn-reg" type="button">登录ajax</button></td>
            <!-- 通过 form submit 不能接收错误信息, 通过 ajax 可接收错误信息 -->
            <td ><button type="submit">登录</button></td>
        </tr>
    </table>
</form>
<h3>手机登录</h3>
<form id="mobile-form" th:action="@{/authentication/mobile}" method="post">
    <table>
        <tr>
            <td>手机号码：</td>
            <td>
                <input type="tel" name="mobile" value="13345678980"><p style="color: #ff0000"
                                                                       id="error-name-mobile"></p>
                <a th:href="@{/code/sms?mobile=13345678980}" >发送验证码</a>
            </td>
        </tr>
        <tr>
            <td>手机验证码：</td>
            <td>
                <input type="text" name="smsCode">
            </td>
        </tr>
        <tr>
            <td ><input type="checkbox" name="rememberMe" checked="true">记住我</input></td>
            <td><p style="color: #ff0000" id="error-code-mobile"></p></td>
        </tr>
        <tr>
            <td ><button id="btn-mobile" type="button">登录ajax</button></td>
            <!-- 通过 form submit 不能接收错误信息, 通过 ajax 可接收错误信息 -->
            <td ><button type="submit">登录</button></td>
        </tr>
    </table>
</form>
<br><br>
<h3>社交登录</h3>
<a th:href="@{/auth2/authorization/gitee}">gitee登录</a>
<a th:href="@{/auth2/authorization/github}">github登录</a>
<a th:href="@{/auth2/authorization/gitee}">github登录</a>

<dev id="basePath" th:basePath="@{/}" style="display: none"/>
</body>
<script>
    var basePath = $("#basePath").attr("basePath");
    $.fn.serializeObject = function()
    {
        let o = {};
        let a = this.serializeArray();
        $.each(a, function() {
            if (o[this.name]) {
                if (!o[this.name].push) {
                    o[this.name] = [o[this.name]];
                }
                o[this.name].push(this.value || '');
            } else {
                o[this.name] = this.value || '';
            }
        });
        return o;
    }

    $(".img").click(function(){
        let uri = this.getAttribute("src");
        console.log(uri)
        let end = uri.indexOf('?', 0);
        console.log(end)
        if (end === -1) {
            uri = uri + '?'+ Math.random();
        } else {
            uri = uri.substring(0, end) + '?'+ Math.random();
        }
        console.log(uri)
        this.setAttribute('src', uri);
    });


    function submitFormByAjax(url, formId, errorNameId, errorCodeId, imgId, refresh) {
        return function () {
            console.log(JSON.stringify($(formId).serializeObject()))
            $.ajax({
                // 如果用的是模板，则 url 可以使用注入的方式，会跟着配置动态改变
                url: url,
                data: JSON.stringify($(formId).serializeObject()),
                type: "POST",
                dataType: "json",
                success: function (data) {
                    $(errorNameId).text("")
                    $(errorCodeId).text("")
                    console.log("==========注册成功============")
                    // 注册成功
                    // ...
                    console.log(data)
                    let uri = data.data.targetUrl
                    if (uri === null) {
                        uri = basePath
                    }
                    window.location.href = uri;
                },
                error: function (data) {
                    // 注册失败
                    $(errorNameId).text("")
                    $(errorCodeId).text("")
                    console.log("********注册失败*********")
                    console.log(data)
                    data = data.responseJSON
                    if (undefined !== data) {
                        console.log(data);
                        // 错误代码看ErrorCodeEnum
                        if (data.code >= 900 && data.code < 1000) {
                            $(errorNameId).text(data.msg)
                        } else if (data.code >= 600 && data.code < 700) {
                            $(errorCodeId).text(data.msg)
                        }
                    }
                    if (refresh) {
                        $(imgId).trigger("click");
                    }
                }
            })
            return
        };
    }


    $("#btn-mobile").click(
        submitFormByAjax($("#mobile-form").attr("action"), "#mobile-form", "#error-name-mobile", "#error-code-mobile", ".img-mobile", true)
    )


    $("#btn-reg").click(
        submitFormByAjax($("#reg-form").attr("action"), "#reg-form", "#error-name", "#error-code", ".img", true)
    )

</script>
</html>
```
#### index.htm
```html
<!DOCTYPE html>
<html xmlns:th="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
hello <span th:text="${username}">world!</span><br>
roles: <span th:text="${roles}"/>
    <!-- 通过 th:action 的方式支持 csrf 或者 添加隐藏域<input type="hidden" th:name="${_csrf.parameterName}" th:value="${_csrf.token}"/> -->
    <form th:action="@{/logout?logout}" method="post">
        <input type="submit" value="退出登录post"/>
    </form>
</body>
</html>
```
### 5. 访问前端页面
- 浏览器访问 `http://localhost:9090/demo/login`, 至此集成了：登录校验，验证码、手机登录、第三方登录(JustAuth)、基于 RBAC 的 uri 访问权限控制功能, 签到等功能; 实现快速开发。
- 此 `Quick Start` 代码在 `demo 模块` -> [quickStart](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/quickStart), 其他功能的详细配置说明参照: [Configurations](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-1%E3%80%81%E5%9F%BA%E6%9C%AC%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE)。
------

## 五、接口使用说明(`Interface instructions`):

### 实现对应功能时需要实现的接口(The interface that needs to be implemented when the corresponding function is present)：  
  
1. 用户服务(user service): `必须实现(Must implemente)`
   - [UmsUserDetailsService](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/service/UmsUserDetailsService.java)    

2. 访问权限控制功能(Access control function): 基于 RBAC 的访问权限控制: 支持多租户与SCOPE
    - [UriAuthorizeService](https://github.com/ZeroOrInfinity/UMS/blob/master/rbac/src/main/java/top/dcenter/ums/security/core/api/permission/service/UriAuthorizeService.java): `推荐通过实现 AbstractUriAuthorizeService 来实现此接口`
    - [AbstractUriAuthorizeService](https://github.com/ZeroOrInfinity/UMS/blob/master/rbac/src/main/java/top/dcenter/ums/security/core/api/permission/service/AbstractUriAuthorizeService.java): `必须实现(Must implemente)`
        
        - uri(资源) 访问权限控制服务接口抽象类, 定义了基于(角色/多租户/SCOPE)的访问权限控制逻辑. 实现 AbstractUriAuthorizeService 抽象类并注入 IOC
         容器即可替换 DefaultUriAuthorizeService.  
        - 注意: 
        
          1\. 推荐实现 AbstractUriAuthorizeService 同时实现 UpdateAndCacheRolesResourcesService 更新与缓存权限服务, 有助于提高授权服务性能. 
          
          2\. 对传入的 Authentication 的 authorities 硬性要求: 
          ```java
           // 此 authorities 可以包含:  [ROLE_A, ROLE_B, ROLE_xxx TENANT_110110, SCOPE_read, SCOPE_write, SCOPE_xxx]
           // authorities 要求:
           //    1. 角色数量    >= 1
           //    2. SCOPE 数量 >= 0
           //    3. 多租户数量  = 1 或 0
           Collection<? extends GrantedAuthority> authorities = authentication.getAuthorities();
          ```          
          3\. 此框架默认实现 `hasPermission(Authentication, HttpServletRequest)` 
          方法访问权限控制, 通过 `UriAuthoritiesPermissionEvaluator` 实现, 使用此接口的前提条件是: 应用使用的是 restful 风格的 API; 
          如果不是 restful 风格的 API, 请使用 `hasPermission(Authentication, String, String)` 接口的访问权限控制, 
          此接口使用注解的方式 `@PerAuthorize("hasPermission('/users', 'list')")` 来实现, 使用注解需先开启 `@EnableGlobalMethodSecurity(prePostEnabled = true)` 注解.
          
    - [UpdateAndCacheRolesResourcesService](https://github.com/ZeroOrInfinity/UMS/blob/master/rbac/src/main/java/top/dcenter/ums/security/core/api/permission/service/UpdateAndCacheRolesResourcesService.java):    

        - 用于更新或缓存基于(角色/多租户/SCOPE)角色的权限的服务接口, 每次更新角色的 uri(资源)权限时,需要调用此接口, 推荐实现此 RolePermissionsService 接口, 会自动通过 AOP
         方式实现发布 UpdateRolesResourcesEvent 事件, 从而调用 UpdateAndCacheRolesResourcesService 对应的方法.
        - 建议:
         
            1\. 基于 角色 的权限控制: 实现所有角色 uri(资源) 的权限 Map(role, map(uri, Set(permission))) 的更新与缓存本机内存. 
            
            2\. 基于 SCOPE 的权限控制: 情况复杂一点, 但 SCOPE 类型比较少, 也还可以像 1 的方式实现缓存本机内存与更新. 
            
            3\. 基于 多租户 的权限控制: 情况比较复杂, 租户很少的情况下, 也还可以全部缓存在本机内存, 通常情况下全部缓存内存不现实, 只能借助于类似 redis 等的内存缓存.
         
    - [RolePermissionsService](https://github.com/ZeroOrInfinity/UMS/blob/master/rbac/src/main/java/top/dcenter/ums/security/core/api/permission/service/RolePermissionsService.java):    

        - 更新与查询基于(角色/多租户/SCOPE)的角色资源服务接口. 主要用于给角色添加权限的操作. 
        - 注意: 
        
            1\. 在添加资源时, 通过PermissionType.getPermission() 来规范的权限格式, 因为要支持 restful 风格的 Api, 
                在授权时需要对 HttpMethod 与对应的权限进行匹配判断 
            
            2\. 如果实现了 UpdateAndCacheRolesResourcesService 接口, 未实现 RolePermissionsService 接口, 
                修改或添加基于"角色/多租户/SCOPE "的资源权限时一定要调用 UpdateAndCacheRolesResourcesService 对应的方法, 有两种方式: 一种发布事件, 另一种是直接调用对应服务; 
            ```java
            // 1. 推荐用发布事件(异步执行)
            applicationContext.publishEvent(new UpdateRolesResourcesEvent(true, ResourcesType.ROLE));
            applicationContext.publishEvent(new UpdateRolesResourcesEvent(true, ResourcesType.TENANT));
            applicationContext.publishEvent(new UpdateRolesResourcesEvent(true, ResourcesType.SCOPE));
            // 2. 直接调用服务
            // 基于角色
            UpdateAndCacheRolesResourcesService.updateAuthoritiesOfAllRoles();
            // 基于多租户
            UpdateAndCacheRolesResourcesService.updateAuthoritiesOfAllTenant();
            // 基于 SCOPE
            UpdateAndCacheRolesResourcesService.updateAuthoritiesOfAllScopes();
            ```
             
            3\. 实现此 RolePermissionsService 接口, 不需要执行上两种方法的操作, 已通过 AOP 方式实现发布 UpdateRolesResourcesEvent 事件.
            
            4\. 注意: RolePermissionsServiceAspect 切面**生效前提**, 事务的 `Order` 的值**必须 大于 1**, 如果是默认事务(优先级为 Integer.MAX_VALUE
                )不必关心这个值, 如果是自定义事务, 且设置了 Order 的值, 那么值**必须 大于 1**.
                
    - 时序图
    
![时序图](https://github.com/ZeroOrInfinity/UMS/raw/master/doc/SequenceDiagram/permission.png?raw=true)  


3. 短信验证码(SMS validate code): `默认空实现`
    - [SmsCodeSender](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/validate/code/sms/SmsCodeSender.java)

4. 图片验证码(image validate code): 已实现缓存功能, 支持定时刷新缓存功能, 可以自定义缓存验证码图片的输出路径与缓存数量
    - [ImageCodeFactory](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/validate/code/image/ImageCodeFactory.java)

5. 滑块验证码(Slider validate code): 已实现缓存功能, 支持定时刷新缓存功能, 可以自定义缓存验证码图片的输出路径与缓存数量, 支持自定义源图片路径与模板图片路径(源图片与模板图片参考[validate-code-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/validate-code-example))
    - [SimpleSliderCodeFactory](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/validate/code/slider/SliderCodeFactory.java) 

6. 自定义验证码(customize validate code):
    - [AbstractValidateCodeProcessor](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/validate/code/AbstractValidateCodeProcessor.java)
    - [ValidateCodeGenerator](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/validate/code/ValidateCodeGenerator.java)

7. [Auth2StateCoder](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/state/service/Auth2StateCoder.java): `用户需要时实现`, 对第三方授权登录流程中的 state 进行自定义编解码. 可以传递必要的信息, 
     如: 第三方登录成功的跳转地址等 注意此接口的两个方法必须同时实现对应的编解码逻辑, 实现此接口后注入 IOC 容器即可, 如有前端向后端获取 authorizeUrl
     时向后端传递额外参数 且用作注册时的信息, 需配合 UmsUserDetailsService.registerUser(AuthUser, String, String, String) 方法实现.

8. [Auth2UserService](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/service/Auth2UserService.java): 获取第三方用户信息的接口, 一般**不需要用户实现**, 除非想自定义获取第三方用户信息的逻辑, 实现此接口注入 IOC 容器即可替代.

9. [UsersConnectionRepository](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/repository/jdbc/UsersConnectionRepository.java): 第三方授权登录的第三方用户信息增删改查, 绑定与解绑及查询是否绑定与解绑接口, 一般**不需要用户实现**. 
     除非想自定义获取第三方用户信息的逻辑, 实现此接口注入 IOC 容器即可替代.

10. [UsersConnectionTokenRepository](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/repository/jdbc/UsersConnectionTokenRepository.java): 第三方授权登录用户 accessToken 信息表增删改查接口, 一般**不需要用户实现**. 
      除非想自定义获取第三方用户信息的逻辑, 实现此接口注入 IOC 容器即可替代.

11. [ConnectionService](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/signup/ConnectionService.java): 第三方授权登录用户的注册, 绑定, 更新第三方用户信息与 accessToken 信息的接口, 一般**不需要用户实现**.
      除非想自定义获取第三方用户信息的逻辑, 实现此接口注入 IOC 容器即可替代.

12. 自定义 OAuth2 Login 扩展接口: 内置两个自定义 providerId(ums.oauth.customize 与 ums.oauth.gitlabPrivate)
    
    - [AuthGitlabPrivateSource](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/justauth/customize/AuthGitlabPrivateSource.java): 抽象类, 实现此自定义的 AuthGitlabPrivateSource 且注入 ioc 容器的同时, 必须实现 AuthCustomizeRequest , 会自动集成进 OAuth2 Login 逻辑流程中, 只需要像 JustAuth 默认实现的第三方登录一样, 配置相应的属性(ums.oauth.gitlabPrivate.[clientId|clientSecret]等属性)即可.
    
    - [AuthCustomizeSource](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/justauth/customize/AuthCustomizeSource.java): 抽象类, 实现此自定义的 AuthCustomizeSource 且注入 ioc 容器的同时, 必须实现 AuthCustomizeRequest , 会自动集成进 OAuth2 Login 逻辑流程中, 只需要像 JustAuth 默认实现的第三方登录一样, 配置相应的属性(ums.oauth.customize.[clientId|clientSecret]等属性)即可.
    
    - [AuthCustomizeRequest](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/oauth/justauth/customize/AuthCustomizeRequest.java): 抽象类, 实现此自定义的 AuthCustomizeRequest 同时, 必须实现 AuthCustomizeSource 或 AuthGitlabPrivateSource 且注入 ioc 容器, 会自动集成进 OAuth2 Login 逻辑流程中, 只需要像 JustAuth 默认实现的第三方登录一样, 配置相应的属性(ums.oauth.customize.[clientId|clientSecret]等属性)即可.

13. 自定义前后端认证 token 以及通信方式

    - [BaseAuthenticationSuccessHandler](https://github.com/ZeroOrInfinity/UMS/blob/master/src/main/java/top/dcenter/ums/security/core/api/authentication/handler/BaseAuthenticationSuccessHandler.java): 认证成功处理器
    
    - [BaseAuthenticationFailureHandler](https://github.com/ZeroOrInfinity/UMS/blob/master/src/main/java/top/dcenter/ums/security/core/api/authentication/handler/BaseAuthenticationFailureHandler.java): 认证失败处理器

14. 如果应用为多租户系统, 且使用 RememberMe 功能: 默认的 RememberMeServices 不支持多租户, 则需要自定义实现 `org.springframework.security.web
.authentication.RememberMeServices` 接口, 使其支持多租户系统, 不过一般情况下多租户系统不使用 RememberMe 功能.

15. [TenantContextHolder](https://github.com/ZeroOrInfinity/UMS/blob/master/commons/src/main/java/top/dcenter/ums/security/core/api/tenant/handler/TenantContextHolder.java):
    - 多租户上下文存储器. 实现此接口并注入 IOC 容器后, 会自动注入 UMS 默认实现的注册/登录/授权组件, 要实现 ums 框架具有多租户功能, 必须实现此接口并注入 IOC 容器.
    
    - 功能: 
    
        1\. `tenantIdHandle(HttpServletRequest, String)`从注册用户入口或登录用户入口提取 `tenantId` 及进行必要的逻辑处理(如: `tenantId` 存入 `ThreadLocal`
        , 或存入 `session`, 或存入 `redis` 缓存等). 
        
        2\. `getTenantId()`方便后续用户注册、登录、授权的数据处理(如：`sql` 添加 `tenantId` 的条件，注册用户添加 `TENANT_tenantId` 权限，根据 `tenantId` 获取角色的权限数据).

        3\. `getTenantId(Authentication)` 默认实现方法, 用户已登录的情况下, 获取租户 ID, 直接从 `authority` 中解析获取.

    - 注意: 
        1\. 多租户系统中, 在未登录时需要用到 tenantId 的接口, 如: `UserCache.getUserFromCache(String)/UmsUserDetailsService` 等接口, 
        可通过 `getTenantId()` 来获取 `tenantId`. 登录用户可以通过 `Authentication` 来获取 `tenantId`.
        
        2\. UMS 默认的登录与注册逻辑中, 都内置了 `TenantContextHolder.tenantIdHandle(HttpServletRequest, String)` 逻辑, 
        用户在实现 `UserCache/UmsUserDetailsService` 等接口中需要 `tenantId` 时, 调用 `TenantContextHolder.getTenantId()` 方法即可.
        
        3\. 如果自定义的注册或登录逻辑, 需要自己先调用 `TenantContextHolder.tenantIdHandle(HttpServletRequest, String)` 逻辑, 再在
        实现 `UserCache/UmsUserDetailsService` 等接口中需要 `tenantId` 时, 调用 `TenantContextHolder.getTenantId()` 方法即可.
      

------
## 六、Configurations:

| **功能(Features)**                                                     | **模块(model)**                                                 | **demo模块--简单配置(Simple Configuration)**                                       | **demo模块--详细配置(detail Configuration)**                                       |
| ------------------------------------------------------------ | -------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1. [基本功能](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-1%E3%80%81%E5%9F%BA%E6%9C%AC%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     | [basic-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-example/src/main/resources/application.yml) |                                                              |
| 2. [登录路由功能](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-2%E3%80%81%E7%99%BB%E5%BD%95%E8%B7%AF%E7%94%B1%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 3. [session](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-3%E3%80%81Session-%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [session-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/session-detail-example/src/main/resources/application.yml) |
| 4. [remember-me](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-4%E3%80%81Remember-me-%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 5. [csrf](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-5%E3%80%81CSRF-%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 6. [anonymous](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-6%E3%80%81Anonymous-%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 7. [验证码](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-7%E3%80%81%E9%AA%8C%E8%AF%81%E7%A0%81%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [validate-code-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/validate-code-example/src/main/resources/application.yml) |
| 8. [手机登录](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-8%E3%80%81%E6%89%8B%E6%9C%BA%E7%99%BB%E5%BD%95%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 9. [第三方登录](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-9%E3%80%81%E7%AC%AC%E4%B8%89%E6%96%B9%E7%99%BB%E5%BD%95%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core) |   | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 10. [给第三方登录时用的数据库表 user_connection 与 auth_token 添加 redis cache](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-10.-%E7%BB%99%E7%AC%AC%E4%B8%89%E6%96%B9%E7%99%BB%E5%BD%95%E6%97%B6%E7%94%A8%E7%9A%84%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A1%A8-user_connection-%E4%B8%8E-auth_token-%E6%B7%BB%E5%8A%A0-redis-cache) | [core](https://github.com/ZeroOrInfinity/tree/master/core) |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 11. [签到](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-11%E3%80%81%E7%AD%BE%E5%88%B0%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [basic-detail-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/basic-detail-example/src/main/resources/application.yml) |
| 12. [基于 RBAC 的访问权限控制功能](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-13%E3%80%81%E5%9F%BA%E4%BA%8E-RBAC-%E7%9A%84%E8%AE%BF%E9%97%AE%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6%E5%8A%9F%E8%83%BD%E5%8A%9F%E8%83%BD%E9%85%8D%E7%BD%AE) | [core](https://github.com/ZeroOrInfinity/tree/master/core)     |                                                              | [permission-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/permission-example/src/main/resources/application.yml) |
| 13. [线程池配置](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-14%E3%80%81%E7%BA%BF%E7%A8%8B%E6%B1%A0%E9%85%8D%E7%BD%AE) | [core](https://gitee.com/pcore/UMS/tree/master/core)     |                                                              | [justAuth-security-oauth2-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/justAuth-security-oauth2-example/src/main/resources/application.yml) |
| 14. [基于 SLF4J MDC 机制的日志链路追踪配置](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AD-15%E3%80%81%E5%9F%BA%E4%BA%8E-SLF4J-MDC-%E6%9C%BA%E5%88%B6%E7%9A%84%E6%97%A5%E5%BF%97%E9%93%BE%E8%B7%AF%E8%BF%BD%E8%B8%AA%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7) | [core](https://gitee.com/pcore/UMS/tree/master/core)     |                                                              | [justAuth-security-oauth2-example](https://github.com/ZeroOrInfinity/UMS/tree/master/demo/justAuth-security-oauth2-example/src/main/resources/application.yml) |


------
## 七、[`注意事项(NOTE)`](https://github.com/ZeroOrInfinity/UMS/wiki/%E4%B8%83%E3%80%81%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9): 

### 1\. HttpSecurity 配置问题：UMS 中的 [HttpSecurityAware](https://github.com/ZeroOrInfinity/blob/master/commons/src/main/java/top/dcenter/ums/security/common/api/config/HttpSecurityAware.java) 配置与应用中的 HttpSecurity 配置冲突问题：

1. 如果是新建应用添加 HttpSecurity 配置, 通过下面的接口即可: 
    - [HttpSecurityAware](https://github.com/ZeroOrInfinity/UMS/blob/master/commons/src/main/java/top/dcenter/ums/security/common/api/config/HttpSecurityAware.java)
2. 如果是已存在的应用：
    - 添加 HttpSecurity 配置, 通过下面的接口即可: `HttpSecurityAware`
    - 已有的 HttpSecurity 配置, 让原有的 HttpSecurity 配置实现此接口进行配置: `top.dcenter.security.core.api.config.HttpSecurityAware`

![核心配置逻辑](doc/SequenceDiagram/securityConfigurer.png) 

### 2\. 在 ServletContext 中存储的属性: 

- 属性名称: SecurityConstants.SERVLET_CONTEXT_PERMIT_ALL_SET_KEY
- 属性值: Set<UriHttpMethodTuple>, 把权限类型为 PERMIT_ALL 的 Set 存储在 servletContext .
      
### 3\. servletContextPath 的值存储在 [MvcUtil](https://github.com/ZeroOrInfinity/blob/master/core/src/main/java/top/dcenter/ums/security/core/util/MvcUtil.java)`.servletContextPath` : 

- 通过静态方法获取 `MvcUtil.getServletContextPath()`
- `MvcUtil.servletContextPath` 的值是通过: [SecurityAutoConfiguration](https://github.com/ZeroOrInfinity/blob/master/core/src/main/java/top/dcenter/ums/security/core/config/SecurityAutoConfiguration.java)`#afterPropertiesSet()` 接口注入
    
### 4\. 验证码优先级(Verification code Priority): 

- 同一个 uri 由多种验证码同时配置, **优先级**如下:
  `SMS > CUSTOMIZE > SELECTION > TRACK > SLIDER > IMAGE`
  
### 5\. Jackson 序列化与反序列化

- 添加一些 Authentication 与 UserDetails 子类的反序列化器, 以解决 redis 缓存不能反序列化此类型的问题,
具体配置 redis 反序列器的配置请看 [RedisCacheAutoConfiguration.getJackson2JsonRedisSerializer()](https://github.com/ZeroOrInfinity/UMS/blob/master/src/main/java/top/dcenter/ums/security/core/oauth/config/RedisCacheAutoConfiguration.java) 方法.

```java
// 示例
Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
ObjectMapper objectMapper = new ObjectMapper();
// Auth2Jackson2Module 为此项目实现的反序列化配置     
objectMapper.registerModules(new CoreJackson2Module(), new WebJackson2Module(), new Auth2Jackson2Module());
jackson2JsonRedisSerializer.setObjectMapper(om);
```
- 注意: [UmsUserDetailsService](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/api/service/UmsUserDetailsService.java)
的注册用户方法返回的 `UserDetails` 的默认实现 `User` 已实现反序列化器, 如果是开发者**自定义的子类**, **需开发者自己实现反序列化器**.

------
## 八、[Properties Configurations](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8)

| **属性配置列表(Properties Configurations)**                                             |
| ------------------------------------------------------------ |
| [基本属性(Basic Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [签到属性(Sign Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [手机登录属性(Mobile login Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [验证码属性(Validate Code Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [第三方授权登录(OAuth2 JustAuth)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [线程池属性(ThreadPool Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [基于 SLF4J MDC 机制的日志链路追踪属性](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [第三方授权登录用户信息数据 redis 缓存配置(UserConnection Redis cache Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
| [第三方授权登录用户信息表 user_connection sql 配置(UserConnection sql Properties)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%85%AB%E3%80%81%E5%B1%9E%E6%80%A7%E9%85%8D%E7%BD%AE%E5%88%97%E8%A1%A8) |
------
## 九、参与贡献(Participate in contribution)

1. Fork 本项目
2. 新建 Feat_xxx 分支
3. 提交代码
4. 新建 Pull Request
------
## 十、[流程图(Flow chart)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%8D%81%E3%80%81%E6%B5%81%E7%A8%8B%E5%9B%BE:-%E9%9A%8F%E7%9D%80%E7%89%88%E6%9C%AC%E8%BF%AD%E4%BB%A3%E4%BC%9A%E6%9C%89%E5%87%BA%E5%85%A5): 随着版本迭代会有出入

### 1. 滑块验证码(sliderValidateCode)

![sliderValidateCode](doc/sliderFlow.png)

------
## 十一、[时序图(Sequence Diagram)](https://github.com/ZeroOrInfinity/UMS/wiki/%E5%8D%81%E4%B8%80%E3%80%81%E6%97%B6%E5%BA%8F%E5%9B%BE:-%E9%9A%8F%E7%9D%80%E7%89%88%E6%9C%AC%E8%BF%AD%E4%BB%A3%E4%BC%9A%E6%9C%89%E5%87%BA%E5%85%A5): 随着版本迭代会有出入

| **时序图**                                                   |
| ------------------------------------------------------------ |
| [csrf](doc/SequenceDiagram/crsf.png)                         |
| [获取验证码逻辑](doc/SequenceDiagram/getValidateCode.png)    |
| [图片验证码逻辑](doc/SequenceDiagram/ImageValidateCodeLogin.png) |
| [logout](doc/SequenceDiagram/logout.png)                     |
| [第三方授权登录](doc/SequenceDiagram/OAuth2Login-justAuth.png)        |
| [rememberMe](doc/SequenceDiagram/rememberMe.png)             |
| [核心配置逻辑](doc/SequenceDiagram/securityConfigurer.png)   |
| [登录路由](doc/SequenceDiagram/securityRouter.png)           |
| [session](doc/SequenceDiagram/session.png)                   |
| [手机登录](doc/SequenceDiagram/SmsCodeLogin.png)             |
| [授权逻辑时序图](doc/SequenceDiagram/permission.png)             |
| [过时:第三方绑定与解绑](doc/SequenceDiagram/OAuth2Banding.png)    |
| [过时:第三方授权登录](doc/SequenceDiagram/OAuth2Login.png)        |
| [过时:第三方授权登录注册](doc/SequenceDiagram/OAuth2SignUp.png)   |


## 十二、基于 SLF4J MDC 机制的日志链路追踪功能

- 使用此功能在日志配置文件中的 `pattern` 中添加 `%X{MDC_TRACE_ID}` 即可.
```xml
<!-- 控制台 -->
<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <!-- 日志格式 -->
    <encoder>
        <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} %-5level ${PID:- } --- [%thread] %X{MDC_TRACE_ID} %logger[%L] - %msg%n</pattern>
        <charset>utf-8</charset>
    </encoder>
    <!--此日志appender是为开发使用，只配置最底级别，控制台输出的日志级别是大于或等于此级别的日志信息-->
    <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
        <!-- 只有这个日志权限才能看，sql语句 -->
        <level>DEBUG</level>
    </filter>
</appender>
```
- 自定义 `SLF4J MDC` 机制实现日志链路追踪 id 的类型: 可通过属性 ums.mdc.type 定义:
```yaml
# 基于 SLF4J MDC 机制实现日志链路追踪 id 的类型, 默认为 uuid. 当需要自定义 id 时, type = MdcIdType.CUSTOMIZE_ID, 再实现 MdcIdGenerator.getMdcId() 方法, 注入 IOC 容器即可.
ums:
  mdc:
    type: UUID/THREAD_ID/SESSION_ID/CUSTOMIZE_ID
```
当 ums.mdc.type = CUSTOMIZE_ID 时 需要实现接口 MdcIdGenerator[MdcIdGenerator](https://github.com/ZeroOrInfinity/UMS/blob/master/mdc/src/main/java/top/dcenter/ums/security/core/api/mdc/MdcIdGenerator.java) 并注入 IOC 容器.


- 多线程使用问题: 父线程新建子线程之前调用 `MDC.getCopyOfContextMap()` 方法获取 `MDC context`, 子线程在执行操作前先调用 
`MDC.setContextMap(context)` 方法将父线程的 `MDC context` 设置到子线程中. ThreadPoolTaskExecutor 的配置请参考 [ScheduleAutoConfiguration](https://github.com/ZeroOrInfinity/UMS/blob/master/core/src/main/java/top/dcenter/ums/security/core/tasks/config/ScheduleAutoConfiguration.java).
- 多线程传递 MDC context 简单示例:  
```java
final Logger log = LoggerFactory.getLogger(this.getClass());
// 获取父线程 MDC 中的内容
final Map<String, String> context = MDC.getCopyOfContextMap();
final Runnable r = () -> {
    log.info("testMDC");
    System.out.println("...");
};
new Thread(() -> {
    // 将父线程的 MDC context 设置到子线程中
    MDC.setContextMap(context);
    r.run();
}, "testMDC").start();
```

## 鸣谢
##### 感谢 JetBrains 提供的免费开源 License：
![JetBrains](doc/jetBrains.png)
