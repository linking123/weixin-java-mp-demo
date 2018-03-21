
### 项目引用

本项目 clone 自[weixin-java-tools](https://github.com/wechat-group/weixin-java-tools)。


### 使用步骤：

1. 配置: 复制/src/main/resources/wx.properties.template 生成 wx.properties 文件，填写相关配置;     
1. 使用maven运行程序: `mvn jetty:run`  或者自己打war包发布到tomcat运行；
1. 配置微信公众号中的接口地址：http://xxx/wechat/portal （注意XXX需要是外网可访问的域名，需要符合微信官方的要求）；
1. 根据自己需要修改各个handler的实现，加入自己的业务逻辑（我的业务都放在schoolmanager/controller中）。


### 项目框架

核心类：
- WxMenuController 微信公众号菜单管理类
- WxMpPortalController 微信消息接收类


### 记录

- [开发过程中问题](devRecords/problems.md)
- [过程记录](devRecords/devProgress.md)
- [公众号测试相关](devRecords/WeChatTestAccountAndProcess.md)
- [公众号申请相关](devRecords/weChatApply.md


### 完整的Spring MVC框架

另一个Repository[WeChat_Official_Account_SpringMVC_demo](https://github.com/linking123/WeChat_Official_Account_SpringMVC_demo)