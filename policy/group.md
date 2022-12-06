# Policy Group

A policy group may contain multiple policies. It can be a proxy policy, another policy group, or a built-in policy \(DIRECT and REJECT\).

There are several group types: `select`, `url-test`, `fallback`, `load-balance` and `subnet`. Policy groups should be declared in section \[Proxy Group\].

## Manual Select Group

Select which policy will be used on the user interface.

`SelectGroup = select, ProxyHTTP, ProxyHTTPS, DIRECT, REJECT`

{% hint style='info' %}
In Surge iOS. You may use the Today Widget to quickly switch the policy for the first 'select' group. <br />

In Surge Mac. You may switch the policy in the menubar menu.
{% endhint %}


## Auto URL Test Group

Automatically select which policy will be used by benchmarking the latency to the testing URL. You change the testing URL in the general settings or override the testing URL for a policy.

`AutoTestGroup = url-test, ProxySOCKS5, ProxySOCKS5TLS`

### Parameters

#### interval: Optional, second \(Default: 600s\).

The benchmark result will be discarded after the interval time. A retest will happen if the policy group is used.

#### tolerance: Optional, millisecond \(Default: 100ms\).

The policy will be changed only when the new winner has a higher score than the old winner's score plus the tolerance.

This option prevents policies with similar scores from constantly alternating.

#### timeout: Optional, second \(Default: 5s\).

Abandon a policy if not finished in timeout.

## Fallback Group

Select an available policy by priority and availability. The availability is tested by accessing a URL, just like an auto URL test group. The policy defined in the front has a high priority.

`FallbackGroup = fallback, ProxySOCKS5, ProxySOCKS5TLS`

### Parameters

#### interval: Optional, s \(Default: 600s\).

Determine how long the benchmark result will be discarded.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if it is not finished until timeout.

## Load Balance Group

A load-balancing group randomly selects a policy from the available sub-policies to use.

### Parameters

#### persistent: Optional

When persistent=true, the same policy will be used for the same target hostname. Avoid triggering risk controls on the target site due to different egress IPs. However, a policy change may occur when availability changes.


## Subnet Group

Starting from Surge iOS 4.12.0 & Surge Mac 4.5.0. The SSID group is now renamed to Subnet Group. You can use [subnet expression](../rule/subnet.md) as a condition.

`Subnet Group = subnet, default = ProxyHTTP, TYPE:WIFI = ProxyHTTP, SSID:MyHome = ProxySOCKS5`

The legacy syntax of SSID Group is still supported. You may use the group type keyword `subnet` or `ssid` for compatibility.

### Parameters

#### default: Required

The policy when no subnet expression is matched.

#### cellular: Optional (Deprecated, use `TYPE:CELLULAR` instead)

The policy for cellular networks. If not provided, the default policy will be used.

## External Group

Starts from Surge Mac v3.0 and Surge iOS v3.4. A policy group may import policies defined in an external file or from a URL.

`egroup = select, policy-path=proxies.txt`

This file contains a list of policies, just like the definition lines in the main profile.

```
Proxy-A = https, example1.com, 443
Proxy-B = https, example2.com, 443
```

#### update-interval: Optional, second

The update interval if the path is a URL.

#### policy-regex-filter: Optional

Only use the policies in the external file that the regex matches the policy name.

## Other Common Parameters

#### no-alert

Do not show the policy change notification for this group.

#### hidden

Do not show the group in the menu (Surge Mac) and the policy selection view (Surge iOS).


## Policy Including

Starting from Surge iOS 4.12.0 & Surge Mac 4.5.0, you can use `include-all-proxies` and `include-other-group` to include all proxies or reuse defines from another group.

#### include-all-proxies

The parameter `include-all-proxies=true` includes all proxy policies defined in the [Proxy] section and can be used with the `policy-regex-filter` parameter for filtering.

#### include-other-group

Parameter `include-other-group="group1,group2"` includes policies from another policy group, and can include multiple policy groups separated by commas, also can be used with the `policy-regex-filter` parameter for filtering.

Some Notes:
- `include-all-proxies`, `include-other-group`, and `policy-path` parameters are allowed to be used in a single policy group at the same time. The policy-regex-filter parameter applies to all three.
- There is an order of precedence among the policy groups for the `include-other-group` parameter, but there is no order of precedence among the `include-all-proxies`, `include-other-group`, and `policy-path` parameters. For scenarios where the order of sub-policies makes sense (e.g., fallback groups), use policy groups nesting with `include-other-group`.


