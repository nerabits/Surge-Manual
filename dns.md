# DNS

Surge uses a customized DNS client to support advanced features. It may behave differently from the DNS client of your operating system.

### Upstream DNS Server

Surge uses the DNS server addresses from the operating system by default. You can override them using ['dns-server'](/dns-override.md) option.

### Details

Surge simultaneously queries all DNS servers to improve performance, similar to dnsmasq with '--all-servers' parameter. The first answer from servers will be used. Surge iOS app and Surge Dashboard will show which server responds first. If Surge has not received any answer in 2 seconds, it will query all servers again. After 4 retries, Surge will give up and report DNS error.

Some domain names may have poorly-performing authoritative name servers, causing upstream DNS servers to return empty answers due to server-side timeout or other connectivity issues. Surge will report empty DNS error if **all** upstream DNS servers explicitly return empty DNS answers, or if some servers return empty answers and others fail to respond in 2 seconds.

When IPv6 is available and enabled, Surge DNS client will send both A and AAAA questions to upstream DNS Servers. The first A or AAAA answer returned will be used.


