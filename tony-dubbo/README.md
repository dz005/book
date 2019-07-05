# Tony Dubbo

[在线demo][demo]

我很懒，不想编写dubbo接口的单元测试代码，有没有一个工具能让我只录接口参数值就可以测试dubbo接口呢？找了半天也没找到，那就自己动手写个dubbo测试平台吧。原理就是从私服上下载service-api架包，然后盘它，解析出接口方法和参数信息，再通过dubbo的泛化调用方式调接口。再加上测试用例保存，用例分组，批量测试，测试报告生成等功能，一个简单的dubbo在线测试平台就做好了

## 遇到的问题
+ 问题描述: 用jarlink做dubbo隔离的时候,发现返回结果反序列化偶尔会出现ClassNotFoundException
+ 原因分析: dubbo的线程模型是异步的,请求消息和响应消息可能由不同的线程处理,无法通过Thread.currentThread()获取到正确的ClassLoader
+ 解决方案：优化返回结果的反序列化逻辑,从Invoker的Interface上获取ClassLoader


感谢@Jerrick Zhu的merge
![tony-dubbo](../images/tony-dubbo/merge_1.png)

![tony-dubbo](../images/tony-dubbo/merge_2.png)

![tony-dubbo](../images/tony-dubbo/merge_3.png)

## UI
### 配置dubbo服务jar的GAV
![tony-dubbo](../images/tony-dubbo/1.png)
### 配置项目
![tony-dubbo](../images/tony-dubbo/2.png)
### 关联接口
![tony-dubbo](../images/tony-dubbo/3.png)
### 添加测试用例
![tony-dubbo](../images/tony-dubbo/4.png)
### 批量测试
![tony-dubbo](../images/tony-dubbo/5.png)

[在线demo][demo]

## Feedback

如果有好的意见或者建议，欢迎随时与[tony.deng][mail]沟通.

 [mail]: mailto:dz_005@163.com
 [demo]: http://dubbo.dengzhi.vip/view/dubbo/providerList
