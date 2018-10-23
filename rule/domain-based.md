# Domain-based Rule

There are 3 domain-based rule types.

#### DOMAIN

`DOMAIN,www.apple.com,Proxy`

Rule matches if the domain of request matches exactly.

#### DOMAIN-SUFFIX

`DOMAIN-SUFFIX,apple.com,Proxy`

Rule matches if the domain of the request matches the suffix. For example: 'google.com' matches 'www.google.com', 'mail.google.com' and 'google.com', but does **not** match 'content-google.com'.

#### DOMAIN-KEYWORD

`DOMAIN-KEYWORD,google,Proxy`

Rule matches if the domain of the request contains the keyword.


### Domain-based Rule Options

#### Option: force-remote-dns (Surge iOS Only)

```
DOMAIN,www.apple.com,Proxy,force-remote-dns
DOMAIN-SUFFIX,apple.com,Proxy,force-remote-dns
DOMAIN-KEYWORD,google,Proxy,force-remote-dns
```

When a raw TCP connection is handled by Surge TUN, the application will firstly try to resolve the domain, then send packets to the IP address directly. If the domain cannot be resolved locally, you can use this option to force the DNS resolution to happen remotely on the proxy.

Technically, when an application tries to resolve a domain which matches a rule with 'force-remote-dns' option, Surge will send a DNS answer with a fake IP address (240.1.x.x). When the application connects to the fake IP, Surge will remap it to a domain and send the request to the remote proxy.

> Notice: This option only works for Surge TUN (only exists in Surge iOS). Request handled by Surge Proxy will always be resolved remotely if the rule's policy is a proxy.
