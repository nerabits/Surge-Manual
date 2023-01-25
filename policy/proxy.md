# 代理策略

代理策略表示将请求转发到其他代理服务器。Surge 支持 HTTP/HTTPS/SOCKS5/SOCKS5-TLS/Vmess/Trojan/Shadowsocks 代理协议。

配置段 [Proxy] 用于声明代理策略。你可以为不同规则创建多个代理策略。

配置行示例：

```
[Proxy]
ProxyHTTP = http, 1.2.3.4, 443, username, password
ProxyHTTPS = https, 1.2.3.4, 443, username, password
ProxySOCKS5 = socks5, 1.2.3.4, 443, username, password
ProxySOCKS5TLS = socks5-tls, 1.2.3.4, 443, username, password, skip-common-name-verify=true
```

## 代理类型

Surge 支持最常见的标准代理协议。

* HTTP Proxy: `ProxyHTTP = http, 1.2.3.4, 443, username, password`
* HTTPS Proxy (HTTP Proxy via TLS): `ProxyHTTPS = https, 1.2.3.4, 443, username, password`
* SOCKS5: `ProxySOCKS5 = socks5, 1.2.3.4, 443, username, password`
* SOCKS5 via TLS: `ProxySOCKS5TLS = socks5-tls, 1.2.3.4, 443, username, password`

Surge 也支持多种非标准代理协议。

* Snell: `Proxy-Snell = snell, 1.2.3.4, 8000, psk=password, version=4`
* Shadowsocks: `Proxy-SS = ss, 1.2.3.4, 8000, encrypt-method=chacha20-ietf-poly1305, password=abcd1234`
* VMess: `Proxy-VMess = vmess, 1.2.3.4, 8000, username=0233d11c-15a4-47d3-ade3-48ffca0ce119`
* Trojan: `Proxy-Trojan = trojan, 192.168.20.6, 443, password=password1`
* TUIC: `Proxy-TUIC = tuic, 192.168.20.6, 443, token=pwd, alpn=h3`

Surge 支持 Snell V3/V4、Shadowsocks 和 Trojan 协议的 UDP 转发。由于 shadowsocks 服务器可能不支持 UDP 转发，所以 shadowsocks 代理的 UDP 转发支持应该通过添加参数 `udp-relay=true` 来手动开启。

## 参数

#### 全部代理策略均支持的参数

[通用策略参数](parameters.md)中的所有参数也可用于代理策略。

* `no-error-alert`

不显示该策略的错误警告。

* `underlying-proxy`

使用一个代理来连接另一个代理，又称代理链。

* `test-udp`

示例：
`test-udp=google.com@1.1.1.1`

覆盖全局的 `proxy-test-udp`  设置。Surge 通过进行 DNS 请求，对 UDP 代理进行可用性和基准测试。


#### 基于 TLS 的代理协议的参数（HTTP, SOCKS5-TLS, VMess, Trojan, TUIC）

* `skip-cert-verify`：可选，可选值："true" 或 "false" （默认：false）
  
	如果该选项被启用，Surge 将不会验证服务器的证书。

* `sni`： 默认为代理服务器的主机名

	你可以在 TLS 握手期间自定义服务器名称指示（SNI）。使用 sni=off 来完全关闭 SNI。默认情况下，Surge 会像大多数浏览器一样使用主机名来发送 SNI。
	
#### HTTP/HTTPS 协议特有的参数

* `always-use-connect`：可选。

始终使用 HTTP CONNECT 方法进行转发，即使是纯 HTTP 请求。


#### 支持混淆的代理协议的参数（Shadowsocks, Snell）

* `obfs`：可选，参数：`http` 或 `tls`。
* `obfs-host`：可选。
* `obfs-uri`：可选。

#### Snell 协议的参数

查看 [Snell 协议](../others/snell.md) 获取更多信息。

* `psk`：必选。
* `version`：必选。
* `reuse`：可选，连接重用是 Snell V4 的可选特性。

#### Shadowsocks 协议的参数

* `udp-relay`：可选，因为 UDP 中继对于 Shadowsocks 服务器来说是可选的，你必须手动开启 UDP 中继。

#### VMess 协议的参数

* `ws`：可选，使用 Web Socket 传输层。
* `ws-path`：可选。
* `ws-headers`：可选。
* `encrypt-method`：可选。

#### TUIC 协议的参数  {{book.BETA}}

* `token`: 必选。
* `alpn`: 可选，必须和服务端的 ALPN 设置相同。

#### Trojan 协议的参数

* `ws`：可选，使用 Web Socket 传输层。
* `ws-path`：可选。
* `ws-headers`：可选。


## TLS 代理的客户端证书

Surge 支持对基于 TLS 的代理进行客户端证书验证。

示例：

```
[Proxy]
Proxy = https, example.com, 443, client-cert=cert1

[Keystore]
cert1 = base64=<P12 base64 string here>, password=123456
```

## Shadow TLS  {{book.BETA}}

Shadow TLS 是一个可用于任何基于 TCP 代理的代理混淆工具。(https://github.com/ihciah/shadow-tls)

自 Surge iOS 5.2.0 & Surge Mac 4.10.0 开始，Surge 支持 Shadow TLS V2 协议。你可以在任何代理配置中添加 `shadow-tls-password` 参数来使用它。

示例：

```
[Proxy]
STLS-SNELL = snell, 1.2.3.4, 443, psk=pwd1, version=4, reuse=true, shadow-tls-password=pwd2
```

#### 参数

* `shadow-tls-password`: 必选，必须和服务端的设置相同。
* `shadow-tls-sni`: 可选，SNI 将在 TLS 握手过程中以明文形式发送到服务器。如果不设置，将不发送SNI。