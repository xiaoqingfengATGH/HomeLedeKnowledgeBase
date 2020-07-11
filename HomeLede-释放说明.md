### v2020.07.11(DEV) 

[版本下载点这里](https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede%E7%89%88%E6%9C%AC%E5%8F%91%E5%B8%83)

**重大升级：内核升级至v5.4.50**

- 除Luci外，其他软件源全部适配至 openwrt 开发分支

- 变更代码超过全部代码70%

- 跨代升级会获得许多好处，也会带来一些潜在问题，需要一段时间慢慢发现调整。

- HomeLede 自行维护的软件源，以及HomeLede固件内置的方案已经初步完成了适配，目前已经可以在v5.x内核版本工作。

- HomeLede 源码仓库主分支（master）仍旧是4.19.123内核，最后一个tag v2020.07.02是最近验证编译通过的v4.19.123版本

- HomeLede v5.x内核源码由k5分支维护，待v5.x分支稳定后，会合并回master分支

- 已验证正常工作功能（欢迎补充反馈）：

  - 综合DNS方案：AdGuardHome、dnsmasq（附带dnsmasq-china-list加速脚本）、chinadns-ng、smartdns、dnscrypt-proxy2

  - UPnP - 摄像头、Steam、BitComet、迅雷X、电驴

  - Docker

  - DDNS - noip.com 、dnspod.cn 正常

  - SSH - 密码、Ed25519、Sftp

  - Passwall - VPS + HomeLede内置海内外解析模式 + 访问控制  + 黑白名单

  - PPPoE 拨号

  - 单线多拨

  - 多拨负载均衡（mwan3）

  - 防火墙 - 端口转发（至内网主机、TCP及UDP）、端口开放

  - 定时任务

  - Turbo ACC 网络加速

    ![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/v5Test/10.UPnP1.jpg)

    ![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/v5Test/10.UPnP2.jpg)

#### **内置组件升级**

+ dnsmasq-china-list 升级至 1.0-6
  
  支持从国内源更新配置，支持下载配置完整性校验，规避配置文件下载不完整导致dnsmasq异常
  
+ **Passwall凤凰涅槃，重新回归！升级至3.9-xiaoqingfengMod-7  20200706**
  
  + 支持直接使用HomeLede内置海内外分流解析
  + 支持劫持Dnsmasq上游
  + 优化tcping逻辑
  + socks节点可选择同tcp节点
  + 修复passwall服务端初始化问题
  + 优化passwall订阅脚本
  + 适配HomeLede暗黑系风格界面
  + 支持使用v2ray 实现分流
  + 支持trojan go
  + 支持trojan plus

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/PSW/v20200705.png)

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/PSW/20.v2ray_shunt.png)

+ KCPTUN 升级至v20200701
+ miniupnpd 升级至 2.1.20200510-5
+ mwan3升级至2.87-1
+ dropbear升级至2020.80-1
+ dnscrypt升级至2.0.44
+ docker-ce升级至19.03.12-2
+ ttyd升级至1.6.0-2
+ luci-app-ttyd升级至1.0-3
+ sqm-scripts升级至1.4.0-8
+ kmod-shortcut-fe 高通开源 转发加速
+ v2ray升级至 4.26.0
+ 增加snmpd 5.8-1 （解决做旁路由时，爱快显示mac地址冲突问题）

#### **软件包**

+ SSR+ 升级至 20200709
+ 网易云音乐解锁 Go 版本，也可以选择高音质了
+ qBittorrent 升级到 v4.2.5
+ luci-app-serverchan 升级至1.78-8

#### **优化及缺陷修正**

- IPSec VPN Server 可完美与各种分流软件共存（无需Docker版本，替刚开发的Docker版本默哀...）
- docker-ce 移除iptables规则时不会输出错误信息
- docker-ce 无法使用预置配置
- CPU 评分算法更新
- 修复 CPU 温度显示及调整显示内容

### v2020.06.27(DEV：开发中间版本，非正式发布)

#### **内置组件升级**

分流底层组件升级

+ v2ray 4.25.1

#### **软件包**

+ frps增加ACL，兼容最新LUCI标准

#### **优化及缺陷修正**

- IPSec VPN Server Docker版升级，修正接入用户管理无效的缺陷
- PSW首页适配暗黑风格（见下图）
- PSW内置规则更新至最新
- HomeClash默认不启动UDP转发

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/PSW/10.global_dark_theme.png)

#### **驱动**

+ 支持RTL8125B 2.5G网卡
+ 支持Mellanox Connect-X 40Gbps 网卡

### v2020.06.20

#### **内置组件升级**

+ 增强原生 IPSec VPN Server，实现一个服务端全终端接入（安卓、苹果、Windows、Mac）。

  + 支持IKEv2协议与Mschapv2认证，装备证书后实现Windows10接入。

  + 支持自定义VPN客户端IP地址

  + 支持自定义VPN客户端DNS

  + 支持VPN客户端直接使用家庭网络IP（直接使用家庭网络DHCP）

    **仅适合实现快速接入家庭网络，不适合VPN客户端共享家庭局域网中各种分流（PSW、Clash等）软件，如需要与分流协同工作，请使用Docker版**。

+ 提供基于Docker的IPSec VPN Server方案，实现一个服务端全终端接入（安卓、苹果、Windows、Mac）。

  + 支持自定义VPN客户端IP地址
  + 支持自定义VPN客户端DNS
  + 支持与Clash、PSW协同工作，可实现VPN客户端共享家庭分流环境

    **IPSecVPN 应用方法请参考 -> [HomeLede IPSec VPN使用说明](https://github.com/xiaoqingfengATGH/HomeLede/wiki/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8IPSecVPN%E5%AE%9E%E7%8E%B0%E5%A4%9A%E7%AB%AF%E6%8E%A5%E5%85%A5%E5%AE%B6%E5%BA%AD%E7%BD%91%E7%BB%9C)**

+ dropbear支持ed25519密钥

+ docker升级至19.03.9

+ upnp小版本升级改善热插拔及接口处理逻辑

+ 可道云更新至2020.06.15

+ 分流底层组件升级

  + v2ray 4.24.2
  + ipt2socks 1.1.3
  + trojan 1.16.0

+ 分流组件

  + HomeClash规则例行升级，内核更新至2020.06.20最新

#### **内置组件新增**

+ 集成订阅地址转换器，可以转换各种分流软件代理格式 入口：http://192.168.1.1:10086/list
+ Docker图形客户端——dockerman v0.5.13
+ 支持7z格式压缩包解压

#### **软件包**

+ helloworld更新至2020.06.15
+ 增加KVM虚拟化QEMU Guest Agent
+ 网易云音乐解锁升级至2.3.5-6
+ frpc支持http2http
+ nextdns 升级至1.6.3

#### **优化及缺陷修正**

- 修正luci放弃配置更改页面，返回路径错误
- 调整防火墙及DDNS日志查看页面样式
- dnsmasq-china-list支持配置自动更新
- 调整AdGuardHome默认过滤列表，增补不过滤白名单

#### **驱动**

+ 提供Realtek r8168 GBE eth 网卡驱动



### v2020.05.27 Clash 预览版
+ 集成Clash作为分流首选软件，提供定制客户端HomeClash（基于openclash）,提供HomeClash分流规则（规则简介：https://github.com/xiaoqingfengATGH/homeclash/wiki/HomeClash%E8%A7%84%E5%88%99%E4%BB%8B%E7%BB%8D）
+ 提供开箱即用方案，可免除繁琐配置快速应用Clash（https://github.com/xiaoqingfengATGH/HomeLede/wiki/HomeLede-20200527-Clash%E9%A2%84%E8%A7%88%E7%89%88--%E5%BF%AB%E9%80%9FClash%E5%BC%80%E5%90%AF%E8%AF%B4%E6%98%8E）
+ 原4级DNS方案与Clash无缝集成，启动，关闭Clash无需调整DNS方案，仍旧可实现去恶意+分流解析+速度优选
+ 内置主题InfinityFreedom针对多款软件提供定制样式
+ 支持SQM、NFT Table QOS
+ 软件包-网易云音乐解锁升级，解决luci-app-frpc无权限问题，luci-app-adbyby-plus升级
+ 内核升级至4.19.122
+ ipt2socks升级至1.1.2
+ 修正并发多拨一个缺陷

### v2020.05.10
+ SmartDNS升级至Release31（2020.05.04），国内组DNS采用TCP 443及80端口测速
+ 增加家庭网络接入管控，可基于MAC黑白名单，按访问网站地址，按时间段控制设备接入
+ 系统DDNS功能重新开启阿里云解析脚本
+ 修正独立阿里云DDNS解析程序没有执行权限问题（注意：本应用已经停止更新，最近更新是2018年，仅为考虑部分网友使用习惯，失效后将移除）
+ 增加对谷歌国内站点dns加速解析脚本
+ 新增DNS菜单入口 ，汇总DNS相关软件
+ IPSec \/PN升级至5.8.4
+ Docker小版本升级
+ 软件包：网易云音乐解锁升级、NextDNS升级至1.5.7，酸酸乳等
+ 调整MWAN3在线检测地址配置，不再使用可能导致误判的海外地址
+ 修改部分默认设置，LAN DNS默认指向127.0.0.1，使用固件内置综合DNS方案
+ 百度网盘应用以软件包形式提供（已经长时间不更新，虽然可以使用但速度很慢，使用价值降低）

### v2020.04.29
+ 解决部分海外域名无法解析问题。4.26将海外组DNS替换为https dns proxy，但https dns proxy稳定性不佳，时有高CPU占用率情况出现，本次更新将海外组DNS由https dns proxy变更为dnscrypt-proxy。替换后，海外组解析稳定，google.com解析恢复正常。
+ 调整chinadns-ng发包策略以及smartdns、dnscrpty-proxy域名缓存策略。
+ smartdns更新至2020.4.19版本
+ 调整DNS各组件启动顺序
+ 切换aliyunddns应用，至坛友反馈有效的版本（感谢qqzwqq）

### v2020.04.26
+ 调整了DNS方案，引入https dns proxy作为海外组DNS入口，不再使用SmartDNS的第二DNS。
+ 移除了失效的国内DNS
+ 升级IPSec xPN
+ chinadns-ng升级至2020.4.10，更新chnroute，chnlist......list
+ Kcptun Luci App升级最新版
+ 提供单独的阿里云DDNS插件（解决DDNS内置阿里云无效问题）
+ WAN口支持PPTP及L2PT
+ 附加软件包：新增udpxy、pptp server、pppoe relay升级acme，还有部分组件包进行批量升级
+ InfinityFreedom主题优化显示细节及主流内核浏览器显示效果微调
+ 增加了固件主分区容量（推荐重新刷入！）


### v2020.04.19
+ 更新chinadns-ng至1.0-beta22
+ 提供定制infinityfreedom主题（HomeLede原创）
+ 修正IPSec接入家庭局域网后无法访问路由本身的问题
+ 内核升级4.19.115
+ 软件包frp升级

### v2020.04.12
+ 国内域名加速脚本升级至2020.04.11
+ smartdns升级至2020.04.06
+ Upnp 默认开启IGDv1模式
+ 提供图形化CIFS/SMB协议共享（NAS、Windows共享）目录挂载工具
+ 使用WatchCat替换原有定时重启功能（WatchCat可以在断网超过一段时间之后或者按固定时间重启，功能超过原定时重启功能）
+ kcptun 升级至 20200409
+ 软件包qBittorrent升级至v4.2.3,PSW升级3.6-40，酸酸乳+升级
+ 以软件包形式临时提供aliddns独立应用，解决少部分坛友反馈内置ddns中阿里ddns失效的问题
+ 软件包提供acme（Let's Encrypt 证书自动更新），accesscontrol（访问控制），airplay2（苹果airplay2协议支持），Diskman（管理RAID4，5，6），music-remote-center（远程控制音乐播放），多种BT下载工具等等应用（尚有一些，就不一一列出了，请在固件下载中查看软件包列表）

### v2020.04.06
+ 以软件包形式提供ServerChan（微信推送）
+ PSW升级，解决订阅导致无法上网问题
+ 升级多线负载均衡组件
+ 禁用AdGuard DNS缓存（改善PSW开启关闭时对DNS变化感知速度）
+ Docker不再开启seccomp
+ 按要求重新打开IPV6

### v2020.04.04
+ 修正国内域名加速脚本部分缺陷
+ 内置打印机共享，ZeroTier
+ 新增多套主题
+ SMARTDNS LUCI缺陷修正
+ UPNP 升级至2.1.20191006
+ Mount.CIFS升级至6.10
+ PSW升级
+ 移除了影响docker自动创建防火墙规则的软件包

### v2020.03.19

+ 增加了IPSec 方案，便于苹果、安卓手机连入家庭网络
+ 内核版小版本升级，必备软件缺陷修正
+ 按大家要求增补了软件包，adbyebye+等

### v2020.03.21

+ 基于OpenWrt（LEDE）R2020.3.19
+ docker-ce升级至19.03.8
+ 初步解决了Docker-ce启动不自动创建iptables规则，导致使用bridge模式容器无法上网的问题
+ 增加了Aria2下载工具（全能下载工具，HTTP，BT，磁力链等等，路由挂载NAS后可实现远程下载到NAS）
+ 应大家要求以软件包形式提供了qBittorrent、frpc、frps、zerotier等等软件
+ Dropbear升级至2019.78-1

### v2020.03.16

+ 基于OpenWrt（LEDE）R2020.3.11
+ 提供恶意网站过滤+国内域名加速解析+ 抗污染 + 速度优选 方案，可与PSW无缝集成