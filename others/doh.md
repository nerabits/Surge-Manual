# DNS over HTTPS

If DNS-over-HTTPS is configured, the traditional DNS will only be used to test the connectivity and resolve the domain in the DOH URL.

### Use DoH for All Domains

```
[General]
doh-server = https://9.9.9.9/dns-query
```

You may specify multiple DNS-over-HTTPS servers here (not recommended).


### Use DoH for Specified Domains

```
[Host]
example.com = server:https://cloudflare-dns.com/dns-query
```


### DNS over HTTPS Format

There are two different types of DoH format: JSON and DNS wireformat (RFC1035).

You need to confirm the supported type of your DoH service.

* Surge iOS 4.1 and below versions / Surge Mac 3.4.1 and below versions: Only JSON format is supported.

* Surge iOS 4.2 and above versions / and Surge Mac 3.5.0 and above versions: Surge uses DNS wireformat by default. You can also choose to continue using JSON.

	```
	[General]
	doh-format=json
	```

### Use DoH with Proxy

If you want to query DoH servers through proxy, you can set doh-follow-outbound-mode to true.

```
[General]
doh-follow-outbound-mode=true
```

All the DoH connections will follow the outbound mode setttings. Then configure a rule for the DoH hostname to use a proxy.

Or, use `PROTOCOL,DOH` rule to match all DoH connections.


