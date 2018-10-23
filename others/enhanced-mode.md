# Enhanced Mode

***Only Surge Mac supports this feature, from version 2.1.0***

Some applications may not obey the system proxy settings. Using enhanced mode can make all applications handled by Surge.

* Surge will setup a TUN interface and route 198.18.0.0/16 to it. All DNS questions will get an answer with a fake IP in 198.18.0.0/16 block. (This block is reserved for future use by IANA.)

* Surge TUN interface can only process TCP, UDP and ICMP traffic. Only use this feature when necessary.（UDP and ICMP traffic can't be proxied. It will passthrough like behind a NAT.）