# Tony Report

[在线demo][demo]

我很懒，不想编写数据导出代码，有没有像bootstrap-table-export.js这样的工具呢？只需要配置下，想导出啥就导出啥。可bootstrap-table-export是通过前端js将数据转换成报表文件的，数据多点就歇菜了。没办法，只能自己写了。简单配置后，只需在Controller方法上添加注解@DataProvider，然后就自动支持CSV，Excel，PDF等报表的导出功能了，通过后端分页查询方式导出，还有记录数最大阀值设置，安全又可靠。

## Getting Started

Download the latest JAR via Maven:
```xml
<dependency>
    <groupId>org.tony.framework.report</groupId>
    <artifactId>tony-report-core</artifactId>
    <version>${tony-report.version}</version>
<dependency>
    <groupId>org.tony.framework.report</groupId>
    <artifactId>tony-report-excel</artifactId>
    <version>${tony-report.version}</version>
</dependency>
<dependency>
    <groupId>org.tony.framework.report</groupId>
    <artifactId>tony-report-pdf</artifactId>
    <version>${tony-report.version}</version>
</dependency>
```
## Config

开启功能, 并添加Excel和PDF类型导出功能, 默认只支持导出CSV类型

```java
@Configuration
@Import({ DelegatingDataConfiguration.class, DelegatingReportConfiguration.class })
public class DataConfig extends ReportConfigurerAdapter {

	@Override
	public void configureReportBuilders(List<ReportBuilder> reportBuilders) {
        //添加扩展
		reportBuilders.add(new DefaultExcelReportBuilder());
		reportBuilders.add(new DefaultPdfReportBuilder());
	}
}
```
## 扩展

实现ReportBuilder接口，可以轻松扩展报表生成类型，比如支持html, word类型等等

```java
/**
 * 报表创建者
 * 
 * @author tony.deng
 */
public interface ReportBuilder {

	/**
	 * 是否支持当前的文件扩展名
	 * 
	 * @param extension 文件扩展名
	 * @return
	 */
	boolean supportsExtension(String extension);

	/**
	 * 生成报表
	 * 
	 * @param out 输出流
	 * @param template 报表模板
	 * @param dataProvider 数据提供者
	 * @throws Exception
	 */
	void build(OutputStream out, Template template, DataProvider dataProvider)
			throws Exception;

}
```

## Demo

```java
    @DataProvider
    @ResponseBody
    @RequestMapping(value = "/test")
    public Page page(HttpServletRequest request, PageInfo pageInfo){
        ......
    }
```

[在线demo][demo]

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

 [mail]: mailto:dz_005@163.com
 [demo]: http://report.dengzhi.vip