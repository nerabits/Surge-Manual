# FAQ for Surge iOS

Q: How does Surge iOS work?

> There are two main components in Surge: Surge proxy server and Surge TUN interface. After being started, Surge sets itself as the default HTTP/HTTPS proxy server to handle all HTTP/HTTPS traffic, which allows Surge to boost performance by using HTTP connections’ keep-alive mechanism globally. But some apps do not obey system proxy settings (such as Mail.app), because they need to use a raw TCP socket. This kind of traffic is handled by Surge TUN interface.

Q: In the system's battery usage panel, it says that Surge consumes a large portion of power. Why?

> Surge handles all network traffic on your device. So the system counts all network power consumption to Surge. In fact, Surge does not use much power on top of the system network power consumption and does not drain your battery.

Q: What does "Skip proxy" option do?
> This option forces connections to these domain/IP ranges to be handled by Surge TUN, instead of Surge Proxy Server. This option is used to fix compatibility problems with some apps.
> 
> * To specify a single domain, enter the domain name - for example, apple.com.
> 
> * To specify all websites on a domain, use an asterisk before the domain name - for example, \*apple.com.
> 
> * To specify a specific part of a domain, specify each part - for example, store.apple.com.
> 
> * To specify hosts or networks by IP addresses, enter a specific IP address such as 192.168.2.11 or an address range, such as 192.168.2.\* or 192.168.2.0/24.
> 
> Notice: If you enter an IP address or address range, you will only be able to bypass the proxy when you connect to that host using that address, not when you connect to the host by a domain name that resolves to that address.

Q: What does “Force Remote DNS” option do?
> Surge always tries to resolve these domains in remote proxy server. This option is useful if some domains cannot be resolved by local DNS.
> 
> Notice: This option is only for Surge TUN interface. When a request is sent to Surge proxy server, Surge always tries to resolve the domain remotely if it matches a rule without DIRECT policy.
> 
