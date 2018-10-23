# Policy Group

A policy group may contain multiple policies. It can be a proxy policy, another policy group or a built-in policy \(DIRECT and REJECT\).

There are three group types: ‘select‘, ’url-test‘ and ’ssid‘. Section \[Proxy Group\] declares policy group.

## Manaully Select Group

Select which policy will be used on the user interface.

`SelectGroup = select, ProxyHTTP, ProxyHTTPS, DIRECT, REJECT`

> In iOS version. You can use Today Widget to quickly select policy for the first 'select' group. You can enable/disable this feature in 'More' tab.

## Auto URL Test Group

Automatically select which policy will be used by benchmarking the latency to an URL.

`AutoTestGroup = url-test, ProxySOCKS5, ProxySOCKS5TLS, url = http://www.google.com/generate_204`

### Parameters

#### url: Required

Surge will send a HTTP HEAD request to the URL. The test only cares about whether receiving a response data, even if the response is a HTTP error.

#### interval: Optional, s \(Default: 600s\).

The benchmark result will be discarded after the interval time. A retest will happen if the policy group is used.

#### tolerance: Optional, ms \(Default: 100ms\).

Policy will be changed only when the new winner has a higher score than the old winner's score plus the tolerance.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if not finished in timeout.



## Fallback Group

Select an available policy by priority. The availability is tested by accessing an URL, just like an auto URL test group.

`FallbackGroup = fallback, ProxySOCKS5, ProxySOCKS5TLS, url = http://www.google.com/generate_204`

### Parameters

#### url: Required

Specify which URL will be tested.

#### interval: Optional, s \(Default: 600s\).

Determine how long the benchmark result will be discarded.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if it is not finished until timeout.

## SSID Group

Select which policy will be used according to the current Wi-FI SSID.

`SSIDGroup = ssid, default = ProxyHTTP, cellular = ProxyHTTP, SSIDName = ProxySOCKS5`

### Parameters

#### default: Required.

The policy when no matched SSID option has been found.

#### cellular: Optional.

The policy under cellular network. If not provided, the default policy will be used.

