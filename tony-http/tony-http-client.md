# tony-http-client

## HttpComponentScan处理

用httpComponentScanParser处理@HttpComponentScan，扫描出全部HttpComponentDefinition，然后通过ProxyFactory生成Proxy，注册到BeanFactoy.

```java
public class HttpComponentConfigurationPostProcessor implements MergedBeanDefinitionPostProcessor {

    ......

	@Override
	public void postProcessMergedBeanDefinition(RootBeanDefinition beanDefinition, Class<?> beanType, String beanName) {
		if (AnnotationUtils.findAnnotation(beanType, Configuration.class) != null) {
			Set<HttpComponentScan> componentScans = AnnotationUtils.getRepeatableAnnotations(beanType,
					HttpComponentScan.class, HttpComponentScans.class);
			if (!componentScans.isEmpty()) {
				Set<HttpComponentDefinition> definitions = new LinkedHashSet<HttpComponentDefinition>();
				for (HttpComponentScan componentScan : componentScans) {
					definitions.addAll(this.httpComponentScanParser.parse(componentScan, beanType.getName()));
				}
				if (!definitions.isEmpty()) {
					this.httpComponentRegister.register(definitions);
				}
			}
		}
	}
}
```

## HttpComponent注册器

通过httpClient.iface()生成代理对象，注册到beanFactory

```java
public class HttpComponentRegisterImpl implements HttpComponentRegister, BeanFactoryAware {
       

	@Override
	public void register(Collection<HttpComponentDefinition> definitions) {
		String beanName;
		String className;
		Class<?> beanType;
		for (HttpComponentDefinition definition : definitions) {
			beanName = definition.getBeanName();
			className = definition.getAnnotationMetadata().getClassName();
			try {
				if (beanFactory.containsBean(beanName)) {
					throw new IllegalStateException(
							"Could not register http component [" + className + "] under bean name '" + beanName
									+ "': there is already object [" + beanFactory.getBean(beanName) + "] bound");
				}
				beanType = Class.forName(className, true, beanFactory.getBeanClassLoader());
				beanFactory.registerSingleton(beanName,
						httpClient.iface(beanType, definition.getClientSecurer(), definition.getBaseURI()));
			} catch (Exception e) {
				Throwables.propagateIfPossible(e);
			}
		}
	}
}
```

## demo

服务提供者基于自定义注解声明接口，提供接口声明架包service-api.jar
```java
@HttpComponent(title = "DEMO服务")
public interface DemoApi {

    @Post(value = "/test", title = "测试接口", description = "测试用的接口")
    Set<Map<String, Pojo>> test(@Param("param1") String param1, @Param("param2) Set<Map<String, Pojo>> param2, @Param("param5") Date param3);

    @Get(value = "/test2", title = "测试接口2", description = "测试用的接口2")
    Pojo2 test2(@Param("param1") String param1, @Param(value = "param2" param2, @Param(value = "param5", required = false) Date param3);

    @Post(value = "/test3", title = "测试接口3", description = "测试用的接口3")
    List<Pojo2> test3(@Body List<ParamVO> paramVOs, @Param("param1") String param1);
}
```

服务消费者引入SDK：tony-http-client.jar + service-api.jar

配置启动HttpClient
```java
@Configuration
@HttpComponentScan(value = "org.tony.framework.http.client.sample", baseURI = "http://localhost:8082/")
@EnableHttpClient
public class HttpClientConfig {

}
```

通过@Resource或@Autowired注入
```java
public class GatewayTest extends TestBase {

    @Resource
    private DemoApi demoApi;

    @Test
    public void test2() throws Exception {
        System.out.println(demoApi.test2("test2", null, new Date()));
    }
}
```

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

 [mail]: mailto:dz_005@163.com
