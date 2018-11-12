# Enhanced Mode

***Only Surge Mac supports this feature, from version 2.1.0***

Some applications may not obey the system proxy settings. Using enhanced mode can make all applications handled by Surge.

- Surge will setup a virtual network interface (VIF) and register as the default route. All DNS questions will get answers with a virtual IP in 198.18.0.0/15 block.

- Surge VIF can only process TCP, UDP and ICMP traffic. Only enable this feature when necessary.

- ICMP traffic can't be proxied. Surge VIF will return a response directly.


