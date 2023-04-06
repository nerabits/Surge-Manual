# Rule

Surge can forward requests to another proxy server or connect to the host directly, depending on customized rules. 

### Priority
Rules are matched from the first one to the last one, in the order they appear in the config file. In other words, rules at the top of the list have higher priority than the latter ones.

### Composition

Each rule consists 3 parts: rule type, a traffic matcher (except for the FINAL rule), and a proxy policy:
         TYPE,         VALUE,         POLICY
Example: DOMAIN-SUFFIX,apple.com,     DIRECT
         IP-CIDR,      192.168.0.0/16,ProxyA

Surge supports 6 different types of rules: DOMAIN, DOMAIN-SUFFIX, DOMAIN-KEYWORD, GEOIP, IP-CIDR, or FINAL. The proxy policy must be named under one of the policy names, including ‘a proxy’, 'a policy group', 'DIRECT', or 'REJECT'. Rules must end with a FINAL rule to define the default behavior.

Example:

```
[Rule]
DOMAIN-SUFFIX,company.com,ProxyA
DOMAIN-KEYWORD,google,DIRECT
GEOIP,US,DIRECT
IP-CIDR,192.168.0.0/16,DIRECT
FINAL,ProxyB
```

DOMAIN, DOMAIN-SUFFIX and DOMAIN-KEYWORD are [domain based rules](/rule/domain-based.md). IP-CIDR and GEOIP are [IP based rules](/rule/ip-based.md).

