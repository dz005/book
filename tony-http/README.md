Tony Http
======

一套简单的Http API调用框架，基于自定义注解，实现APP网关，开放平台，RPC客户端SDK，接口WIKI平台，接口测试，接口Mock

结构
--------

* [tony-http](tony-http/README.md)
	* [tony-http-annotation](tony-http/tony-http-annotation.md)
	* tony-http-server
		* [tony-http-server-core](tony-http/tony-http-server-core.md)
		* tony-http-server-gateway
		* tony-http-server-open-api
		* tony-http-server-adapter
	* [tony-http-client](tony-http/tony-http-client.md)
	* [tony-http-wiki](tony-http/tony-http-wiki.md)
    * [tony-http-test](tony-http/tony-http-test.md)
    * [tony-http-mock](tony-http/tony-http-mock.md)
    
+ 自定义注解：tony-http-annotation
+ APP网关：tony-http-annotation + tony-http-server-gateway
+ 开放平台：tony-http-annotation + tony-http-server-open-api
+ RPC客户端SDK：tony-http-annotation + tony-http-client
+ 接口WIKI：tony-http-annotation + tony-http-wiki
+ 接口测试：tony-http-annotation + tony-http-test
+ 接口Mock：tony-http-annotation + tony-http-mock


Feedback
--------

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

 [1]: #
 [2]: #
 [3]: #
 [snap]: #
 [mail]: mailto:dengzhi@111.com.cn