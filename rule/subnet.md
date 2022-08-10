# Subnet Rule

### Subnet Expression

A subnet expression can be one of these:
  - Use SSID:value to match the Wi-Fi SSID, wildcard character is allowed.
  - Use BSSID:value to match the Wi-Fi BSSID, wildcard character is allowed.
  - Use ROUTER:value to match the router IP address.
  - Use TYPE:WIFI to match all Wi-Fi networks.
  - Use TYPE:WIRED to match all wired networks.
  - Use TYPE:CELLULAR to match all cellular networks.
  - Use MCCMNC:100-200 to match a cellular network
  - If no prefix is provided, it tries to match SSID/BSSID/Router for the legacy version compatibility.



#### SUBNET

Rule matches if the subnet expression matches.

```
SUBNET,TYPE:WIRED,DIRECT
SUBNET,SSID:MyHome,Proxy
```


