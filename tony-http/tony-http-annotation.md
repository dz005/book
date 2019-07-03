Tony Http Annotation
======

一套仿SpringMvc的自定义注解

Getting Started
--------

Download [the latest JAR][3] via Maven:
```xml
<dependency>
  <groupId>org.tony.framework</groupId>
  <artifactId>tony-http-annotation</artifactId>
  <version>0.0.3</version>
</dependency>
```
or Gradle:
```groovy
compile 'org.tony.framework:tony-http-annotation:0.0.3'
```

Snapshots of the development version are available in [Sonatype's `snapshots` repository][snap].


Config
--------

在网关项目的springContext-beans.xml中添加配置信息并开启功能:
```xml
<!-- 开启HTTP注解功能 -->
<bean class="org.tony.framework.http.server.config.DelegatingHttpConfiguration"/>
<!-- 开启网关功能 -->
<bean class="org.tony.framework.http.server.gateway.GatewayConfiguration"/>
```

Annotations
--------

注解中的 title 和 description属性分别对应在线wiki中的含义和描述。

| 注解     |  必填    |描述    |
| ------  | ------ |------ |
| @ HttpComponent |是|带该注解的Bean才会被处理|
| @ Mapping|是|value指定requestURI, 请求方式默认为GET,POST|
| @ Get|是|继承 @ Mapping, 请求方式为GET|
| @ Post|是|继承 @ Mapping, 请求方式为POST|
| @ Param|否|value指定requestParameterName, required配置参数是否能为空，defaultValue 设置默认值(JSON格式)|
| @ ParamMap|否|将 requestParameterMap组装成POJO|
| @ Body|否|HTTP request body|
| @ CrossOrigin|否|支持跨域访问|
| @ Anonymous|否|支持匿名访问|
| @ Deprecated|否|接口已过期|
| @ Model|否| 标注POJO和枚举|
| @ Property |否| 标注属性Get方法|
| @ EnumConstant|否| 标注枚举常量|

Context
--------

可以通过 HttpContextHolder.getContext() 获取 Adapter方式中的所有入参，例如当前用户信息，当前UrlPath等。

因为采用的是线程局部变量方式获取，所以起多线程前请做传值，以免取不到值。

Demo
--------

```java
@HttpComponent(title = "DEMO服务")
@Service
public class DemoGateway {

	@CrossOrigin
	@Mapping(value = "/test", title = "测试接口", description = "测试用的接口")
	public Set<Map<String, Pojo>> test(@Param("param1") String param1,
			@Param(value = "param2", defaultValue = "[{\"pojo\":{\"a\":\"as\"}},{\"pojo\":{\"a\":\"sad\"}}]") Set<Map<String, Pojo>> param2,
			@Param(value = "param5", required = false) Date param3) {
		Pojo pojo = new Pojo();
		pojo.setA(param1);
		Pojo2 p2 = new Pojo2();
		p2.setPojo(pojo);
		System.err.println(HttpContextHolder.getContext().getUrlPath());
		System.err.println(param3);
		return param2;
	}

	@Anonymous
	@Get(value = "/test2", title = "测试接口2", description = "测试用的接口")
	public Collection<Map<String, Pojo>> test(@Param("param1") String param1,
			@Param(value = "param2", defaultValue = "[{\"pojo\":{\"a\":\"as\"}},{\"pojo\":{\"a\":\"sad\"}}]") Collection<Map<String, Pojo>> param2,
			@Param(value = "param5", required = false) Date param3) {
		Pojo pojo = new Pojo();
		pojo.setA(param1);
		Pojo2 p2 = new Pojo2();
		p2.setPojo(pojo);
		System.err.println(HttpContextHolder.getContext().getUrlPath());
		System.err.println(param3);
		return param2;
	}

	@Deprecated
	@Post(value = "/test3", title = "测试接口3", description = "测试用的接口")
	public List<Pojo2> test3(@Body ParamVO paramVO, Date param3) {
		Pojo pojo = new Pojo();
		pojo.setA(paramVO.getParam1());
		pojo.setDate(paramVO.getParam3());
		Pojo2 p2 = new Pojo2();
		p2.setPojo(pojo);
		paramVO.getParam2().add(p2);
		return paramVO.getParam2();
	}

}
```

标注POJO：

```java
@Model(title = "Pojo")
public class Pojo {

	private String a;
	private Date date;
	private MyEnum myEnum;

	@Property(title = "字段2")
	public String getA() {
		return a;
	}

	......
}
```

标注枚举：

```java
@Model(title = "枚举测试")
public enum MyEnum {

	@EnumConstant(title = "枚举")
	a, 
	@EnumConstant(title = "枚举b")
	b, 
	@EnumConstant(title = "枚举c")
	c, 
	@EnumConstant(title = "枚举d")
	d;
}
```

Feedback
--------

如果有好的意见或者建议，以及不明白的问题，欢迎随时与[tony.deng][mail]沟通.

 [1]: #
 [2]: #
 [3]: #
 [snap]: #
 [mail]: mailto:dengzhi@111.com.cn