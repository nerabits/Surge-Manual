# Proxy Policy

A proxy policy indicates forwarding the request to another proxy server. Surge supports HTTP/HTTPS/SOCKS5/SOCKS5-TLS proxy protocols.

Section [Proxy] declares proxy policies. You can create multiple proxies for different rules.

The configuration lines example:

```
[Proxy]
ProxyHTTP = http, 1.2.3.4, 443, username, password
ProxyHTTPS = https, 1.2.3.4, 443, username, password
ProxySOCKS5 = socks5, 1.2.3.4, 443, username, password
ProxySOCKS5TLS = socks5-tls, 1.2.3.4, 443, username, password, skip-common-name-verify=true
```

## Proxy Type

Surge supports the most common standard proxy protocols.

* HTTP Proxy: `ProxyHTTP = http, 1.2.3.4, 443, username, password`
* HTTPS Proxy (HTTP Proxy via TLS): `ProxyHTTPS = https, 1.2.3.4, 443, username, password`
* SOCKS5: `ProxySOCKS5 = socks5, 1.2.3.4, 443, username, password`
* SOCKS5 via TLS: `ProxySOCKS5TLS = socks5-tls, 1.2.3.4, 443, username, password`

Surge also supports several non-standard proxy protocols.

* Snell: `Proxy-Snell = snell, 1.2.3.4, 8000, psk=password, version=4`
* Shadowsocks: `Proxy-SS = ss, 1.2.3.4, 8000, encrypt-method=chacha20-ietf-poly1305, password=abcd1234`
* VMess: `Proxy-VMess = vmess, 1.2.3.4, 8000, username=0233d11c-15a4-47d3-ade3-48ffca0ce119`
* Trojan: `Proxy-Trojan = trojan, 192.168.20.6, 443, password=password1`
* TUIC: `Proxy-TUIC = tuic, 192.168.20.6, 443, token=pwd, alpn=h3`

Surge supports UDP relay of Snell V3/V4, Shadowsocks, Trojan, WireGuard, and TUIC protocols. The UDP relay support for shadowsocks proxies should be turned on manually by adding the parameter `udp-relay=true` since the shadowsocks server may not support the UDP relay.

## Parameters

#### Parameters for all proxy types

All parameters in [Common Policy Parameters](parameters.md) are also available for proxy policies.

* `no-error-alert`

Do not show error alerts for this policy.

* `underlying-proxy`

Use a proxy to connect another proxy, aka proxy chain.

* `test-udp`

Example:
`test-udp=google.com@1.1.1.1`

Override the global `proxy-test-udp` settings for the proxy. Surge test and benchmark the UDP relay by performing a DNS lookup.


#### Parameter for proxy via TLS (HTTP, SOCKS5-TLS, VMess, Trojan, TUIC)

* `skip-cert-verify`: Optional, "true" or "false" (Default: false).
  
	If this option is enabled, Surge will not verify the server's certificate.

* `sni`: The default value is the proxy hostname

	You may customize the Server Name Indication (SNI) during the TLS handshake. Use sni=off to turn off SNI completely. By default, Surge sends the SNI using the hostname like most browsers.
	
#### Parameter for HTTP/HTTPS protocol

* `always-use-connect`: Optional.

Always use the HTTP CONNECT method to relay, even for plain HTTP requests.


#### Parameter for protocols that support obfuscating (Shadowsocks, Snell)

* `obfs`: Optional. `http` or tls`
* `obfs-host`: Optional.
* `obfs-uri`: Optional.

#### Parameter for Snell protocol

See [Snell Protocol](../others/snell.md) for more information.

* `psk`: Required.
* `version`: Required.
* `reuse`: Optional. Connection reuse is an optional feature for Snell V4.

#### Parameter for Shadowsocks protocol

* `udp-relay`: Optional. Since the UDP relay is optional for the shadowsocks server, you must enable the UDP relay explicitly.

#### Parameter for VMess protocol

* `ws`: Optional. Use the Web Socket transport layer.
* `ws-path`: Optional.
* `ws-headers`: Optional.
* `encrypt-method`: Optional.

#### Parameter for Trojan protocol

* `ws`: Optional. Use the Web Socket transport layer.
* `ws-path`: Optional.
* `ws-headers`: Optional.

#### Parameter for TUIC {{book.NEW}}

* `token`: Required.
* `alpn`: Optional. It must match the server's ALPN setting.


## Client Certificate for TLS Proxy

Surge supports client certificate verification for TLS-based proxies.

Example: 

```
[Proxy]
Proxy = https, example.com, 443, client-cert=cert1

[Keystore]
cert1 = base64=<P12 base64 string here>, password=123456
```

## Shadow TLS {{book.BETA}}

Shadow TLS is a proxy obfuscator and can be used with any TCP-based proxy. (https://github.com/ihciah/shadow-tls)

Starting from Surge iOS 5.2.0 & Surge Mac 4.10.0, Surge supports Shadow TLS V2 protocol. Append `shadow-tls-password` to any proxy declaration to utilize it.

Example: 

```
[Proxy]
STLS-SNELL = snell, 1.2.3.4, 443, psk=pwd1, version=4, reuse=true, shadow-tls-password=pwd2
```

#### Parameters

* `shadow-tls-password`: Required. It must match the server's setting.
* `shadow-tls-sni`: Optional. The SNI will be sent to the server during the TLS handshake in plain. If not set, no SNI will be sent.


