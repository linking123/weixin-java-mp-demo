## 测试服务器

192.168.96.211 root
域名：wechat.cloud.sun-create.com 

## 测试号  

### 微信测试号 配置

https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login&code=061zS1Jb1q1nju0GFAHb1p0UIb1zS1Jp&state=

### 测试号信息
- linking
- appID：wx64c2e6c309d3fc29
- appsecret：582a656adde8387cf46bac7c58580e8d

- pan
- appID：wx78e39d1e03c4aa21
- appsecret：ca95e2d4efba7c9dc0768819b3f5c352

- lixin
- appID：wx6c690923e33eb548
- appsecret：22194fd8211d0e3e739b5ce688dccb4c

### 接口配置信息

基于`ngrok`生成随机外网映射url
- URL: https://5753287e.ngrok.io/wechat/portal
- Token: wechattocken


### JS接口安全域名

- 域名: 5753287e.ngrok.io（随机）

### 测试号问题

#### 菜单生效时间 

菜单设置后24小时生效？重新关注无效；重启项目无效。

解决方法：可先调用删除菜单接口，删除菜单之后，取消关注；再调用生成菜单接口，重新关注

- 删除菜单接口: http://localhost:8093/wechat/menu/delete
- 生成菜单接口: http://localhost:8093/wechat/menu/create

#### 前端设计

前后端交互问题，前端框架用哪一套？框架用自己熟悉的，样式用微信提供的？

终极参考：https://weui.io/example/#/

注意weui.css版本问题，有v1.1.2和v0.4.2两个版本。

