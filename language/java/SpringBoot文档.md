## 基础配置

### YAML语法

```
基本规则：
	大小写敏感
	使用缩进表示层级关系
	缩进不允许使用tab键,只允许使用空格
	缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
数据结构：
  对象: 键值对的集合
  数组: 一组按次序排列的值
  纯量: 单个的，不可再分的值

```

- 基本规则：

  - 大小写敏感
  - 使用缩进表示层级关系
  - 缩进不允许使用tab键,只允许使用空格
  - 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可

- 数据结构：

  - 对象: 键值对的集合

  ```
  // kv
  hash:
      name: server
      foo: bar
  // 行内写法
  hash: { name: Steve, foo: bar }
  ```

  - 数组: 一组按次序排列的值

  ```
  // 连词线开头的行，构成一个数组
  list:
  	- Cat
  	- Dog
  	- Gold
  // 行内表示
  animal: [Cat, Dog]
  ```

  - 纯量: 单个的，不可再分的值

  ```
  字符串：
      (1) 字符串默认不使用引号表示
      str: 这是一行字符串
      (2) 字符串之中包含空格或特殊字符，需要放在引号之中。
      str: '内容： 字符串'
      (3)单引号和双引号都可以使用，双引号不会对特殊字符转义
      s1: '内容\n字符串'  js=> { s1: '内容\\n字符串' }
      s2: "内容\n字符串"  js=> { s2: '内容\n字符串' }
  布尔值
  isSet: true
  整数
  number: 23
  浮点数
  number: 23.0
  Null 用~表示
  parent: ~
  时间 采用 ISO8601 格式
  iso8601: 2001-12-14t21:59:43.10-05:00 
  日期
  date: 1976-07-31
  数据转换 允许使用两个感叹号，强制转换数据类型。
  e: !!str 123
  f: !!str true
  
  ```

  

### 多环境开发

- 开发环境   `dev`
  - win-dev
  - mac-dev
- 测试环境   `test`
- 预发布环境 `pre`
- 生产环境   `pro`

```yaml
// 创建不同环境文件 application-{active-name}.yml
spring:
  profiles:
    active: active-name
```



### 热部署

## WEB

### WEBMVC

### FLUX



## 安全框架

保证软件运行安全，包含的主要功能有

- 认证：用户认证就是判断一个用户的身份是否是合法的过程，用户去访问系统资源时系统要求验证用户的身份信息，身份合法可继续访问，不合法，拒绝访问。常用的认证方式有：账号密码登录、二维码登录、手机短信登录、指纹认证、刷脸登录登方式
- 会话：用户认证通过后，将创建会话，记录用户登录状态，直到退出；为了避免用户每次操作都将进行认证，常用的认证方式有基于Session的认证方式、基于token的方式

  基于Session的认证方式：用户认证成功后，在服务端生成用户相关的数据保存在session中，发送给客户端的session_id存放到Cookie中，这样用户客户端请求时带上session_id就可以验证服务器是否存在session数据，以此完成用户的合法校验，当用户退出系统或session过期销毁时，客户端的session_id也就无效了

  基于Token的认证方式：



- 授权

- 加密

### Spring Security

​		Spring Security应用级别的安全主要包含两个主要部分，即登录认证(Authentication)和访问授权(Authorization),首先用户登录的时候传入登录信息，登录验证器完成登录验证将用户信息存储到上下文，才能进行其它操作，如在进行访问授权时，权限认证器从上下文中获取登录信息，根据认证认证信息获取权限信息，通过权限信息和特定的授权决定是否授权

- 介绍

  认证、授权（权限控制）、加密、会话、缓存、remember me

- 基础

- 整合使用

初始验证功能



**Springboot配置**

```
1、引入依赖




```

- 分析

```

配置类
类 WebSecurityConfig extend WebSecurityConfigurerAdapter
方法
  void configure(HttpSecurity http)  处理url
  
  void configure(AuthenticationManagerBuilder auth)
  void configure(WebSecurity web)
	

类 MyUserDetails implements UserDetails
方法
  String getPassword()
  String getUsername()
  boolean isAccountNonExpired()
  boolean isAccountNonLocked()
  boolean isCredentialsNonExpired()
  boolean isEnabled()
  
加密验证
类 MyPasswordEncoder implements PasswordEncoder
方法
  String encode(CharSequence rawPassword)
  boolean matches(CharSequence rawPassword, String encodedPassword)
  
自定义我们的验证方法 
类 AuthenticationProviderServiceImpl implements AuthenticationProviderService
方法
  Authentication authenticate(Authentication authentication)
  boolean supports(Class<?> authentication)

```



- 技术源码

  - 实现技术

  Filter、Servlet、Spring DI、Spring AOP

  - 核心是通过一组过滤器链，项目启动后将自动配置。最核心的就是Basic Authentication Filter用来认证用户的身份

```
SpringSecurityFilterChain 的SpringBean FilterChainProxy, 特殊拦截器，
提供DelegatingFilterProxy过滤器，获取Ioc自动创建的FilterChainProxy对象,这个对象上有一个拦截器列表List，列表上存在用户验证的拦截器，跨站点请求伪造等拦截器，可以注册Filter，自定义拦截器，满足不同的需要





```



### Apache Shiro





### Spring Security与Shiro对比

- 功能

  认证、授权、加密、会话、缓存、rember me功能

- Spring Security基于Spring开发，项目中使用Spring作为基础，配合Spring Security做权限更加方便。而Shiro要和Spring进行整合
- Spring Security功能与Shiro更加丰富些，如安全防护方面
- Spring Security社区资源相对比Shiro更加丰富
- 如果使用Springboot, SpringCloud，三者可以无缝集成
- Shiro的配置和使用比较简单，SpringSecurity上手复杂
- Shiro依赖性低，不需要任何框架和容器，可以独立运行，而Spring Security依赖Spring容器









## JSON

### GJSON



### FASTJSON





### GJSON与FASTJSON比较



# 测试

Springboo测试



## `mockMvc使用`

### 获取`mockMvc`

```
@SpringBootTest
public class FileStoreControllerTest {

    private MockMvc mockMvc;

    @Autowired
    private WebApplicationContext webApplicationContext;

    @BeforeEach
    public void beforeTestMethod() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
    }
}
```



### `get`

```
@Test
public void testGet() throws Exception {
    ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/file/getFileList")
        .accept(MediaType.ALL)
        .param("pageSize", "12")
        .param("pageNum", "1"));
    MockHttpServletResponse response = resultActions.andReturn().getResponse();
    String res = response.getContentAsString();
    System.out.println(res);
}
```



### `post`

```
@Test
public void testPost() throws Exception {
	Map<String, Object> map = new HashMap<>();
	map.put("aa", "bbb");
	MockHttpServletResponse response = mockMvc
			.perform(MockMvcRequestBuilders.post("/file/testPost").accept(MediaType.ALL)
					.content(JSON.toJSON(map).toString().getBytes()))
			.andReturn()
			.getResponse();
	String res = response.getContentAsString();
	System.out.println(res);
}
```

### `文件上传`

```
@Test
public void testUpload() throws Exception {
    String filePath = "E:\\Users\\Administrator\\Pictures\\公众号素材\\冷发抖.jpg";
    File file = new File(filePath);
    MockMultipartFile mockMultipartFile = new MockMultipartFile("file", file.getName(),
            MediaType.IMAGE_JPEG_VALUE, new FileInputStream(file));
    ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.multipart("/file/testUpload").file(mockMultipartFile));
    MvcResult mvcResult = resultActions.andReturn();
    String res = mvcResult.getResponse().getContentAsString();
    System.out.println(res);
}
```

### swagger教程

