# 规则集

从 Surge Mac v3.0 和 Surge iOS v3.4 开始，您可以使用来自文件或URL的规则集。Surge 还提供两个内置规则集。

## 内置规则集

内置规则集的内容可能随着 Surge 版本的更新而改变。请到规则集设置中查看最新的子规则。

### SYSTEM

`RULE-SET,SYSTEM,DIRECT`

包含由 macOS 和 iOS 本身发送的大多数请求的规则。不包括由 App Store、iTunes 和其他内容服务发送的请求。

```
USER-AGENT,*com.apple.mobileme.fmip1
USER-AGENT,*WeatherFoundation*
USER-AGENT,%E5%9C%B0%E5%9B%BE*
USER-AGENT,%E8%AE%BE%E7%BD%AE*
USER-AGENT,com.apple.geod*
USER-AGENT,com.apple.Maps
USER-AGENT,FindMyFriends*
USER-AGENT,FindMyiPhone*
USER-AGENT,FMDClient*
USER-AGENT,FMFD*
USER-AGENT,fmflocatord*
USER-AGENT,geod*
USER-AGENT,locationd*
USER-AGENT,Maps*
DOMAIN,api.smoot.apple.com
DOMAIN,captive.apple.com
DOMAIN,configuration.apple.com
DOMAIN,guzzoni.apple.com
DOMAIN,smp-device-content.apple.com
DOMAIN,xp.apple.com
DOMAIN-SUFFIX,ess.apple.com
DOMAIN-SUFFIX,push-apple.com.akadns.net
DOMAIN-SUFFIX,push.apple.com
DOMAIN,aod.itunes.apple.com
DOMAIN,mesu.apple.com
DOMAIN,api.smoot.apple.cn
DOMAIN,gs-loc.apple.com
DOMAIN,mvod.itunes.apple.com
DOMAIN,streamingaudio.itunes.apple.com
DOMAIN-SUFFIX,lcdn-locator.apple.com
DOMAIN-SUFFIX,lcdn-registration.apple.com
DOMAIN-SUFFIX,ls.apple.com
PROCESS-NAME,trustd
```

> 这些规则可能会随着 Surge 的更新而改变。请参考 App 中的描述，以获得最新的子规则。

### LAN

`RULE-SET,LAN,DIRECT`

包括 LAN IP 地址和 .local 后缀的规则。请注意这个规则集将触发 DNS 查询。

```
DOMAIN-SUFFIX,local
IP-CIDR,192.168.0.0/16
IP-CIDR,10.0.0.0/8
IP-CIDR,172.16.0.0/12
IP-CIDR,127.0.0.0/8
IP-CIDR,100.64.0.0/10
IP-CIDR6,fe80::/10
```


## 外部规则集

从 URL 或本地文件中获取规则集。规则集文件应该是一个文本文件，每一行都包含一个规则声明，没有策略。

示例：

```
DOMAIN,exampleA.com
DOMAIN,exampleB.com
```

