# Misc Options

```
[General]
ipv6 = false
loglevel = notify

skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local

tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12
tun-included-routes = 192.168.1.12/32
```

### Common Options

#### Enable full IPv6 support (Default: false)

`ipv6 = false`

#### loglevel (Default: notify)

`loglevel = notify`

One of verbose, info, notify or warning. It's not recommended to enable verbose in daily use because this will slow down the performance significantly.

#### skip-proxy

`skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local`

In iOS version, this option forces connections to these domain/IP ranges to be handled by Surge TUN, instead of Surge proxy. In macOS version, these settings will be applied to system when "Set as System Proxy" is enabled. This option is used to fix compatibility problems with some apps.

* To specify a single domain, enter the domain name - for example, apple.com.
* To specify all websites on a domain, use an asterisk before the domain name - for example, *apple.com.
* To specify a specific part of a domain, specify each part - for example, store.apple.com.
* To specify hosts or networks by IP addresses, enter a specific IP address such as 192.168.2.11 or an address range, such as 192.168.2.* or 192.168.2.0/24.

> Notice: If you enter an IP address or address range, you will only be able to bypass the proxy when you connect to that host using that address, not when you connect to the host by a domain name that resolves to that address.


#### Misc

```
use-default-policy-if-wifi-not-primary = false
```

#### Helper

```
proxy-settings-interface = Wi-Fi
```

#### Excluded Routes

`tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12`

Surge VIF can only process TCP and UDP protocols. Use this option to bypass specific IP ranges to allow all traffic to pass through.

> Notice: This option only works for Surge VIF. Requests handled by Surge Proxy Server will not be affected. Combine 'skip-proxy' and 'tun-excluded-routes' to make sure that certain HTTP traffic bypasses Surge.
> 
> This option might cause a system error ENOMEM (Cannot allocate memory). It seems a bug in iOS system. Please do noy use this option if possible.

#### Included Routes

`tun-included-routes = 192.168.1.12/32`

By default, Surge VIF interface will declare itself as the default route. But since the Wi-Fi interface has a smaller route. Some traffic may not go through Surge VIF interface. Use this option to add a smaller route.