# Misc Options in [General] section

```
[General]
ipv6 = false
loglevel = notify

skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local

tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12
tun-included-routes = 192.168.1.12/32
```

### ipv6

Enable full IPv6 support (Default: false)

`ipv6 = false`

### loglevel (Default: notify)

`loglevel = notify`

One of verbose, info, notify or warning. It's not recommended to enable verbose in daily use because this will slow down the performance significantly.

### skip-proxy

`skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local`

In the iOS version, this option forces connection to these domain/IP ranges to be handled by Surge TUN, instead of Surge proxy. In the macOS version, these settings will be applied to the system when "Set as System Proxy" is enabled. This option is used to fix compatibility problems with some apps.

* To specify a single domain, enter the domain name - for example, apple.com.
* To specify all websites on a domain, use an asterisk before the domain name - for example, *apple.com.
* To specify a specific part of a domain, specify each part - for example, store.apple.com.
* To specify hosts or networks by IP addresses, enter a specific IP address such as 192.168.2.11 or an address range, such as 192.168.2.* or 192.168.2.0/24.

> Notice: If you enter an IP address or address range, you will only be able to bypass the proxy when you connect to that host using that address, not when you connect to the host by a domain name that resolves to that address.


### use-default-policy-if-wifi-not-primary

Use the default policy if Wi-Fi isn't primary interface for SSID Group. (macOS only)

```
use-default-policy-if-wifi-not-primary = false
```

### proxy-settings-interface

Helper proxy interface setting.

```
proxy-settings-interface = Wi-Fi
```

### always-real-ip

```
always-real-ip = *.apple.com
```

This option will ask Surge to return a real IP address instead of a fake IP address when Surge VIF handles a DNS question.

Surge will forward the DNS packet to upstream DNS servers.

### hijack-dns

`hijack-dns = 8.8.8.8:53`

By default, Surge only returns fake IP addresses for DNS queries sent to Surge DNS address (198.18.0.2). Queries that are sent to standard DNS will be  forwarded.

Some devices or software always use a hardcoded DNS server. (For example, Google Speakers always use 8.8.8.8). You may use this option to hijack the query to get a fake address.

You may use `hijack-dns = *:53` to hijack all DNS queries.

### force-http-engine-hosts

`force-http-engine-hosts = example.com:80`

Make Surge treat TCP connections as HTTP requests. HTTP engine will process the requests and all advanced features may be available, such as capturing, rewrite and scripting.

### tun-excluded-routes

`tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12`

Surge VIF can only process TCP and UDP protocols. Use this option to bypass specific IP ranges to allow all traffic to pass through.

> Notice: This option only works for Surge VIF. Requests handled by Surge Proxy Server will not be affected. Combine 'skip-proxy' and 'tun-excluded-routes' to make sure that specific HTTP traffic bypasses Surge.
> 
> This option might cause a system error ENOMEM (Cannot allocate memory). It seems a bug in the iOS system. Please do not use this option if possible.

### tun-included-routes

`tun-included-routes = 192.168.1.12/32`

By default, Surge VIF interface will declare itself as the default route. But since the Wi-Fi interface has a smaller route. Some traffic may not go through Surge VIF interface. Use this option to add a smaller route.

