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


