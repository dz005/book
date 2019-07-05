# Tony Wiki

我很懒，不想在WIKI系统上编写和维护Http接口文档。swagger？我的懒超出你的想象，我连swagger注解都懒得学，懒得写。那就写个懒人专用HTTP接口文档平台吧。

和swagger对比：

| swagger    |  tony wiki |
| ------  | ------ |
| 支持servlet，SpringMVC等多种框架|只支持SpringMVC注解|
| 需要引入swagger架包|通过Maven插件方式生成文档，无jar依赖|
| 通过自定义注解生成文档，有代码侵入性|只通过SpringMVC注解生成文档，无侵入|
| 需要写swagger注解，增加了工作量|无工作量增加|
| 文档分散|文档统一收集，平台展示|
| 文档查看权限无控制|按部门，团队，人员授权|
| 简单测试接口|保存测试用例，批量测试，生成测试报告|

技术方案已敲定，正在开发中，敬请期待......

UI部分将会参考 [tony-http-ui](../tony-http/tony-http-ui.md)

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

 [mail]: mailto:dz_005@163.com