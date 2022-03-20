# DNS 服务器

你可以使用此选项来覆盖系统的 DNS 设置。

```
[General]
dns-server = 8.8.8.8, 8.8.4.4
```

关键字 'system' 可用于在系统配置中添加额外的 DNS 服务器（重复的服务器将被忽略）。

```
[General]
dns-server = system, 8.8.8.8, 8.8.4.4
```

### 


