# 加密 DNS
如果配置了加密 DNS，传统 DNS 将仅用作解析加密 DNS 域名和测试网络连通性。

支持的协议：

- DNS over HTTPS: https://example.com
- DNS over HTTP/3: h3://example.com
- DNS over QUIC: quic://example.com

### 为所有域名使用加密 DNS

```
[General]
encrypted-dns-server = https://8.8.8.8/dns-query
```

你可以在这里指定多个加密 DNS 服务器，多个服务器之间使用逗号分隔。


### 为特定域名使用加密 DNS

```
[Host]
example.com = server:https://cloudflare-dns.com/dns-query
```
### 与代理配合使用 DoH

如果你想通过代理查询DoH服务器，你可以把 `doh-follow-outbound-mode` 设置为true。

```
[General]
encrypted-dns-follow-outbound-mode=true
```

所有的加密 DNS 连接将遵循出站模式的设置。然后为 DoH 主机名配置一个规则来使用代理。

或者，使用 `PROTOCOL,DOH`, `PROTOCOL,DOH3` 或 `PROTOCOL,DOQ` 规则来匹配所有加密 DNS 连接。






