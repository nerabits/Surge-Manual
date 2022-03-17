# Subnet Settings

You may use the [subnet expression](../rule/subnet.md) to match specified networks and apply particular settings. 

> For compatibility reasons. The subnet settings names [SSID Setting] in the profile.

### Suspend

Suspend Surge temporarily under specified networks.

```
[SSID Setting]
SSID:MyHome suspend=true
```

### Cellular Fallback (iOS Only)

Control the Wi-Fi assist and Hybrid Network Behaviour for specified Wi-Fi networks.

```
[SSID Setting]
SSID:MyHome cellular-fallback=off
```

- cellular-fallback=default 
  Use the global Wi-Fi assist and Hybrid Network settings.
- cellular-fallback=off
  Turn off Wi-Fi assist and Hybrid Network for the network.
- cellular-fallback=hybrid 
  Turn on Hybrid Network for the network.
- cellular-fallback=wifi-assist
  Turn on Wi-Fi assist for the network.

### TCP Fast Open Behaviour

```
[SSID Setting]
SSID:MyHome tfo-behaviour=force-enabled
```

- tfo-behaviour=auto
Use the default TFO behaviour.
- tfo-behaviour=force-disabled
Disable TFO for the network completely.
- tfo-behaviour=force-enabled
Forcibly enable TFO for the network. This option will make Surge ignore the system TFO blackhole detecting mechanism.


