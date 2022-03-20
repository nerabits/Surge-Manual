# [General] 部分的其他选项

由于选项经常变化，你可以在应用程序中查找 [General] 部分选项的最新解释。

- Surge Mac: 主窗口 -> 帮助 -> 配置文件符号
- Surge iOS: "更多" 标签 -> 帮助 -> 配置文件符号


```
[General]
ipv6 = false
loglevel = notify
skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local
tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12
tun-included-routes = 192.168.1.12/32
```

### loglevel

日志级别。可选值包含 verbose, info, notify 和 warning。不建议在日常使用中启用 verbose 模式，因为会大大降低性能。

### ipv6

开启完整 IPv6 支持。

### dns-server

上级 DNS 服务器的 IP 地址。

### skip-proxy

在 iOS 版本中，该选项将使得发往这些域名或者 IP 段的请求由 Surge VIF 进行处理（而不是 Surge Proxy）；在 macOS 版本中，当“设置为系统代理”开启时，该选项中的设置将会被提交到系统。该选项用于修正和某些应用的兼容性问题。

  - 指定单一域名，输入域名 - 例如，apple.com。

  - 指定一个域名上的所有网站，在域名前使用星号 - 例如，\*apple.com。

  - 指定一个域的特定子域名，输入完整域名 - 例如，store.apple.com。

  - 要通过IP地址指定主机或网络，请输入一个特定的IP地址，如 192.168.2.11 或一个地址范围，如 192.168.2.* 或 192.168.2.0/24。

注意：如果你指定了 IP 地址或地址范围，你只能在使用该地址或地址范围直接连接到该主机时绕过代理；而在使用这些IP或IP段对应的域名连接时，则不能绕过代理。

### exclude-simple-hostnames

和 skip-proxy 参数类似，该选项允许使用简单的主机名（没有.）的请求由 Surge VIF 而不是 Surge Proxy 进行处理。

### external-controller-access

该选项允许外部控制器来控制 Surge，例如 Surge 请求查看器（macOS）和 Surge iOS 远程控制器（iOS）。例如：key@0.0.0.0:6165

### http-api

该选项允许使用 HTTP API 来控制 Surge。例如：key@0.0.0.0:6166

### http-api-tls

使用 HTTPS 协议替代HTTP。必须先配置 MitM CA 证书。你需要在客户端设备上手动安装该证书。

### http-api-web-dashboard

你可以在启用该功能后，使用浏览器控制 Surge。

### show-error-page-for-reject

如果请求时普通的 HTTP 请求，则为 REJECT 策略显示一个错误网页。

### tun-excluded-routes

Surge VIF 仅可处理 TCP 和 UDP 协议。使用此功能来绕过特定的 IP 范围，来允许所有流量通过。

注意。这个选项只适用于Surge VIF。由 Surge Proxy 处理的请求不受影响。你可以结合 "skip-proxy" 和 "tun-excluded-routes" 选项来确保特定的 HTTP 流量绕过 Surge。

### tun-included-routes

默认情况下，Surge VIF 将自己定义为默认路由。然而，由于 Wi-Fi 网卡有一个较小的路由，一些流量可能不会通过 Surge VIF。使用这个选项可以添加一个较小的路由。

### internet-test-url

用于测试互联网连接性的 URL，同时也用于 DIRECT 策略的网络测试。

### proxy-test-url

代理策略的默认测试 URL。

### test-timeout

连接测试的超时时间。

### always-real-ip

当 Surge VIF 处理 DNS 查询时，该选项要求 Surge 返回真实的 IP 地址，而不是 fake IP。

DNS 数据包将被转发至上游 DNS 服务器。

### hijack-dns

By default, Surge only returns fake IP addresses for DNS queries sent to Surge DNS address (198.18.0.2). Queries sent to a standard DNS will be forwarded.

Some devices or software always use a hardcoded DNS server. (For example, Google Speakers always use 8.8.8.8). You may use this option to hijack the query to get a fake address.

You may use hijack-dns = \*:53 to hijack all DNS queries.

### network-framework

Uses Network.framework to utilize userspace network stack, which can improve throughput, reduce latency and enable cutting edge features such as Multipath TCP. (Manual restart is required)

Experimental features may be unstable, and may even cause the system to become frozen.

### force-http-engine-hosts

Make Surge treat TCP connections as HTTP requests. Surge HTTP engine will process the requests, and all advanced features will be available, such as capturing, rewrite and scripting.

Wildcard characters \* and ? are supported.

  - Use prefix - to exclude a hostname.

  - By default, only the requests to port 80 are decrypted.

  - Use suffix :port to allow other ports.

  - Use suffix :0 to allow all ports.

Example:

  - -\*.apple.com: Excludes all requests sent to \*.apple.com on port 80.

  - www.google.com: Uses forced HTTP processing for www.google.com on port 80.

  - www.google.com:8080: Uses forced HTTP processing for www.google.com on port 8080.

  - www.google.com:0: Uses forced HTTP processing for www.google.com on all ports.

  - \*:0: Uses forced HTTP processing for all hostnames on all ports.

### tls-provider

Available values: secure-transport, openssl, network-framework

Choose OpenSSL or Network.Framework to utilize TLS 1.3. OpenSSL is more stable but Network Framework can provide more cutting-edge features but very unstable.

### debug-cpu-usage

Enable CPU debug mode. This may slow down the performance.

### debug-memory-usage

Enable memory debug mode. This may slow down the performance.

### doh-format

Available values: wireformat, json. Default: wireformat

### doh-follow-outbound-mode

By default, the DOH lookup uses the direct outbound. Enabling the option makes the DOH follow the outbound mode settings and rules.

### doh-server

The URL of the DNS-over-HTTPS server.

### use-local-host-item-for-proxy

By default, DNS lookup is always performed on the remote server if a proxy policy is used. After enabling this option, Surge uses the IP address instead of the domain to set up the proxy connection if the local DNS mapping result of the target domain exists.

### geoip-maxmind-url

The URL of the GeoIP database for updating.

### disable-geoip-db-auto-update

Disable the auto-updating for the GeoIP database.

### allow-dns-svcb

iOS system might perform an SVCB record DNS lookup instead of a standard A record lookup. This causes Surge to fail to return a virtual IP address. So by default, the SVCB record lookup is forbidden to force the system to perform an A record lookup.

### udp-policy-not-supported-behaviour

The fallback behavior when UDP traffic matches a policy that doesn't support UDP relay. Possible values: DIRECT, REJECT.

### proxy-test-udp

(null)

### compatibility-mode (iOS Only)

Not available

### allow-wifi-access (iOS Only)

Allow Surge proxy services access from other devices in the LAN.

### wifi-access-http-port (iOS Only)

The port number of Surge HTTP proxy service.

### wifi-access-socks5-port (iOS Only)

The port number of Surge SOCKS5 proxy service.

### wifi-access-http-auth (iOS Only)

Require authentication for Surge HTTP proxy service. E.g.: username:password

### include-all-networks (iOS Only)

By default, some requests might not be taken over by Surge. For example, apps can bind to the physical network interface to bypass Surge VIF. Enabling the Include All Networks option to make sure all requests are handled by Surge without leaking. This option is useful when you use Surge as a firewall. (Requires iOS 14.0 or above)

Enabling this option may cause AirDrop and Xcode debugging issues, Surge Dashboard via USB not working, and other unexpected side effects. Use with caution.

### include-local-networks (iOS Only)

Enable this option to make Surge VIF handle requests sent to LAN. (Requires iOS 14.2 or above)

Enabling this option may cause AirDrop and Xcode debugging issues, Surge Dashboard via USB not working, and other unexpected side effects. Use with caution.

### wifi-assist (iOS Only)

Enable Wi-Fi assist.

### hide-vpn-icon (iOS Only)

Hide the VPN icon in the status bar.

### ipv6-vif (iOS Only)

Allow the IPv6 through Surge VIF. Useful when you want Surge to handle raw TCP connections connecting to IPv6 addresses.

### all-hybrid (iOS Only)

Not available

### allow-hotspot-access (iOS Only)

Allow Surge proxy services access from other devices while Personal Hotspot is on.

### use-default-policy-if-wifi-not-primary (macOS Only)

If disabled, SSID/BSSID patterns can still match even when Wi-Fi is not the primary network interface.

### read-etc-hosts (macOS Only)

Follow local DNS mapping items in /etc/hosts.

### http-listen (macOS Only)

The HTTP proxy service listen parameter. E.g.: 0.0.0.0:6152

### socks5-listen (macOS Only)

The SOCKS5 proxy service listen parameter. E.g.: 0.0.0.0:6153


