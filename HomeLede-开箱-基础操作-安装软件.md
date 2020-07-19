### 常见疑问

+ 为什么HomeLede会随版本提供软件包？

+ HomeLede基于OpenWrt软件包体系，全部利用官方软件包不好吗？



OpenWrt确实有官方软件包源，但由于OpenWrt碎片化比较严重（多种软件分支，多种设备），官方源的软件包并不一定可以适应所有版本。还有某些软件会依赖于内核模块，会严格要求内核版本，很有可能因为软件包编译时依赖的内核版本和安装环境里不一致导致无法使用或者工作不正常。

总结一句话——**随着固件编译时一同打包出来的软件，才能最大程度保证顺利安装到固件上**。在其他环境下打包出来的软件，不一定可以。

### HomeLede安装软件的方法

以安装Server酱为例，「Server酱」，英文名「ServerChan」，是一款从服务器推送报警信息和日志到微信的工具。

#### 获取安装包的名称

通过百度，或者查阅各大论坛帖子，或者交流群里询问，得知「Server酱」安装包大致是叫“serverchan”。

#### 查找软件包

HomeLede固件附带的“3 软件包列表.txt”中有所有软件包名称的列表，打开后，搜索下"`serverchan`"。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_1.jpg)

很快找到`luci-app-serverchan_1.78-8_all.ipk`，位置在xiaoqingfeng目录中。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_2.jpg)

打开固件“`软件包.zip`”，找到对应目录下的ipk安装包，解压出来。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_3.jpg)

#### 上传固件

使用固件“系统”->“文件传输”，上传刚才解压出来的文件。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_4.jpg)

成功上传的文件会显示在“上传文件列表”中，如下。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_5.jpg)

#### 安装软件

在上传文件列表中，可以直接点击右侧“安装”按钮进行安装。

**至此，一个常规的软件安装过程已经结束。**

不过，安装软件还可能出现各种各样的意外，接下来内容是以`luci-app-serverchan_1.78-8_all.ipk`为例，介绍一下出现问题怎么解决。

我们来尝试安装`luci-app-serverchan_1.78-8_all.ipk`，点击安装后，出现如下提示。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_6.jpg)

整个浏览器都变白了，弹出了报错的信息。

**不要慌**。通常弹出报错信息基本有两个可能：

+ 软件包依赖没有安装，但文件传输自带的快捷安装没有处理好，导致报错。

+ 软件包损坏

这时候重新登录路由界面（比如地址栏输入[http://192.168.1.1](http://192.168.1.1)），**刷新浏览器**。

发现ServerChan已经安装上了，菜单入口叫做“微信推送”，我们设置一部分信息。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_7.jpg)

勾选“启用”之后，点击右下角“保存&应用”，发现ServerChan没有运行。无论怎么样设置都没运行。

估计软件有问题了，怎么办？

+ 查看系统日志（图形界面“状态”->"系统日志"里查看）

+ 看软件自己日志

不巧的是ServerChan并没有留下有用的系统日志，我们查看一下软件自己的日志。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_8.jpg)

软件日志提示

```
2020-07-19 12:59:17 【！！！】依赖项未安装
2020-07-19 12:59:17 【！！！】读取设置出错，请检查设置项 
```

看来是软件依赖的包不存在啊。

我一个用户，怎么知道这个软件依赖什么啊？？？？？！！！！

莫慌，软件包在手里呢，看看有没有线索？

用7zip打开`luci-app-serverchan_1.78-8_all.ipk`，一层一层往下找（遇到名称为一个.的目录，请继续双击它打开），发现一个叫做“control.tar.gz”的，继续打开。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_9.jpg)

发现一个叫做·control·的文件，按F3打开查看。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_10.jpg)

原来软件包的依赖记录在这里，这里有三个依赖`libc, iputils-arping, curl`，其中lib开头的是库文件，缺少可能性极小，curl是一个命令，在命令行里输入以下，没有报`-ash: curl: not found`就是安装好了。

只剩下`iputils-arping`了。去软件包里再找一轮。

找到一个在`packages`文件夹下，叫做`iputils-arping_20190709-1_x86_64.ipk`的软件包。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_11.jpg)

按照之前步骤，文件传输到固件，安装。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_12.jpg)

这次很顺利，直接提示安装成功了。

再次回到ServerChan，点击”保存&应用“，发现ServerChan已经正常启动。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_13.jpg)

日志中，也提示”初始化完成“。

![](https://github.com/xiaoqingfengATGH/HomeLede/wiki/opencase/INST_IPK_14.jpg)

至此，ServerChan安装完成。

#### 小结

软件安装失败，除了软件本身问题之外（小概率），还有是因为操作错误导致的，比如架构不正确（arm软件运行在x86），内核不匹配。如果前面问题都没有，最大概率就是”依赖包缺失“。

通过官方源在线安装可以自动解决一部分依赖缺失的问题，如果官方安装失败，可以通过上面介绍的思路尝试解决。

祝大家使用愉快！