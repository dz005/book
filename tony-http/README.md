# Tony Http

[在线demo][demo]

一套简单的Http API调用框架，基于自定义注解，实现APP网关，开放平台，RPC客户端SDK，接口WIKI平台，接口测试，接口Mock

## 结构

* tony-http
	* tony-http-annotation
	* tony-http-server
		* tony-http-server-core
		* tony-http-server-gateway
		* tony-http-server-open-api
	* tony-http-client
	* tony-http-extra
		* tony-http-wiki
    	* tony-http-test
    	* tony-http-mock
    	* tony-http-ui
    

+ 自定义注解：tony-http-annotation
+ APP网关：tony-http-annotation + tony-http-server-gateway
+ 开放平台：tony-http-annotation + tony-http-server-open-api
+ RPC客户端SDK：tony-http-annotation + tony-http-client
+ 接口WIKI：tony-http-annotation + tony-http-wiki
+ 接口测试：tony-http-annotation + tony-http-test
+ 接口Mock：tony-http-annotation + tony-http-mock

## 概念图
![tony-http](../images/tony-http/tony-http.png)

## 应用

### 改造前
![before](../images/tony-http/before.png)

### 改造后
![after](../images/tony-http/after.png)

[在线demo][demo]

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

[mail]: mailto:dz_005@163.com
[demo]: http://gateway-wiki.dengzhi.vip