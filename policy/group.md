# Policy Group

A policy group may contain multiple policies. It can be a proxy policy, another policy group or a built-in policy \(DIRECT and REJECT\).

There are three group types: ‘select‘, ’url-test‘ and ’ssid‘. Section \[Proxy Group\] declares policy group.

## Manual Select Group

Select which policy will be used on the user interface.

`SelectGroup = select, ProxyHTTP, ProxyHTTPS, DIRECT, REJECT`

> In iOS version. You may use Today Widget to quickly switch policy for the first 'select' group. 
> In macOS version. You may switch the policy in the menubar menu.

## Auto URL Test Group

Automatically select which policy will be used by benchmarking the latency to a URL.

`AutoTestGroup = url-test, ProxySOCKS5, ProxySOCKS5TLS, url = http://www.google.com/generate_204`

### Parameters

#### url: Required

Surge will send an HTTP HEAD request to the URL. The test only cares about whether receiving a response data, even if the response is an HTTP error.

#### interval: Optional, s \(Default: 600s\).

The benchmark result will be discarded after the interval time. A retest will happen if the policy group is used.

#### tolerance: Optional, ms \(Default: 100ms\).

Policy will be changed only when the new winner has a higher score than the old winner's score plus the tolerance.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if not finished in timeout.



## Fallback Group

Select an available policy by priority. The availability is tested by accessing a URL, just like an auto URL test group. The policy defined in the front has a high priority.

`FallbackGroup = fallback, ProxySOCKS5, ProxySOCKS5TLS, url = http://www.google.com/generate_204`

### Parameters

#### url: Required

Specify which URL will be tested.

#### interval: Optional, s \(Default: 600s\).

Determine how long the benchmark result will be discarded.

#### timeout: Optional, s \(Default: 5s\).

Abandon a policy if it is not finished until timeout.

## SSID Group

Select a policy according to the current Wi-Fi SSID.

`SSIDGroup = ssid, default = ProxyHTTP, cellular = ProxyHTTP, SSIDName = ProxySOCKS5`

### Parameters

#### default: Required.

The policy when no matched SSID option has been found.

#### cellular: Optional.

The policy under cellular network. If not provided, the default policy will be used.

## External Group

Starts from Surge Mac v3.0 and Surge iOS v3.4. A policy group may import policies defined in an external file or from a URL.

`egroup = select, policy-path=proxies.txt`

This file contains a list of policies, just like the definition lines in the main profile

```
Proxy-A = https, example1.com, 443
Proxy-B = https, example2.com, 443
```


