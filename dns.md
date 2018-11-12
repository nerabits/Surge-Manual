# DNS

To implement complex DNS features, Surge has its own DNS client implementation. It may perform different behaviors to system DNS implementation.

### Upstream DNS Server

By default, Surge uses system's DNS server address settings. You may override it using ['dns-server'](/dns-override.md) option.

### Details

To boost performance Surge will send DNS query to all DNS servers simultaneously, just like dnsmasq with '--all-servers' parameter.  The first answer from servers will be used. Surge iOS app and Surge Dashboard will show which server responds first.

If Surge has not received answer from any server in 2 seconds, it will resend the question to all servers again. After 4 times retries, Surge will stop lookup and report a DNS error.

Some domain may have a poor NS server, so that the DNS server may return an empty answer due to server-side timeout or other connectivity issues. Surge will report an empty DNS error, if **all** servers return explicit empty answers, or some servers return empty answers and the others have not responded in 2 seconds.

When IPv6 is available and enabled, Surge DNS client will send A and AAAA questions to upstream DNS Server. In current version, which answer will be used depends on which answer returns first.


