# Proxy Policy

A proxy policy indicates forwarding the request to another proxy server. Surge supports HTTP/HTTPS/SOCKS5/SOCKS5-TLS proxy protocols.

Section [Proxy] declares proxy policies. You can create multiple proxies for different rules.

Example:

```
[Proxy]
ProxyHTTP = http, 1.2.3.4, 443, username, password
ProxyHTTPS = https, 1.2.3.4, 443, username, password
ProxySOCKS5 = socks5, 1.2.3.4, 443, username, password
ProxySOCKS5TLS = socks5-tls, 1.2.3.4, 443, username, password, skip-common-name-verify=true
```


## Parameters

### Parameter for all proxy type

#### interface: Optional (Default: null).
Force to use a specified outgoing network interface (available in macOS only). Please make sure the interface has a valid route table for the destination address.
 
```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2
```

#### allow-other-interface: Optional (Default: false).

```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2, allow-other-interface=true
```

When the option is ture, if the desired interface is not available, Surge is allowed to use the default interface to setup the connection. Otherwise the connection fails directly.

### Parameter for proxy with TLS (https and socks5-tls)
#### skip-cert-verify: Optional, "true" or "false" (Default: false).
If this option is enabled, Surge will not verify the server's certificate.

#### sni (Default: hostname)
You may customize Server Name Indication (SNI) during TLS handshake. Use sni=off to turn off SNI completely. By defualt Surge will send SNI with hostname like most browsers.