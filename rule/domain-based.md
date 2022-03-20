# 域名规则

域名规则有三个类型。

#### DOMAIN

`DOMAIN,www.apple.com,Proxy`

此规则用于完全匹配请求的域名。

#### DOMAIN-SUFFIX

`DOMAIN-SUFFIX,apple.com,Proxy`

此规则用于匹配对应请求的域名后缀。例如："google.com" 匹配 www.google.com mail.google.com和 "google.com"，但不***匹配*** "content-google.com"。

#### DOMAIN-KEYWORD

`DOMAIN-KEYWORD,google,Proxy`

如果请求的域名包含该关键词，则规则匹配。


#### DOMAIN-SET

专为大量的域名列表设计，支持快速搜索数千条记录。文件中的每一行都是一个域名，如果某一行以.开头，则匹配所有子域名和域名本身。此规则可用于广告过滤。

> 由于性能优化，DOMAIN-SET 规则不支持 eTLD 后缀。
> 
> 例如：.github.io不会匹配 example.github.io。
> 
> 以下是完整的 eTLD 列表： https://publicsuffix.org/list/
> 
> 如果你想使用 eTLD 作为后缀，请使用 RULE-SET 代替。


