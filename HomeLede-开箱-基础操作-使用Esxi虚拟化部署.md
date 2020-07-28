**本文介绍使用VMware虚拟化平台部署HomeLede，并扩容固件硬盘的方法。**

推荐使用虚拟化方式部署软路由，理由如下：
+ 部署、升级、回退、扩容等操作非常方便，特别适合折腾
+ 可以方便的调整网络结构（个人不建议直通，直通可能会带来的一点性能优势，但丧失了灵活性）

本文使用的软件情况：
+ VMware Esxi 7.0
+ VMware Workstation 15.5 pro
+ Windows 10
+ HomeLede

开始前，请确认：
+ 虚拟化平台工作正常
+ Internet线路正常
+ 获取了HomeLede固件

**操作步骤：**
+ 使用VMware Workstation在本地创建虚拟机，部署HomeLede（并完成配置，本文中略）
+ 上传至Esxi启动

**这样操作的优势：**
+ 相比于使用Esxi的基于Web浏览器的管理界面，WMware Workstation是Windows本地应用，不仅操作体验方便，还可以进行可以一些Esxi无法完成的操作（比如编辑虚拟磁盘）。
+ 无需转换固件vmdk格式，VMware Workstation会自动处理
+ 本地测试路由运行没问题后再上传到Esxi，相比于直接在Esxi上操作安全很多

### 操作详述

***

#### 1 创建虚拟机

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-1.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-2.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-3.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-4.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-5.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-6.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-7.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-8.jpg)

***

#### 2 选择HomeLede的ESXI格式固件作为虚拟机硬盘。（建议提前创建好虚拟机保存位置，将HomeLede固件拷贝进去）

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-9.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-10.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-11.jpg)

**注意：这里会提示转换虚拟磁盘格式，选择“转换”即可。**

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-12.jpg)

在向导最后一页，打开“自定义硬件”，为虚拟机添加第二块网卡（默认会添加一块，对应于HomeLede内部的eth0，也就是LAN，再增加一块，对应于eth1，也就是WAN）。
为了测试方便：
+ 这里第一块网卡选择了“仅主机模式”，默认对应于VMware Workstation在系统中创建的VMNet1。用于模拟HomeLede的LAN。
+ 第二块网卡选择“桥接”模式，相当于使这台虚拟机直接连入家庭网络。用于模拟HomeLede的WAN（可以直接利用家庭网络上网）。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/10-createVM-13.jpg)

***

#### 3 扩充硬盘
点击“编辑虚拟机”设置。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/20-editvmconfig.jpg)

选择“硬盘”，点击“扩展”，在弹出框内输入容量，最后点击“扩展”。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/30-extenddiskcapacity.jpg)

#### 4 启动HomeLede虚拟机，进行磁盘分区及格式化
点击“开启此虚拟机”，等待HomeLede引导完毕。

在命令行界面，执行硬盘分区操作。
固件默认磁盘（Linux下第一块磁盘标记为/dev/sda）有两个分区，刚才执行了扩充操作，在现有两个分区后面扩展了60G容量，现在要把这新扩充的部分做成一个新的分区。
执行命令`fdisk /dev/sda`，表示开始对第一块硬盘进行分区。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/50-fdisk.jpg)

依次输入：
+ `n` （表示新建分区）`回车`
+ `p` （创建一个新的主分区）`回车`
+ `3` （创建第三分区，固件内置分区分别为/dev/sda1、/dev/sda2，现在要将扩充的容量创建为第三分区，也就是/dev/sda3）`回车`
+ `w` （将新创建的分区写入磁盘分区表）`回车`

接下来，对新创建的分区进行格式化。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/51-mkfs.jpg)

输入`mkfs.ext4 /dev/sda3`，将新创建的分区格式化为ext4格式。

最后，重启路由。

重启后可以进行一些在本地的换固件的准备工作。
+ 比如临时修改固件WAN的IP（如果默认IP和你家庭网络路由冲突的话），打开图形界面完成一些配置。
+ 上传一些备份的配置文件（dhcp、ddns、firewall、psw等等）
+ 测试固件中分流软件是否运作正常
+ 将安装软件路径、docker，某些需要记录日志的路径指向新增加的大容量分区。
+ 全部完成后，如果临时修改过路由ip，记得改回来
+ 关闭虚拟机

#### 5 上传至ESXI

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/70-connesxi.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/71-uploadvm.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/72-selectesxiserver.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/73-confirmesxiserver.jpg)
![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/esxi/81-configesxinet.jpg)
