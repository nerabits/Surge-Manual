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


#### DOMAIN-SET

Designed for a large number of domain name list, supports fast search for thousands of records. Each line in the file is a domain name, if a line begins with . matches all sub-domains and the domain name itself. This can be used for ad filtering.

> The DOMAIN-SET rule doesn't support including an eTLD suffix due to performance optimization.
> 
> For example: .github.io won't match example.github.io
> 
> Here is the full eTLD list: https://publicsuffix.org/list/
> 
> Please use RULE-SET instead if you want to use eTLD as a suffix.


