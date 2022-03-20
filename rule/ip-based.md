# IP 规则

IP 规则有三种类型。如果请求的主机名是一个域名，基于 IP 的规则将触发 DNS 查询。如果 DNS 查询失败，Surge 将中止规则测试，并报告一个错误。

#### IP-CIDR

```
IP-CIDR,192.168.0.0/16,DIRECT
IP-CIDR,10.0.0.0/8,DIRECT
IP-CIDR,172.16.0.0/12,DIRECT
IP-CIDR,127.0.0.1/8,DIRECT
```

如果请求的 IP 地址与指定地址范围相匹配，则规则匹配。

#### IP-CIDR6

```
IP-CIDR6,2001:db8:abcd:8000::/50,DIRECT
```

如果请求的 IPv6 地址与指定地址范围相匹配，则规则匹配。


#### GEOIP

`GEOIP,US,DIRECT`

如果 GeoIP 的测试结果与指定的国家代码相匹配，则规则匹配。

### IP 规则选项
#### 选项：no-resolve

```
GEOIP,US,DIRECT,no-resolve
IP-CIDR,172.16.0.0/12,DIRECT,no-resolve
```

当某个请求触发 GEOIP 或 IP-CIDR 规则时，Surge 将发送一个 DNS 查询，以检查请求的主机名是否为域名。对于有域名的请求，你可以选择 'no-resolve' 选项，以跳过这个规则。

> 注意：如果本地 DNS 服务器无法解析某些域名，请确保在该规则前没有基于 IP 的规则与该域名匹配。否则，会因为 DNS 解析错误，而规则测试失败。你也可以使用 "no-resolve" 来解决这个问题。
