Clash不同运行模式下内置DNS的行为：
+ FakeIP
  + 命中代理规则（需要代理）的流量，DNS由远程主机解析（机场或者VPS主机）。
  + DNS配置的nameserver、fallback仅用于解析远程主机的域名。
+ Redir-Host
  + DNS配置的nameserver、fallback用于流量DNS解析，nameserver与fallback并行解析，当返回结果中有国外IP时，仅信任fallback的结果（类似chinadns的按IP所属区域分流解析）。
  + 此模式下，nameserver相当于chinadns的国内dns，fallback相当于可信dns。