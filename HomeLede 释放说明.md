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