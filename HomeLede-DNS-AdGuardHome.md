

固件内置AdGuardHome作为去广告方案。AdGuardHome基于DNS过滤方式，一次部署，全家庭内网生效。

去广告原理及常见技术对比，[请见这里](https://github.com/xiaoqingfengATGH/HomeLede/wiki/%E6%BC%AB%E8%B0%88%E5%8E%BB%E5%B9%BF%E5%91%8A%EF%BC%8C%E5%8E%9F%E7%90%86%E5%8F%8A%E9%81%BF%E5%9D%91%E6%8C%87%E5%8D%97)

去广告效果除了技术方案本身能力外，核心在于规则库。合理搭配，调整规则库，才可以获得较好的效果。

#### 如果之前没有使用过去广告，初次使用可能导致一些网站打不开，如何处理？

清理DNS缓存，任何人都可以胜任的清除方法：断开网络接口重连，重启电脑，重启路由。

#### 如果怀疑因为广告过滤，导致某些网站上不了，可以禁用广告过滤。

禁用方法：

[http://192.168.1.1:3000](http://192.168.1.1:3000/) 打开AdGuardHome管理界面（路由IP请根据实际情况修改）

用户密码都是root

首页，左上角接近Logo处，有”禁用保护“字样，点击即可禁用广告过滤，再次点击会打开。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/DNS/AdGuardHome1.jpg)

#### 如何调整规则库

勾选即为启用规则，取消勾选即为禁用。无需其他步骤。

启用状态规则，点击“检查更新”时才会更新。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/DNS/AdGuardHome2.jpg)

#### 如何解除部分域名拦截（应对误杀）

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/DNS/AdGuardHome3.jpg)

#### 判断某站点是否被AdGuardHome拦截

“过滤器”->“自定义过滤规则”页面下方，可以输入域名进行测试。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/DNS/AdGuardHome4.jpg)