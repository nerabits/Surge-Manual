# 子网设置

您可以使用 [子网表达式](../rule/subnet.md) 以匹配指定的网络，并应用特定的设置。

> 出于兼容性的考虑。配置文件中的子网设置部分的名称为 [SSID Setting]。

### 临时禁用

在连接到指定网络时，自动禁用 Surge。

```
[SSID Setting]
SSID:MyHome suspend=true
```

### 蜂窝网络回落（仅限 iOS）

在特定 Wi-Fi 网络下，控制增强版 Wi-Fi 助理和混合网络的行为。

```
[SSID Setting]
SSID:MyHome cellular-fallback=off
```

- cellular-fallback=default 
  使用增强版 Wi-Fi 助理和混合网络默认设置。
- cellular-fallback=off
  在指定网络下开启增强版 Wi-Fi 助理和混合网络设置。
- cellular-fallback=hybrid 
  在指定网络下关闭增强版 Wi-Fi 助理和混合网络设置。
- cellular-fallback=wifi-assist
  在指定网络下开启增强版 Wi-Fi 助理。

### TCP Fast Open 行为

```
[SSID Setting]
SSID:MyHome tfo-behaviour=force-enabled
```

- tfo-behaviour=auto
  使用默认 TFO 设置。
- tfo-behaviour=force-disabled
  在指定网络下完全关闭 TFO。
- tfo-behaviour=force-enabled
  在特定网络下强制开启 TFO。此选项将允许 Surge 忽略系统 TFO 黑洞检测机制。

### DNS 覆盖

在特定网络中覆盖 DNS 设置。

```
[SSID Setting]
SSID:MyHome dns-server=8.8.8.8,encrypted-dns-server=https://1.1.1.1/
```

若已在全局设置中配置加密 DNS，则必须在此处显式使用关键字 `off` 来使用传统 DNS。

```
[SSID Setting]
SSID:MyHome dns-server=8.8.8.8,encrypted-dns-server=off
```
