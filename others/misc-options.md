# Miscellaneous Options in [General] Section

As the options change frequently, you may look up the most up-to-date explanation for the [General] section options within the app.

- Surge Mac: Main Window Menu -> Help -> Profile Syntax
- Surge iOS: More Tab -> Help -> Profile Syntax


```
[General]
ipv6 = false
loglevel = notify
skip-proxy = 127.0.0.1, 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, localhost, *.local
tun-excluded-routes = 192.168.0.0/16, 10.0.0.0/8, 172.16.0.0/12
tun-included-routes = 192.168.1.12/32
```

### loglevel

Log level. One of verbose, info, notify, or warning. It's not recommended to enable verbose in daily use because this slows down the performance significantly.

### ipv6

Enable full IPv6 support.

### dns-server

The IP addresses of upstream DNS servers.

### skip-proxy

In the iOS version, this option forces connection to these domain/IP ranges to be handled by Surge VIF, instead of Surge proxy. In the macOS version, these settings are applied to the system when "Set as System Proxy" is enabled. This option is used to fix compatibility problems with some apps.

  - To specify a single domain, enter the domain name - for example, apple.com.

  - To specify all websites on a domain, use an asterisk before the domain name - for example, \*apple.com.

  - To specify a specific part of a domain, specify each part - for example, store.apple.com.

  - To specify hosts or networks by IP addresses, enter a specific IP address such as 192.168.2.11 or an address range, such as 192.168.2.\* or 192.168.2.0/24.

Notice: If you enter an IP address or address range, you are only able to bypass the proxy when you connect to that host using that address, not when you connect to the host by a domain name that resolves to that address.

### exclude-simple-hostnames

Just like the skip-proxy parameter. This option lets requests using simple hostnames (without dot) handled by Surge VIF instead of Surge proxy.

### external-controller-access

This option allows an external controller to control Surge, such as Surge Dashboard (macOS) and Surge iOS Remote Controller (iOS). E.g.: key@0.0.0.0:6165

### http-api

This option allows using HTTP APIs to control Surge. E.g.: key@0.0.0.0:6166

### http-api-tls

Use HTTPS protocol instead of HTTP. The MitM CA certificate must be configured first. You need to install the certificate on the client device manually.

### http-api-web-dashboard

You may control Surge via a web browser after enabling this.

### show-error-page-for-reject

Show an error webpage for REJECT policy if the request is a plain HTTP request.

### tun-excluded-routes

Surge VIF can only process TCP and UDP protocols. Use this option to bypass specific IP ranges to allow all traffic to pass through.

Notice: This option only works for Surge VIF. Requests handled by Surge Proxy Server aren't affected. Combine 'skip-proxy' and 'tun-excluded-routes' to make sure that specific HTTP traffic bypasses Surge.

### tun-included-routes

By default, Surge VIF interface declares itself as the default route. However, since the Wi-Fi interface has a smaller route, some traffic may not go through Surge VIF interface. Use this option to add a smaller route.

### internet-test-url

The URL for the Internet connectivity testing. Also the testing URL for DIRECT policy.

### proxy-test-url

The default testing URL for proxy policies.

### test-timeout

The connectivity testing timeout.

### always-real-ip

This option asks Surge to return a real IP address instead of a fake IP address when Surge VIF handles a DNS question.

The DNS packet will be forwarded to upstream DNS servers.

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


