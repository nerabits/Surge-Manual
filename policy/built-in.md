# Built-in Policy

There are two built-in policies: DIRECT and REJECT. DIRECT means the request should be sent to the host directly. REJECT means the request should be rejected.

DIRECT and REJECT can be used in rule and policy group directly. You can also define an alias in the proxy section.

### Alias

```
[Proxy]
On = direct
Off = reject
```

Then you can use 'On' and 'Off' as a policy name in rule and policy group.

#### Interface Option

Direct policy alias supports 'interface' parameter like a proxy policy.

```
[Proxy]
Crop-VPN = direct, interface = utun0
WiFi = direct, interface = en2, allow-other-interface=true
```

Please make sure the interface has a valid route table for the destination address.

'allow-other-interface=true' means when the desired interface is not available, Surge is allowed to use another interface to setup the connection. Otherwise the connection will fail directly.