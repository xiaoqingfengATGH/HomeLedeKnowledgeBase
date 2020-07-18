### HomeLede 快速设置指南

[版本下载点这里](https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede%E7%89%88%E6%9C%AC%E5%8F%91%E5%B8%83)

[释放说明点这里](https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede-%E9%87%8A%E6%94%BE%E8%AF%B4%E6%98%8E)

**固件设计思路：最大程度简化使用HomeLede作为家庭网络主路由、通过PPPoE拨号上网等最典型使用场景配置，实现开箱即用**

以下以**使用HomeLede作为家庭网络主路由方案**，介绍固件快速设置方法。

开始前，请确认已经重新刷入了固件，且网络物理连接正常（推荐使用网线连接软路由和电脑，确认网线，网口有效，LAN、WAN对应网口连接正确）。

- 如果使用光猫，建议将光猫设置为桥接模式，使用HomeLede拨号
- 如果光猫非桥接模式（光猫拨号），请确认光猫LAN（连接软路由WAN）口的IP地址，IP不要和固件默认192.168.1.1冲突，如果冲突修改光猫LAN地址或者 [修改HomeLede默认地址](https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede-%E5%BC%80%E7%AE%B1-%E5%9F%BA%E7%A1%80%E6%93%8D%E4%BD%9C-%E4%BF%AE%E6%94%B9%E8%B7%AF%E7%94%B1IP)
- 如果修改HomeLede默认IP地址，请按照固件附带文档的说明操作。（**请一定注意，除了修改固件LAN IP外，还需要同步修改固件DHCP服务公开DNS地址，修改完毕后，请一定重启一次路由**）



接下来，登录固件图形界面，默认地址是`http://192.168.1.1`，如果你修改了固件默认IP，则使用新地址登录。

在“网络”-“接口”中，配置好WAN。默认可能还有个WAN6直接删除。

- 通常WAN使用拨号，切换协议，PPPoE，随后输入用户名密码即可。
- 如果WAN使用DHCP（如光猫拨号，非桥接），观察WAN是否正确获得了地址。
- 如果WAN采用静态地址，填好上级分配的固定地址，子网掩码，DNS。



通常到了这步，即可正常上网了。固件自带的多级DNS方案（去广告、国内域名加速、国内外分流解析、缓存等等）已经预先配置完毕，并不需要额外操作。



如果你想对DNS再多做一些优化，则可以参考如下步骤，再次强调，以下步骤非必须，请在您了解相关知识的前提下操作。

1 **填入你ISP的DNS**。固件国内DNS解析采用的是最著名的4个公共DNS外加一个ISP的DNS的方式。可以打开SMARTDNS配置界面，将“CN-ISP #1”项目对应的IP修改成你ISP的主DNS地址。如果不想使用ISP的DNS，直接将这个项目前的的勾取消即可。操作完毕不要忘记点击页面右下角的“保存&应用”生效。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/DNS_SETTING_1.jpg)

2 **尝试启用非常规国内DNS解析**。如果你的ISP有非常严重的DNS劫持（典型，移动宽带，移动已经实现了全网DNS拦截），换句话说，在严重劫持环境下，普通DNS设置基本可以视为无效（所有发出的送往UDP 53端口的DNS请求都会被ISP统一拦截，并返回运营商预置的结果）。如果你厌恶这种行为，或者ISP的DNS解析结果影响了你的网络访问，可以考虑将固件国内DNS解析方式进行切换，规避ISP劫持。

如下图，固件在smartdns中预置了四个不使用标准UDP协议的国内DNS（国际早已实现DOH，无需考虑），如下图。两个是知名公共DNS的DOH解析，还有两个使用5353端口的DNS。

从目前情况看，这四个DNS可以规避国内ISP对标准DNS的劫持。

同样，如果切换了DNS，不要忘记点击页面右下角的“保存&应用”生效。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/DNS_SETTING_2.jpg)



#### 使用分流

- Passwall

  配置好节点，在Passwall首页，设置好TCP节点，其他保持固件默认（如下）即可。

  ![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/DNS_SETTING_3_PSW.jpg)

- Clash

  [点这里参考Clash快速开启指南](https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede-20200527-Clash%E9%A2%84%E8%A7%88%E7%89%88--%E5%BF%AB%E9%80%9FClash%E5%BC%80%E5%90%AF%E8%AF%B4%E6%98%8E)

