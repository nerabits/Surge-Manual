# Common Policy Parameters

### Egress Parameters

All of these parameters are available for both built-in and proxy policies.

#### interface (macOS only, Default: automatically)

Force to use a specified outgoing network interface.

```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2
```

Direct policy alias supports 'interface' parameter like a proxy policy.

```
[Proxy]
Crop-VPN = direct, interface = utun0
WiFi = direct, interface = en2, allow-other-interface=true
```

Please make sure the interface has a valid route table for the destination address.

#### allow-other-interface (macOS only)

When the option is true, if the desired interface is not available, Surge is allowed to use the default interface to bind the connection. Otherwise, the connection fails directly.

```
ProxyHTTP = http, 1.2.3.4, 443, username, password, interface = en2, allow-other-interface=true
```

#### ip-version

Choose the behavior between IPv4 and IPv6 protocol.

- dual (Default, use the faster link)
- v4-only
- v6-only
- prefer-v4
- prefer-v6

#### hybrid (Boolean, iOS Only, Default: off)

Setup the connection with cellular data and Wi-Fi simultaneously, then use the faster link.

#### tfo (Boolean, Default: off)

Enable TCP Fast Open.

#### mptcp (Boolean, iOS Only, Default: off)

Enable MultiPath TCP. (Requires Network.framework enabled)

#### tos (Decimal or Hexadecimal, Default: 0)

Customize the IP TOS value.


#### test-url

Override the global testing URL. The URL is used for availability and latency testing.


