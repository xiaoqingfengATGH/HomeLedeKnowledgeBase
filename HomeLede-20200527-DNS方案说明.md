固件仍旧保持之前4级DNS设计，实现去广告+分流解析+国内外速度优选，可无需配置直接使用。引入Clash后，仍可与4级DNS方案无缝集成。依旧保持去广告+分流解析+国内外速度优选的能力。关闭后，自动恢复为默认方案。
固件默认DNS方案如下:
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/DNS/1Default.png)
DNS解析示意图：
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/DNS/2DNSResolutionProcess.png)
当打开Clash时，DNS方案如下：
![](https://raw.githubusercontent.com/wiki/xiaoqingfengATGH/HomeLede/DNS/3DNSwithClash.png)