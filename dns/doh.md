# DNS over HTTPS
如果配置了 DNS-over-HTTPS，传统 DNS 将仅用作解析 DoH 域名和测试网络连通性。

### 为所有域名使用 DoH

```
[General]
doh-server = https://9.9.9.9/dns-query
```

您可以在这里指定多个 DNS-over-HTTPS 服务器（不推荐）。


### 为特定域名使用 DoH

```
[Host]
example.com = server:https://cloudflare-dns.com/dns-query
```


### DNS over HTTPS 格式

有两种不同的 DoH 格式：JSON 和 DNS wireformat (RFC1035).

您需要确定您的 DoH 服务支持的格式。

* Surge iOS 4.1 及以下版本 / Surge Mac 3.4.1 及以下版本：仅支持 JSON 格式。

* Surge iOS 4.2 及以上版本 / and Surge Mac 3.5.0 及以上版本：Surge 使用 DNS wireformat 作为默认。 您仍可以继续选择使用 JSON。

	```
	[General]
	doh-format=json
	```

### 与代理配合使用 DoH

如果你想通过代理查询DoH服务器，你可以把 `doh-follow-outbound-mode` 设置为true。

```
[General]
doh-follow-outbound-mode=true
```

所有的 DoH 连接将遵循出站模式的设置。然后为 DoH 主机名配置一个规则来使用代理。

或者，使用 `PROTOCOL,DOH` 规则来匹配所有 DoH 连接。






