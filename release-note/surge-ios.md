# Surge iOS Release Note

### Version 5.0.0 (Aug 10, 2022)

Surge 5.0 comes with a brand new UI design, including a brand new policy group selection view, a new Start tab, and a new icon.

And now you can try all the features for free for seven days before you purchase.

#### New Features:
- DNS over QUIC and DNS over HTTP3 support
- Real-Time View: Show live speed or request list floating window when using other applications.
- Subnet Setting: Override global settings under specified networks.

#### Minor updates:
- Comprehensive UI improvements.
- New contextual menu in the tab bar items.
- Fixed a bug that encrypted-dns-skip-cert-verification may not work
- MITM hostname and force-http-engine-hosts now support keywords: `<ip-address>`, `<ipv4-address>`, and `<ipv6-address>`.
- Script added function `$utils.ipasn(ipAddress:<String>)` to lookup ASN.
- Script added function `$utils.ipaso(ipAddress:<String>)` to lookup ASO
- Script added function `$utils.ungzip(ipAddres:<Uint8Array>)` for gzip decompression.
- Bug fixes.

### Version 4.15.0 (Jun 30, 2022)

#### MITM over HTTP/2

- Surge now supports performing MITM with HTTP/2 protocol to improve concurrent performance.
- Surge now supports performing MITM on WebSocket connections.

#### Others

- You may use `doh-skip-cert-verification=true` to disable server certificate verification for DNS-over-HTTPS.
- Bug fixes.

### Version 4.14.0 (Jun 1, 2022)

#### SSH Proxy Support
- You can use SSH protocol as a proxy protocol. The feature is equivalent to the `ssh -D` command.
- Both password and public key authentications are supported.
- All the four types of private keys, RSA/ECDSA/ED25519/DSA, are supported.
- Surge only supports `curve25519-sha256` as the kex algorithm and `aes128-gcm` as the encryption algorithm. The SSH server must use OpenSSH v7.3 or above. (It should not be a problem since OpenSSH 7.3 was released in 2016.)

#### Keystore
- You may now save sensitive keystore items to the system keychain.
- You may now configure TLS client certificate authentication with the UI.
- You may use a keystore item as the CA certificate for MITM.

#### Others
- New rule type: `IP-ASN`. You may use the rule to match the autonomous system number of the remote address.
- The request details now include the ASN and ASO information of remote IP addresses.
- You can now enable/disable the rewrite rules and DNS local mapping items.
- The preview of SVG images is removed. You can use the new Web View to see the SVG image.
- Bug fixes.

---

### Version 4.13.0 (Apr 24, 2022)

#### HTTP Capture
- You can now export HTTP/HTTPS requests to a HAR file, which is a standard format and can be opened by many web analysis tools
- The image viewer now supports SVG format.

#### Proxy
- New parameter `server-cert-fingerprint-sha256` for TLS proxy policies. Use a pinned server certificate instead of the standard X.509 validation.
- `tls-engine` option is now deprecated. OpenSSL is now the only TLS engine.
- You can now use a full profile as the external policy group (policy-path). All proxies in the [Proxy] section will be used.

#### MITM
- You can export the CA certificate to a P12 or PEM file.
- Fixed an issue that the CA certificate can’t be installed if the default browser isn’t Safari.

#### Header Rewrite
- Header rewrite now supports using the regex to replace the value.
- Header rewrite now supports modifying the response headers.
Scripting
- The default timeout of $httpClient is now 5 seconds and you may override it with the timeout parameter.
- You can manage the data of $persistentStore with the UI now.
- You may edit the argument with UI now.

#### Remote Controller
- You may sort and search in the remote device list.

---

### Version 4.12.0 (Mar 18, 2022)

#### New Feature: Personal Hotspot Proxy Access

- When using an iPhone/iPad as a hotspot, an HTTP or SOCKS5 proxy can be used on the client device to take over the traffic using Surge iOS.

- The proxy IP to be configured on the client is shown in the More Settings and the port number is the same as the WiFi proxy service.

#### New Feature: Hybrid Network

- Instead of setting up connections with cellular data when the Wi-Fi network is poor, always set up connections with Wi-Fi and cellular data simultaneously.

- This feature can improve the network experience significantly on poor Wi-Fi or when the Wi-Fi network is switching.

#### WireGuard

- WireGuard supports multiple peers.

- The allowed-ips now support multiple IP ranges.

- WireGuard supports preshared-key and keepalive.

- WireGuard supports peers with IPv6 endpoints. (But still no IPv6 tunnel support)

- WireGuard now supports underlying-proxy.

- The raw TCP connections are now relayed on the L3 layer if no high-level features are used.

#### Detached Profile

- You can now include multiple detached profiles in one section. But the section will be marked read-only and can't be edited with UI.

`#!include A.dconf, B.dconf`

#### Policy Group

- You can now temporarily override an auto test group or an SSID group's optimal option, until Surge restart or reload.

- The new parameter include-all-proxies=true is added to the policy group, which will include all proxy policies defined in the [Proxy] section, and can be used with the policy-regex-filter parameter for filtering.

- The new parameter include-other-group="group1,group2" is added to include policies from another policy group, and can include multiple policy groups separated by commas, also can be used with the policy-regex-filter parameter for filtering.

- include-all-proxies, include-other-group, and policy-path parameters are allowed to be used in a single policy group at the same time. The policy-regex-filter parameter applies to all three.

- There is an order of precedence among the policy groups for the include-other-group parameter, but there is no order of precedence among the include-all-proxies, include-other-group, and policy-path parameters. For scenarios where the order of sub-policies makes sense (e.g., fallback groups), use policy groups nesting with include-other-group.

#### Subnet expression

- SSID Group is now upgraded to Subnet Group, which supports subnet expression.

- SSID Setting now supports subnet expression.

- The SUBNET rule now supports subnet expression.

- The [SSID Setting] can control the TCP Fast Open behavior now. Read the manual for more information.

- The [SSID Setting] can control the Wi-Fi assist and Hybrid Network behavior now. Read the manual for more information.

#### Proxy Protocol

- The Trojan protocol now supports using WebSocket as the transport layer.

- Shadowsocks protocol now supports underlying-proxy for UDP relay.

- You may configure the UDP testing endpoint for proxies. e.g., proxy-test-udp = google.com@1.1.1.1

- You may benchmark a single proxy by long press on the proxy cell.

#### Module

- New Official Module: Block HTTP3/QUIC

- Surge will check updates for installed modules automatically.

#### Others

- Performance improvements.

- OpenSSL is now the default TLS engine.

- The managed profile can be opened with the text editor now.

- The default timeout of $httpClient is 5 seconds now.

- Reduced the app package size.

- You need to perform a one-time Dropbox re-authorization if you are using Dropbox syncing.

- Modules allow modifying the skip-server-cert-verify and tcp-connection parameters of [MITM].

- The client will get an ICMP connection refused message instead of TCP RST if a REJECT policy matches.

- Supports IPv6 addresses with scope ID.

- The Network diagnostics can test proxy UDP relay now.

- Bug fixes.

---

### Version 4.11.1 (Jan 27, 2022)
- You may edit the profile in the text mode without changing the current profile now.
- The REJECT policy now can evolve to REJECT-DROP policy for UDP traffics.
- Bug fixes.

---

### Version 4.11.0 (Jan 21, 2022)

#### Proxy Protocol Upgrades:

- WireGuard: Uses Surge as a WireGuard client, converting L3 VPN as an outbound proxy policy.
- Snell V3: Snell protocol now supports UDP relay.
- Trojan protocol now supports UDP relay. (No additional parameter required)
- VMess protocol supports VMessAEAD. (Policy parameter: vmess-aead = true)

#### Improvements:
- The underlying proxy (aka proxy chains) now supports using a policy group.
- New parameter: udp-policy-not-supported-behaviour. To control the fallback behavior when UDP traffic matches a policy that doesn't support UDP relay.
- You may acquire the request's headers within an http-response script via $request.headers.
- Performance optimization.
- Bug fixes.

---

### Version 4.10.0 (Dec 3, 2021)
- You may extend your Surge iOS Pro license to 6 devices for free. You may find the guidance in the License Management view.

#### New Features
- Sorting option in the request list.
- Supports remote rule editing for the remote controller.
- Added the effective order adjustment view for the module. You can now adjust the effective order of the module.
- Supports custom the policy IP TOS field. Example: test-policy = direct, tos=0xb8.

#### Other Improvements
- UI details refined.
- Performance improvements.
- The network changed notification message will display the data network operator. If network automatic switching is enabled, you can use the notification to confirm the current carrier.
- The URL query part of the HTTP request is no longer displayed in the request list. It is now displayed in the details view.
- Fixed the problem that the JavaScript script timeout mechanism might not work properly.
- Fixed an issue that could occur when a load-balance group contains another group.
- Removed the "All" option from traffic statistics, as it took too long to count all historical traffic when the feature had not been used for a long time.
- You may remove devices in DDNS and Cloud Notification views.

---

### Version 4.9.4 (Oct 28, 2021)
Bug fixes

---

### Version 4.9.3 (Sep 30, 2021)
- New feature: Information Panel. Read the manual for more info: https://manual.nssurge.com/others/panel.html
- The profile now supports the profile version remark. Read the manual for more info: https://manual.nssurge.com/release-note/profile-version.html
- The HTTP scripts now support binary mode to modify the request/response body.
- Other minor improvements and bug fixes.

---

### Version 4.9.2 (Sep 3, 2021)

Bug fixes

---

### Version 4.9.1 (Aug 24, 2021)

Bug fixes

---

### Version 4.9.0 (Aug 20, 2021)

#### New Features: Surge Private DDNS
Surge Mac can associate its external IP address to .sgddns hostname. You may use the hostname with Surge iOS or Surge Mac on another device. The data is synced via iCloud, and the hostname can't be used publicly.

#### New Features: Egress Control (No UI Settings Currently)
- You can use the new internal policy HYBRID to make requests to try Wi-Fi and cellular simultaneously. You can also use the "hybrid=true" parameter to gain a proxy policy for the behavior.
- You can now tell Surge to use IPv4 or IPv6 under a dual-stack environment. Read the manual for more information.

#### New Features: Profile Syntax
You can look up the configuration parameters for the text editing mode within the app. It always displays the syntax for the current version.

#### New Features: Surge VIF IPv6 Stack (No UI Settings Currently)
Surge VIF now supports the IPv6 stack for the raw TCP connections. Use parameter "ipv6-vif=true" to enable.

#### Improvements
- We have changed the proxy benchmark standard. The result is now similar to a ping test result, which ignores the proxy setup cost.
- $request.id is added to the http-request and http-response scripts for continuity among scripts.
- Bug fixes.

---

### Version 4.8.0 (Jun 14, 2021)
New Features:
- Request Display Filter
You may use multiple conditions to filter which requests to show.
- Web Dashboard
You may control Surge via a web browser on local or remote devices.

Other bug fixes and improvements.

---

### Version 4.7.0 (Apr 21, 2021)

#### Rules

- New rule type: SUBNET, which can match SSID/BSSID/router IP address with a wildcard pattern.
- New rule type: CELLULAR-CARRIER, which can match the MCC-MNC code.
- New rule type: CELLULAR-RADIO, which can match the radio access technology of the cellular network.

#### Profile

- You may put partial sections into a detached file. See manual for more information.

#### HTTP API

- Added new profile related HTTP APIs, including GET /profiles, POST /profiles/check
- Added new device management HTTP APIs, including: GET /devices, POST /devices, GET /devices/icon
- The HTTP API, proxy services, and external controller now support listening on IPv6 addresses. (No UI supports. Manual profile editing is required.)
- You may now use 'http-api-tls=true' enable TLS for HTTP API access. (aka HTTPS-API)

Other bug fixes and improvements.

---

### Version 4.6.0 (Feb 26, 2021)

#### Remote Controller

- You may use this remote controller to view real-time statistics, and events and perform network diagnostics remotely.
- You may use the remote controller to control the DHCP server feature of Surge Mac, including adjusting each device's settings.

#### Cloud Notification
- You can receive Surge Mac's notifications on your iOS device.

#### Scripting
- You may execute a script with Siri or Shortcuts.

#### Policy Group
In this release, we completely refactored the policy group functionality, bringing the following changes:
1. The url-test/fallback/load-balance policy group can no longer be configured with a specific testing URL but with a global testing URL or a policy-configured testing URL. The policy's test results can be used directly in all policy group decisions, eliminating the need to retest each policy group individually.
2. All types of policy groups support mixed nesting. The only requirement is that no circular references can be used.
3. When a group policy is used as a sub-policy of the url-test/fallback/load-balance group.
- The latency of the select/url-test/fallback/ssid group is the latency of the selected policy.
- The latency of the load-balance group is the average of the latencies of all available policies.
4. The timeout parameter of a policy group marks policies with latency exceeding this parameter as unavailable when making decisions for the group. But the maximum time taken to test the policy group is controlled by the global test-timeout parameter. (Default is 5s)
5. When testing a group due to decision making, all sub-policies that the group may use are tested, including sub-policies of the sub-policy group.
6. You may use no-alert=true parameter to suppress notifications for particular groups.

---

### Version 4.5.1 (Jan 20, 2021)

Bug fixes

---

### Version 4.5.0 (Jan 19, 2021)

- New Feature: Network Layer Packet Capture: You may now capture the raw TCP/UDP/ICMP packets and inspect them right on the device. Or you can export a standard .pcap file for other tools.
- You can customize the GeoIP database updating URL now.
- The GeoIP database can be updated automatically now.
- Bug fixes and improvements.

---

### Version 4.4.3 (Oct 28, 2020)

- Optimized for the iPhone 12 series.
- Modified requests are now marked with orange color.
- Bug fixes.

---

### Version 4.4.2 (Sep 25, 2020)

Bug fixes

---

### Version 4.4.1 (Sep 23, 2020)

Bug fixes

---

### Version 4.4.0 (Sep 20, 2020)

New Features:
- HTTP API: Control Surge with HTTP API with another app or from another device.
- Proxy Chain: Connection to a remote host will be performed sequentially from one proxy server to another.

Major Improvements:
- You may mix the external proxies with the proxies of the profile in one policy group now.
- The DNS result view has more information.
- You may use 'policy-regex-filter' to include a part of an external proxy list's content.
- New CELLULAR and CELLULAR-ONLY policy.

Minor Improvements:
- iCloud Drive sync improved.
- You may use $notification.post in a script to post a notification with an action URL.
- The HTTP proxy service now supports basic authentication.
- Surge now enables TCP keepalive for all outgoing connections.
- Surge now supports to use of a URL with a username and password to perform basic authentication for an external resource. (https://username:password@example.com)

We recently published official guidance for you to understand Surge. You may find it in the More tab.
Version 4.3.2 (Jun 25, 2020)
Improvements for the latest iOS system.
Version 4.3.1 (Jun 22, 2020)
New Feature: Wi-Fi Timeline
You may check the connected Wi-Fi network timeline, including entering and leaving time.

Minor Changes
- Optimized the timing system. The DNS time cost is now calculated precisely.
- Bug fixes.

---

### Version 4.3.0 (Jun 4, 2020)

New Feature: Mock
- You may mock the API server and return a static response. This feature may also be called as Map Local or API Mocking.
New Feature: Event Center
- You may now review all historical events.

Minor Changes:
- Optimized the classical start view for Dark Mode.
- The Load-Balance group now supports connectivity testing.
- Add a parameter "use-local-host-item-for-proxy", to use local DNS mapping result even through a proxy protocol.
- The module may adjust contents in [SSID Setting] now.
- Optimized Wi-Fi Assist feature.
- You may specify the timeout while using the script editor.
Version 4.2.2 (May 19, 2020)
- New Feature: Traffic Statistics
You may examine the history of traffic usage grouped by the host, by policy, or by the network interface.

- New Feature: DOMAIN-SET
We have added a new type of rule: DOMAIN-SET, which may contain millions of sub-rules. No UI configuration in this version. Please configure with the Text Mode

[Rule]
DOMAIN-SET,hostname.txt,REJECT

Each line in the file is a hostname or an IP address. If the hostname starts with a dot, all sub-domains will be matched.

- Other bug fixes and improvements.
Version 4.2.1 (Apr 28, 2020)
New Feature: Enhanced Wi-Fi Assist
- Surge will try to set up a connection with cellular data when the Wi-Fi network is poor.

Changes in DNS-over-HTTPS
- From this version, if DNS-over-HTTPS is configured, the traditional DNS will only be used to test the connectivity and resolve the domain in the DOH URL.
- The DNS over HTTPS now has a separate parameter: doh-server. The DOH servers in 'dns-server' will be moved to the new parameter after saving.
- The legacy DNS is always required now.
- DOH can be matched with rule 'PROTOCOL,DOH' now.
- Added a new parameter 'doh-follow-outbound-mode'. In the previous version, the DOH client follows the system proxy settings. From this version, all DOH requests will use DIRECT policy by default. If 'doh-follow-outbound-mode' is set, the DOH requests will follow the outbound mode settings regardless of the system proxy settings.

Bug fixes and stability improvements

---

### Version 4.2.0 (Apr 17, 2020)

New Feature: Module
Module is a set of settings to override the current profile. You may use modules to:
- Tweak settings in a non-editable profile, such as managed profile and enterprise profile.
- Change part of settings with one tap. For example, you may use a module to enable MitM for all hostnames and adjust the filter temporarily.
- Use a module written by others to accomplish a particular task. For example, your co-work may share with you a module that rewrites the API requests to a test server.
- When you share one profile among devices, some settings might need modifying for different scenarios. The enabling state of modules won't be synced to other devices, so you can use a module to fulfill.

Minor Improvements:
- Added a new rule type: PROTOCOL.
- Improved the MITM CA certificate install assistant.
- You may now use UI to configure a load-balance policy group.
- You may now use UI to configure SSID suspend.
- Bug fixes.

---

### Version 4.0.2 (Feb 11, 2020)

- Bug fixes
- Supports choosing profiles in a subdirectory
- A new feature has been added: iperf3 client mode.
You may use it to benchmark the bandwidth. Different from the standalone iperf app, you may force the test to use a specified proxy.

A quick guide:
1. Install iperf3 on the proxy server.
2. Run "iperf3 -s" within a screen or tmux session.
3. Start iperf test with Surge. Leave the hostname field empty. 127.0.0.1 will be used and indicates the proxy server itself.
Version 4.0.1 (Dec 31, 2019)
- Support VMess proxy protocol
- Bug fixes

---

### Version 4.0.0 (Sep 18, 2019)

Welcome to Surge 4. We are now introducing the Feature Subscription. As a Pro license owner, you:
· Always have access to all your features for a lifetime.
· Get free enhancement updates for features you already have for a lifetime.
· Get compatibility updates for new systems and new devices for a lifetime.
· Get a one-year free Feature Subscription since your purchasing date.
· Renew the subscription when a new feature impresses you, totally optional.

New features:
· Scripting: Use JavaScript to extend the ability of Surge as your wish.
· Dark Mode: Fully adapted for iOS 13 Dark Mode.
· DNS over HTTPS: Use DNS over HTTPS (DoH, RFC 8484) to perform DNS queries.
· TLS v1.3: TLS v1.3 support for HTTPS/SOCKS5-TLS proxy.
· Dropbox: Use Dropbox to sync your profiles across devices.

---

### Version 3.8.1 (Jun 4, 2019)

Bug fixes

---

### Version 3.8.0 (May 21, 2019)

Proxy
- Rules can be enabled/disabled now. Try sliding left on it.
- New option for url-test/fallback group: evaluate-before-use. By default, the requests before a connection evaluation will use the first policy in the list and trigger the evaluation. Enable the option to delay the requests until the evaluation is completed.

MitM
- HTTP and MitM engine has been refactored.
- You can now use the URL-REGEX rule for MitM connections.
- You may use the prefix '-' to exclude domains for MitM.
- MitM hostname list now supports port numbers. By default, only the connections to port 443 will be decrypted.

Minor Improvements
- Move the 'External Resources' item to the profile list view. Managed profile users may utilize the view to update resources now.
- It won't bother you anymore that the Cloud profiles disappear sometimes.
- Touch ID / Face ID now allows passcode as a fallback.
- Refined English localization.
- Refined UI details.
- The notification banner is draggable now.
- All advanced options can be edited with UI now. Please do not touch it before reading the manual.

Bug Fixes
- Fixed a bug that the request detail page doesn't update in real-time
- Fixed a bug that the GEOIP rule doesn't work for IPv6 addresses.
Version 3.7.1 (Apr 27, 2019)
- Remote Dashboard: You may connect to another device with Surge iOS/Mac running and inspect the requests.
- An active connection can be killed now.
- Bug fixes
Version 3.7.0 (Apr 16, 2019)
- Refined UI, including a fullscreen text editor for complex text fields, new colorful icons, and more detail improvements.
- New feature: Always On. Surge may start automatically even after a device reboot.
- The request detail page now updates in real-time.
- The ruleset can be added or edited with UI now.
- Policy group with an external list can be added or edited with UI now.
- Bug and compatibility fixes.

---

### Version 3.6.1 (Mar 20, 2019)
- Bug fixes

---

### Version 3.6.0 (Mar 15, 2019)

- Added support for a new proxy protocol Snell.
- You may export all dumped requests to a .surgearchive file and open with Surge Mac Dashboard.
- Optimizations for the request search view.
- Experimental feature: You can enable Network.framework to utilize user-space network stack, which can improve throughput, reduce latency and enable cutting edge features such as Multipath TCP.
- Minor bug fixes.

---

### Version 3.5.0 (Jan 3, 2019)
- Performance improvements
- Prompts profile changes via iCloud Drive
- Allows to customize Wi-Fi access ports for HTTP & SOCKS5 proxy services
- Supports to update GeoIP database manually
- Copy cURL is now available for all HTTP methods
- Captured body data may be exported to other apps
- Bug fixes

---

### Version 3.4.2 (Nov 21, 2018)
Bug fixes


