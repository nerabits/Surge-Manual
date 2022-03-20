# 规则

Surge 可以依据自定义规则，转发请求到其他代理服务器或直接发送给目标主机。

### 优先级
Surge 按照配置文件中的顺序，从头到尾匹配规则。换句话说，第一条规则的优先级高于后面的规则。

### 组成

每条规则包含三个部分：规则类型、匹配的请求（FINAL 规则除外），和对应的策略：
         类型,          匹配的请求,     对应的策略
示例：    DOMAIN-SUFFIX,apple.com,     DIRECT
         IP-CIDR,      192.168.0.0/16,ProxyA

Surge 支持 6 种不同类型的规则。DOMAIN、DOMAIN-SUFFIX、DOMAIN-KEYWORD、GEOIP、IP-CIDR 和 FINAL。对于对应的策略，可以是代理服务器配置、策略组配置、"DIRECT" 或 "REJECT"。规则必须以 FINAL 规则结束，以定义默认行为。

示例：

```
[Rule]
DOMAIN-SUFFIX,company.com,ProxyA
DOMAIN-KEYWORD,google,DIRECT
GEOIP,US,DIRECT
IP-CIDR,192.168.0.0/16,DIRECT
FINAL,ProxyB
```

DOMAIN, DOMAIN-SUFFIX 和 DOMAIN-KEYWORD 是 [域名规则](/rule/domain-based.md)。 IP-CIDR 和 GEOIP 是 [IP 规则](/rule/ip-based.md)。

