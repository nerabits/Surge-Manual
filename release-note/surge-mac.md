# Surge Mac Release Note

## Surge Mac V3

### Version 3.2.0

**Scripting**

* New major feature: scripting. You may use JavaScript to modify the response as you wish. See the manual for more information: https://manual.nssurge.com/http-processing/scripting.html
* You can now use a script to modify the response headers and status code.

**Dashboard**
* USB module has been refactored to improve stability. Also, you may choose the device from multiple USB devices now.

**MitM**
* HTTP and MitM engine has been refactored. Please report if you encounter any issues.
* You can now use URL-REGEX rule for MitM connections.
* You may use prefix '-' to exclude domains for MitM. Example: 
```
[MITM]
hostname = -*.apple.com, -*.icloud.com, *
```
* MitM hostname list now supports port number. By default only the connections to port 443 will be decrypted. Use suffix :port to enable MitM for other ports. Use suffix :0 to enable MitM for all ports on the hostname.
* URL rewrite type 'header' is now available for MitM connections. You may also use it to rewrite a plain HTTP request to an HTTPS request.

**Misc**
* You can now enable/disable a rule.
* Added a small indicator in the menu icon for Metered Network Mode.</lo>
* Added main switches for rewrite and scripting.
* Supports TCP SACKs for Surge VIF.
* New general option: force-http-engine-hosts. You can force Surge to treat a raw TCP connection as an HTTP connection, to enable high-level functions such as URL-REGEX rules, rewrite and scripting. This option uses the same format as [MITM] hostname option.
* New option for url-test/fallback group: evaluate-before-use. By default, the requests before a connection evaluation will use the first policy in the list and trigger the evaluate. Enable the option to delay the requests until the evaluation completed.

https://www.nssurge.com/mac/v3/Surge-3.2.0-860.zip

### Version 3.1.1

* Bug fixes.

https://www.nssurge.com/mac/v3/Surge-3.1.1-811.zip

### Version 3.1.0

* Added more feature to the main menu.
* Dashboard now supports to export all requests to an archive file for opening later or sharing.
* Supports a new proxy protocol: Snell. (https://github.com/surge-networks/snell)
* Surge Mac can work as a Snell proxy server now. See https://manual.nssurge.com/others/snell-server.html for more information.
* A new option to automatically reload if the profile was modified externally/remotely.
* Fixed a compatibility issue with some FTP clients.
* Added a new option to disable automatically notification dismissing.
* The update notification is now shown as a banner instead of an alert window.
* Bug fixes.

https://www.nssurge.com/mac/v3/Surge-3.1.0-807.zip

### Version 3.0.6

* Optimizations for no network error handling.
* Reduces CPU usage on idle.
* Fixed a bug while enabling MitM with a new certificate.
* Fixed crashes on macOS 10.11.

https://www.nssurge.com/mac/v3/Surge-3.0.6-781.zip


### Version 3.0.5

* CPU usage optimizations (50% reduced for high throughout).
* Enabled Hardened Runtime to get enhanced security protections in macOS Mojave.
* Add more notes for rule evaluating stage.
* WeChat.app may flood ping when network is unstable, which causes a high CPU usage of Surge. We added a mechanism to limit ICMP throughput in this version.

https://www.nssurge.com/mac/v3/Surge-3.0.5-773.zip


### Version 3.0.4
          
* Added a new option 'hijack-dns' to hijack DNS queries to other DNS servers with fake IP addresses. See manual for more information: https://manual.nssurge.com/others/misc-options.html.
* Bug fixes

https://www.nssurge.com/mac/v3/Surge-3.0.4-759.zip


### Version 3.0.3

* Supports new iCloud container for Surge iOS migration.
* The MitM feature is now compatible with Android system. Please regenerate an new CA certificate before using with Android.
* Fixed some UI issues in Dashboard.
* Fixed a bug that MitM may refuse to enable after modifying settings.
* Fixed a bug that br decompress may fail.
* Fixed a bug that the menu item may use a wrong color if the accent color of system isn't blue.
* Fixed the JSON viewer color issue in the Dark Mode.
* Minor bug fixes.
                
https://www.nssurge.com/mac/v3/Surge-3.0.3-754.zip

### Version 3.0.2

* Allows import the profile from a URL.
* Fixed an issue that the HTTP capture button may show wrong state in Dashboard.
* Fixed an issue that Dashboard doesn't show User-Agent as the process name while connecting to iOS device.
* Fixed an issue that the bandwidth of processes may be inaccurate.
* Fixed an issue that the DEST-PORT rule may not be parsed.
* Fixed an issue that ruleset can't be used with logical type rule.

https://www.nssurge.com/mac/v3/Surge-3.0.2-736.zip

### Version 3.0.1

* Fixed an issue that TFO option will not be saved.
* Fixed an issue that UDP relay option shows wrong state.
* Fixed some i18n issues.
* Fixed crashs on macOS 10.11.
* Save proxy declarations with legacy style (custom) if the proxy is written in legacy style in the text file.
* Other minor bug fixes.

https://www.nssurge.com/mac/v3/Surge-3.0.1-711.zip

### Version 3.0.0

https://www.nssurge.com/mac/v3/Surge-3.0.0-702.zip

## Surge Mac V2

### Version 2.6.7

* Fixed a compatibility issue with 304 response.
* Fixed a Dashboard crash.

https://www.nssurge.com/mac/Surge-2.6.7-656.zip

### Version 2.6.6

* Fixed a compatibility issue with 304 response.
* Fixed an issue that Dashboard may not use the correct encoding to decode text body.

https://www.nssurge.com/mac/Surge-2.6.6-654.zip

### Version 2.6.5

* Bug fixes.

https://nssurge.com/mac/Surge-2.6.5-652.zip

### Version 2.6.4

* Bug fixes.

https://nssurge.com/mac/Surge-2.6.4-647.zip

### Version 2.6.3

* New Features: External Proxy Provider. See https://medium.com/@Blankwonder/surge-mac-new-features-external-proxy-provider-375e0e9ea660 for more information.
* Surge will automatically track system proxy settings now. When Surge is no longer the default proxy, the status icon will turn grey and a notification will raise.
* Fixed a compatibility issue with Docker.

https://nssurge.com/mac/Surge-2.6.3-637.zip

### Version 2.6.2

* Fixed an issue that the UDP mode with AEAD ciphers doesn't work.
* Bug fixes.

https://nssurge.com/mac/Surge-2.6.2-618.zip

### Version 2.6.1

* Surge now allows expired DNS answers for performance reasons. See 'Optimistic DNS' section in https://developer.apple.com/videos/play/wwdc2018/714/ for more information.
* Performance improvements.
* Fixed an issue that UDP traffics are not included in the real-time speed.
* Supports hardware acceleration for AES-GCM encryption.
* Supports NAT64 in a pure IPv6 network. (Previous versions already supported DNS64)

https://nssurge.com/mac/Surge-2.6.1-612.zip

### Version 2.6.0

* Supports using Surge Mac as a gateway.
* A new setup guide view.
* A new config panel for traffic capture options.
* Fixed an issue which Dashboard may disconnect unexpectedly under huge pressure.
* The status bar icon will be red while traffic capture is enabled.
* Improved TUN interface performance.
* Enabling TCP Fast Open in macOS 10.14.

https://nssurge.com/mac/Surge-2.6.0-596.zip

### Version 2.5.3

* Supports UDP relay for shadowsocks protocol. A brief introduction in Chinese: https://trello.com/c/ugOMxD3u.
* You may use Dashboard to view UDP conversations.
* Dashboard now can save multiple remote machine profiles.
* Improved the JSON viewer in Dashboard.
* Added an UI switch for the dns-failed option in FINAL rule.
* Bug fixes.

https://nssurge.com/mac/Surge-2.5.3-563.zip

### Version 2.5.2

* You may toggle the hidden state of columns in Dashboard now.
* Supports to export selected rows to csv file.
* Added a connection duration column in Dashboard.
* Supports obfs-uri parameter.
* Improved the benchmark view.
* Fixed a serious bug in the SOCKS5 proxy implementation.
* Bug fixes.

https://nssurge.com/mac/Surge-2.5.2-544.zip

### Version 2.5.1

* The MitM enabling switch has been moved to the main menu and isolated from profile.
* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.5.1-528.zip

### Version 2.5.0

* Added Outbound Mode options: Direct Outbound, Global Proxy and By Rule.
* Added options for all policy to specify outgoing interface: 'interface' and 'allow-other-interface'.
* Added all_proxy environment variable for 'Copy Shell Export Command'
* Supports client-side SSL/TLS certificate validation for HTTPS and SOCKS5-TLS proxy. A config example is here: https://gist.github.com/Blankwonder/cd9fa1987e41cf1a1f1df50583ba1d9c (DO NOT support editing with UI in this version.)
* Refined MitM.
* Concurrently setup connection to host with Round-robin DNS to boost performance.
* Bug fixes.
                
http://dl.nssurge.com/mac/Surge-2.5.0-520.zip

### Version 2.4.6

* Supports xchacha20-ietf-poly1305.
* Bug fixes.
* HTTP request header and response header can be extracted from TCP connection now. (SOCKS5 and TUN)
* Enhanced mode can handle all connections now, even for connections initialized with IP address directly.
* Surge TUN now supports forwarding ICMP packets.

**From this version, the minimum system version requirement was raised to macOS 10.11. If you are still using macOS 10.10, please use version 2.4.5.**

http://dl.nssurge.com/mac/Surge-2.4.6-490.zip

### Version 2.4.5

* Bug fixes.
* Improved performance for high concurrency.
* TCP fast open has been disabled temporarily since there is a serious problem in macOS/iOS kernel.
* Dashboard will display decoded URL query now.

http://dl.nssurge.com/mac/Surge-2.4.5-468.zip

### Version 2.4.4

* Supports obfs=tls for shadowsocks protocol.
* Refined the proxy edit panel.
* Added Simplified Chinese language.

http://dl.nssurge.com/mac/Surge-2.4.4-459.zip

### Version 2.4.3

* Supports obfs=tls for shadowsocks protocol.
* Refined the proxy edit panel.
* Added Simplified Chinese language.

http://dl.nssurge.com/mac/Surge-2.4.3-457.zip

### Version 2.4.2

* Fixed an issue that enhanced mode may not be closed properly when switching to a profile without dns-server.
* Fixed an issue that managed profile updating and license info are unavailable while enhanced mode enabled.
* When the necessary port is used by another process, the error alert will show which process is using the port.
* Fixed an issue that map local items can't be edited with UI.
* Fixed an issue that system proxy settings may not be reset properly.
* Auto URL test group will execute a retest immediately after the selected policy has failed.

http://dl.nssurge.com/mac/Surge-2.4.2-445.zip

### Version 2.4.1

* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.4.1-439.zip

### Version 2.4.0

* Supports enterprise license and profile management.
* Fixed a bug that some fields are unavailable in the configuration panel in some cases.
* Fixed a bug that the FINAL rule can't be edited.
* Fixed a bug that you may not be able to use custom storage path for profiles.
* The interface related options are no longer controlled by profile. Sorry for the repetitive changes.
* You may use $1, $2 to use the matched string in the value while using header rewrite.
* Added an option for HTTP/HTTPS proxy: always-use-connect. When it is true, Surge will use CONNECT method for plain HTTP requests.

http://dl.nssurge.com/mac/Surge-2.4.0-429.zip

### Version 2.3.2

* Added a option to control whether show proxy error notification.
* Fixed a problem that Dashboard show data doesn't exist error.

http://dl.nssurge.com/mac/Surge-2.3.2-421.zip

### Version 2.3.1

* Added a wizard to install CA’s root certificate for iOS simulator.
* Connectivity quality is now an option. (Not show by default)
* Line comments in [Rule] section in profile file is now presented in UI.
* You may add proxy rule with Dashboard by right-clicking the request or process.
* Dashboard will always open a new window for local machine, instead of asking. You may use "File" menu to connect to a remote machine.
* Added a patch mechanism for adjusting settings for managed config. See manual for more information: https://manual.nssurge.com/others/managed-configuration.html

http://dl.nssurge.com/mac/Surge-2.3.1-420.zip

### Version 2.3.0

* Completely redesign the configure interface. You may configure every function with UI now.
* Proxy benchmark is now moved to main application from Dashboard.
* New feature: Header rewrite. See manual for more information: https://manual.nssurge.com/header-rewrite.html.
* You may switch profile with command line now: surge-cli switch-profile profilename.

http://dl.nssurge.com/mac/Surge-2.3.0-416.zip

### Version 2.2.4

* Notifications presented by Surge will be removed from Notification Center automatically.
* The interval of attempts to refresh managed config changes to one hour from one minute. (After config expired)
* Supports new encryption methods for shadowsocks-libev 3.0.
* Optimized Dashboard performance.
* Supports TCP Fast Open for shadowsocks proxy. You need add "tfo=true" flag in [Proxy] section to enable the feature. You may use benchmark to confirm TFO is working.
* You can sort benchmark results now.
* You may choose to reload config after managed config updated.

http://dl.nssurge.com/mac/Surge-2.2.4-394.zip

### Version 2.2.2

* Fixed a bug when using SOCKS5 without authorization.

http://dl.nssurge.com/mac/Surge-2.2.2-375.zip

### Version 2.2.1

* You may use Dashboard to benchmark proxies now.
* Fixed "Too many open files" error by raising limit to 2048.
* Fixed a bug in SOCKS5 with authorization.
* Fixed a bug that managed config may refresh continuously.

http://dl.nssurge.com/mac/Surge-2.2.1-374.zip

### Version 2.2.0

* Map local function is now available.
* Adds notifications when proxy encounters errors.
* Network changed notification will show service name instead of BSD name now.
* Fixed a bug that Dashboard may show the incorrect state of body dump.
* Changes for HTTPS and SOCK5-TLS proxy:
  * Option 'skip-common-name-verify' is deprecated.
  * Add a new option 'skip-cert-verify' to skip certificate verify completely.
  * Add a new option 'sni' to customize SNI field while handshaking. You may use 'sni=off' to disable SNI.
* New rule type: PROCESS-NAME, USER-AGENT and URL-REGEX.
* You can use simple wildcard matching (? and *) for PROCESS-NAME rule, local DNS mapping and MitM hosts.
* Dashboard supports display POST form data in a table view.
* You may let Surge reload config by sending SIGHUP. You can use command 'killall -HUP Surge' or 'surge-cli reload'.
* Managed configuration is supported now.
* Add a new option 'skip-server-cert-verify' for MitM.

http://dl.nssurge.com/mac/Surge-2.2.0-368.zip

### Version 2.1.4

* Fixed a bug that helper may crash on macOS 10.10.
* Add a option to remove Surge helper for troubleshooting.
* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.1.4-362.zip

### Version 2.1.3

* Fixed a bug that helper may crash on macOS 10.10.
* Add a option to remove Surge helper for troubleshooting.
* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.1.3-337.zip

### Version 2.1.2

* New option: Collapse policy group items in menu
* Fixed a bug that enhanced mode DNS settings may not be reverted.
* Hold option key to click 'Copy Shell Export Command' to get a command with primary interface IP instead of 127.0.0.1.
* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.1.2-327.zip

### Version 2.1.0

* New feature: Enhanced Mode

  Some applications may not obey the system proxy settings. Using enhanced mode can make all applications handled by Surge.
  
* New rule type: IP-CIDR6

  Example: IP-CIDR6,2005::/16,DIRECT,no-resolve

* The /etc/hosts file will be reloaded automatically if it has changes.

http://dl.nssurge.com/mac/Surge-2.1.0-318.zip

### Version 2.0.13
* Dashboard supports to use ⌘ + 1,2,3,4 to switch panel.
* Dashboard Supports handoff with Surge iOS.
* Fixed a bug that Dashboard may show incorrect process name.

http://dl.nssurge.com/mac/Surge-2.0.13-304.zip

### Version 2.0.12

* Bug fixes.
* Supported SNI while performing MitM.
* The original certificate will be resigned and used while performing MitM, instead of generating a new certificate.

http://dl.nssurge.com/mac/Surge-2.0.12-295.zip

### Version 2.0.11

* Rule test cache will be flushed after network switching now.
* Added a option 'Grey icon if set as system proxy is disabled'.
* Bug fixes and performance improvements.

http://dl.nssurge.com/mac/Surge-2.0.11-289.zip

### Version 2.0.10

* Surge talks to HTTP proxies with a plain HTTP method for non-HTTPS requests now, instead of CONNECT.
* Improved compatibility with some HTTP server.
* Improved compatibility with some DNS server.

http://dl.nssurge.com/mac/Surge-2.0.10-280.zip

### Version 2.0.9

* Dashborad: The height of the detail panel will not change now while switching pages.
* A notification will show when proxy client access from other machine.
* Used SF Mono as monospaced font for header and body data display.
* Supported TCP half-open mechanism.

http://dl.nssurge.com/mac/Surge-2.0.9-273.zip

### Version 2.0.8
 
* Add a new option 'exclude-simple-hostnames' in the gereral section.
* Dashborad: Selected row will not be lost while the filter or sort column changed.
* Dashborad: Fixes some issues in the active panel.

http://dl.nssurge.com/mac/Surge-2.0.8-260.zip
 
### Version 2.0.5
 
* Bug fixes.

http://dl.nssurge.com/mac/Surge-2.0.5-255.zip

### Version 2.0.3

* New feature: Show connectivity quality in menu.

	Surge will send a DNS question to all DNS servers concurrently to test physical network connectivity while opening the menu.

* Fixes a problem that Surge may freeze while opening the menu.
* Fixes a problem that if a policy group contains duplicate policies, Surge may crash.

http://dl.nssurge.com/mac/Surge-2.0.3-250.zip
 
### Version 2.0.2

* Dashboard will no longer display process icon in remote mode.
* Fixes a bug: "Set as System Proxy" option does not work properly if only SOCKS service is enabled.
* Fixes a bug: Dashboard can't add a rule with no-resolve option on and comment not empty.
* Minor bug fixes.

### Version 2.0.1

* Bug fixes


