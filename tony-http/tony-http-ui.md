# Tony Http UI

[在线demo][demo]

基于tony-http-annotation自定义注解自动生成文档，采用插件方式部署，通过jarslink实现类加载隔离，spring容器隔离，通过MDC和SiftingAppender实现日志隔离。
支持：
* 插件式热部署
* jar依赖分析
* 接口文档自动生成
* 接口测试
* 接口Mock
* 执行日志在线查看
* ......

## 概念图

![tony-http-ui](../images/tony-http/tony-http-ui.png)

## UI

![tony-http-ui](../images/tony-http/idx_1.png)
#### 新增插件
![tony-http-ui](../images/tony-http/idx_2.png)
### 重新安装插件
![tony-http-ui](../images/tony-http/idx_3.png)
### 重新加载插件
![tony-http-ui](../images/tony-http/idx_4.png)
### jar依赖列表
![tony-http-ui](../images/tony-http/idx_5.png)
### 接口列表
![tony-http-ui](../images/tony-http/idx_6.png)
### 模型列表
![tony-http-ui](../images/tony-http/idx_7.png)
![tony-http-ui](../images/tony-http/idx_8.png)
### 环境配置
可以配置平台环境(mock环境)，开发环境，测试环境，预发环境
可以配置 时间戳(变量)，签名(变量)，appId，token等公共请求参数
![tony-http-ui](../images/tony-http/idx_9.png)
### 文档列表
![tony-http-ui](../images/tony-http/wiki.png)
### 接口测试
![tony-http-ui](../images/tony-http/test_1.png)
### 执行结果
![tony-http-ui](../images/tony-http/test_2.png)
### Header信息
![tony-http-ui](../images/tony-http/test_3.png)
### 执行耗时分析
![tony-http-ui](../images/tony-http/test_4.png)

[在线demo][demo]

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

[mail]: mailto:dz_005@163.com
[demo]: http://gateway-wiki.dengzhi.vip