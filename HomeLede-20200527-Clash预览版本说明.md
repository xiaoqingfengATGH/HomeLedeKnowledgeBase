本版本中，将Passwall替换为了Clash，并基于OpenClash定制了图形化界面HomeClash。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/1.jpg)
HomeClash提供了全新的分流规则HomeClash规则集，包含两类13组规则。
规则简介请见：https://github.com/xiaoqingfengATGH/homeclash/wiki/HomeClash%E8%A7%84%E5%88%99%E4%BB%8B%E7%BB%8D

**快速开启Clash步骤：**

*进行下列步骤前，请确认已经设置好路由WAN（拨号或者静态IP）在局域网内电脑确认可以正常访问网络（比如百度）。*

1. 左侧菜单VPN -> HomeClash，点击顶部“服务器与策略组管理”标签页。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/2.jpg)
找到页面下方“服务器节点配置”，点击“添加”。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/3.jpg)
2. 在弹出的“编辑服务器配置”页面，填入服务器信息。注意：第一项“配置文件”，保留“添加到所有配置文件”，最后一项目“添加到策略组（请勿重复添加）”留空。点击左下角“保存配置”，返回“服务器与策略组管理”标签页。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/4.jpg)
刚添加的服务器会出现在“服务器节点配置”列表中，“服务器延迟”列会显示各个服务器ping延迟数据。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/5.jpg)
3. 找到页面最上方（仍旧是“服务器与策略组管理”标签页），“一键生成配置文件”选择“启用”，“选择配置文件模板”选择“HomeClash规则”。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/6.jpg)
找到页面最下方，点击最右侧“应用配置”按钮。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/7.jpg)
4. 此时会回到HomeClash首页（“运行状态”标签页），间隔15-20秒，可以看到“OpenClash主程序”，“OpenClash守护程序”都变成“运行中”。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/8.jpg)
向下拉页面，页面最下方会显示 IP地址，网站访问检查，可以看到国内，国外检测的地址，以及国内外网站访问情况。正常情况会看到全部网站显示“连接正常”。
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/FastClash/9.jpg)

至此，全部完成。Have Fun！

**等等。。。。。我就是喜欢PassWall，就想用Passwall怎么办？**

1. 确认关闭Clash，在 左侧菜单VPN -> HomeClash，找到页面最下方“关闭OpenClash”按钮，点击。确认页面上方“OpenClash主程序”，“OpenClash守护程序”等等都处于停止状态。

2. 在浏览器中输入 http://192.168.1.1/cgi-bin/luci/admin/vpn/passwall/show 回车。（如果你修改过路由IP，请把192.168.1.1替换成你自己的IP）

此时你就会看到Passwall首页了。随后一切和以前一样，设置好主机，策略，DNS按照默认，OK！