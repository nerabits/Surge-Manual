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

