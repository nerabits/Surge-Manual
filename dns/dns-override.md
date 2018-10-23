# DNS Server

You can use this option to override system's DNS setting.

```
[General]
dns-server = 8.8.8.8, 8.8.4.4
```

Use keyword 'system' to append additional DNS servers to system's setting. (Duplicate servers will be ignored)

```
[General]
dns-server = system, 8.8.8.8, 8.8.4.4
```
