### 定义

端口转发是将一个网络接口上某端口的流量转发至另外一个网络接口的某端口的技术。在家庭路由上，常常用于将家庭网络内部设备直接开放到公共互联网上。

### 典型场景

如下图：

+ 家庭内网192.168.1.130是一台运行Windows的电脑，开启了3389端口的远程桌面服务，192.168.1.140运行着群晖的DSM，端口5000 。

+ 在HomeLede上设置端口转发，将路由上63389端口，转发到192.168.1.130的3389端口，将路由上55000端口转发到192.168.1.140的5000端口。

+ 此时，访问路由器IP+63389端口流量会被转发到192.168.1.130的3389，访问路由器IP+55000端口流量会被转发到192.168.1.140的5000。

  路由器IP可以是外网IP-202.96.36.34（WAN口）,也可以是内网IP（LAN口）192.168.1.1。

+ 通常为了访问方便，会为公网地址（WAN口）设置DDNS(即动态域名)，这样通过域名即可访问到路由的WAN口地址。

+ 在互联网上的设备，如手机，可以通过DDNS域名+63389访问家里192.168.1.130的3389（如使用微软远程桌面连接连回家中电脑），图中标号1，图中2也类似。

+ 家庭网络中主机，亦可以使用DDNS域名+55000访问192.168.1.140的5000。

  在家庭网络内部使用DDNS域名+端口转发时，流量实际经过了内部网络的LAN、随后到WAN，再由WAN转发到家庭网络内网地址，网络流量还会通过相反的路径回流。这就是通常提到的**NAT回流**（NAT Loopback）。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/homeredirect_scenario.png)

### 配置方式

在“服务”中找到“端口转发”，打开HomeRedirect端口转发工具。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/homeredirect_1.jpg)

“总开关”用于控制端口转发是否生效，“总开关”处于勾选状态，且“转发设置”中的某条规则“已启用”为勾选状态，某条转发规则才会生效。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/homeredirect_2.jpg)

如上图，勾选开启两条规则，点击右下角“保存&应用”，即可生效。状态列会列出此条规则当前状态。

路由器的端口，是**独占**的。图中开启了两条从路由器60609端口到其他目的地的转发，只有一条可以运行。

### 注意事项

#### 关于防火墙规则

HomeRedirect转发规则生效时，会自动打开防火墙相应端口（“网络”-“防火墙”-“通信规则”中查看）。端口规则以“HR”开头。请不要修改这些规则。当转发关闭时，相应规则会自动取消。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/homeredirect_3.jpg)

#### 与防火墙自带端口转发的关系

系统防火墙自带端口转发功能，但在某些场景下运作并不正常（如无法完成NAT回环）。

使用HomeRedirect后，请不要在防火墙-端口转发中建立同端口规则。防火墙规则优先级较高，一旦配置，HomeRedirect相应端口转发将失效（如果HomeRedirect中也有60607端口转发规则，如下图配置，将使得HomeRedirect转发失效）。

![homeredirect_4](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/homeredirect_4.jpg)