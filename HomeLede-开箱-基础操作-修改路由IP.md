###### 本文适用场景

+ 使用HomeLede的DHCP为家庭网络分配地址

+ 使用HomeLede内置DNS方案作为家庭网络DNS

最典型的使用场景：HomeLede作为家庭网络唯一路由的，即符合上述条件。

其他场景，如做旁路由等等，请大家根据你自己的需要，决定是否使用HomeLede的DHCP及DNS，并根据实际情况调整配置。



### 操作方法

**操作关键在于修改路由IP地址同时，同步修改DHCP服务公开的DNS地址，否则家庭网络设备将会收到指向旧路由IP地址的DNS信息，导致无法解析请求而无法上网。**

介绍两种修改方式，通过图形界面及命令行。如无法访问图形界面，请使用命令行方式修改。

#### 通过图形界面修改

“网络”->“接口”，在右侧上方找到“LAN”，修改下方的“IPV4地址”，为你期望的地址。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/IP_DHCP_1.jpg)

接下来，同一个页面向下滚动，找到“DHCP服务器”，打开“高级设置”，在DHCP选项中填入“6,你期望的地址”。注意，数字6，英文逗号后面跟你新的路由IP地址。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/IP_DHCP_2.jpg)

随后，点击右下角”保存&应用“。

**最后，重新启动路由！请一定要重新启动一次路由！**

”系统“，”重启“，点击右侧”执行重启“。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/REBOOT.jpg)

#### 通过命令行修改

在路由终端上按回车键，激活命令行。以下以将路由IP修改为192.168.5.1为例。

首先，修改路由LAN的IP，输入命令如下：

```
uci set network.lan.ipaddr='192.168.5.1' 
uci commit network
```

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/IP_DHCP_CMD1.jpg)

接下来，修改路由DHCP公开网关地址：

```
uci delete dhcp.lan.dhcp_option
uci add_list dhcp.lan.dhcp_option='6,192.168.5.1'
uci commit dhcp
```

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/IP_DHCP_CMD2.jpg)

最后，重启路由。输入重启命令后等待约10s，路由会自动重启，全部步骤完成。

```
reboot
```

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/IP_DHCP_CMD3.jpg)