# Policy Group

A policy group may contain multiple policies. It can be a proxy policy, another policy group or a built-in policy \(DIRECT and REJECT\).

There are three group types: ‘select‘, ’url-test‘, ’fallback‘, ’load-balance‘ and ’ssid‘. Section \[Proxy Group\] declares policy group.

## Manual Select Group

Select which policy will be used on the user interface.

`SelectGroup = select, ProxyHTTP, ProxyHTTPS, DIRECT, REJECT`

> In iOS version. You may use Today Widget to quickly switch policy for the first 'select' group. 
> In macOS version. You may switch the policy in the menubar menu.

## Auto URL Test Group

Automatically select which policy will be used by benchmarking the latency to the testing URL. You change the testing URL in the general settings, or override the testing URL for a policy.

`AutoTestGroup = url-test, ProxySOCKS5, ProxySOCKS5TLS`

### Parameters

#### interval: Optional, second \(Default: 600s\).

The benchmark result will be discarded after the interval time. A retest will happen if the policy group is used.

#### tolerance: Optional, millisecond \(Default: 100ms\).

Policy will be changed only when the new winner has a higher score than the old winner's score plus the tolerance.

#### timeout: Optional, second \(Default: 5s\).

Abandon a policy if not finished in timeout.

## Fallback Group

Select an available policy by priority. The availability is tested by accessing a URL, just like an auto URL test group. The policy defined in the front has a high priority.

`FallbackGroup = fallback, ProxySOCKS5, ProxySOCKS5TLS`

### Parameters

#### interval: Optional, s \(Default: 600s\).

Determine how long the benchmark result will be discarded.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if it is not finished until timeout.

## Load Balance Group

A load-balancing group is randomly selected from the sub-policies to use.

When the url parameter is configured, availability is checked against the behavior of the fallback group and then only a random selection is made from the available sub-policies.

In addition to the url, timeout, and interval, there is one other parameter.


### Parameters

#### persistent: Optional

When persistent=true, the same policy will be used as much as possible for the same target hostname. Avoid triggering risk controls on the target site due to different egress IPs. However, a policy change may occur when availability changes.


## SSID Group

Although still called the SSID Policy Group, it has been expanded to include the ability to select sub-policies based on the current network’s SSID, BSSID, routed IP address, etc. The iOS version can also specify policies for data networks.

`SSIDGroup = ssid, default = ProxyHTTP, cellular = ProxyHTTP, SSIDName = ProxySOCKS5`

### Parameters

#### default: Required

The policy when no matched SSID option has been found.

#### cellular: Optional

The policy under cellular network. If not provided, the default policy will be used.

## External Group

Starts from Surge Mac v3.0 and Surge iOS v3.4. A policy group may import policies defined in an external file or from a URL.

`egroup = select, policy-path=proxies.txt`

This file contains a list of policies, just like the definition lines in the main profile

```
Proxy-A = https, example1.com, 443
Proxy-B = https, example2.com, 443
```

#### update-interval: Optional, second

The update interval if the path is a URL.

#### policy-regex-filter: Optional

Only use the lines in the external file that the regex matches.

## Other Common Parameters

#### no-alert

Do not show the policy change notification for this group.

#### hidden

Do not show the group in the menu (Surge Mac) and the policy selection view (Surge iOS).


