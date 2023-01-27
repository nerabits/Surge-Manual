# Final 规则

FINAL 规则必须写在全部规则之后，它定义了其他规则没有匹配的请求最终策略。 

示例：

```
[Rule]
DOMAIN-SUFFIX,company.com,ProxyA
DOMAIN-KEYWORD,google,DIRECT
GEOIP,US,DIRECT
IP-CIDR,192.168.0.0/16,DIRECT
FINAL,ProxyB
```

### 选项
#### 选项：dns-failed

如果在为某个请求匹配规则时 DNS 查询失败，则使用 FINAL 规则。此选项的前提是该请求的对应策略不是 DIRECT。