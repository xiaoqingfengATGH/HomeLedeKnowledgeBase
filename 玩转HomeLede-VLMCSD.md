![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/vlmcsd.png)

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/vlmcsd_luci.png)

使用前提：

+ Windows、Office使用VOL版本（绝大部分默认都是，如果不是，Windows可以通过安装KMS密钥实现转换，Office需要使用版本转换脚本，请自行查找）

+ 激活服务器指向路由

KMS密钥可以去微软站点找：

+ windows

  https://docs.microsoft.com/en-us/windows-server/get-started/kmsclientkeys

+ office

  https://docs.microsoft.com/zh-cn/DeployOffice/vlactivation/gvlks

### Windows

以Win10为例（下面例子中`192.168.1.1`是路由地址，如果已经更改请按实际情况调整）：

以管理员身份运行cmd，依次输入如下指令：

```shell
slmgr.vbs /upk
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms 192.168.1.1
slmgr /ato
```

WinServer2016：

```shell
slmgr /upk
slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
slmgr.vbs /skms 192.168.1.1
slmgr.vbs /ato
```

参考效果：

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/vlmcsd_win10.png)

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/immerse/vlmcsd_win10_2.png)

### Office

1.以管理员身份运行cmd，进入Office OSPP.VBS目录

打开命令提示符(管理员)执行以下命令进入OSPP.VBS目录(若Office安装在其他盘符和路径，请自行修改命令)。

Office2016、Office2019、Office365 默认安装目录 64位系统为例：
32位版本：
`cd C:\Program Files (x86)\Microsoft Office\Office16`
64位版本：
`cd C:\Program Files\Microsoft Office\Office16`

Office2013 默认安装目录 64位系统为例：
32位版本：
`cd C:\Program Files (x86)\Microsoft Office\Office15`
64位版本：
`cd C:\Program Files\Microsoft Office\Office15`

Office2010 默认安装目录 64位系统为例：
32位版本：
`cd C:\Program Files (x86)\Microsoft Office\Office14`
64位版本：
`cd C:\Program Files\Microsoft Office\Office14`

总之就是在CMD命令提示符(管理员)内 使用cd命令进入 OSPP.VBS 文件所在的目录。
如果不确定自己安装的Office是32位还是64位，就两行命令都执行一下 不报错的就是对的。

2.执行命令激活Office软件

完成上一步骤后，执行以下命令（下面例子中`192.168.1.1`是路由地址，如果已经更改请按实际情况调整）。

`cscript ospp.vbs /sethst:192.168.1.1 && cscript ospp.vbs /act`