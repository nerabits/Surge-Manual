# WireGuard

You can use Surge as a WireGuard client, converting L3 VPN as an outbound proxy policy.

```
[Proxy]
wireguard-home = wireguard, section-name = HomeServer

[WireGuard HomeServer]
private-key = sDEZLACT3zgNCS0CyClgcBC2eYROqYrwLT4wdtAJj3s=
self-ip = 10.0.2.2
dns-server = 223.5.5.5
mtu = 1280
peer = (public-key = fWO8XS9/nwUQcqnkfBpKeqIqbzclQ6EKP20Pgvzwclg=, allowed-ips = 0.0.0.0/0, endpoint = 192.168.20.6:51820)
```

Notes for configuration:

- All keys can be in base64 or HEX form.
- The self-ip field must be provided, please note that the self-ip must be different for each device, otherwise it may cause IP preemption.
- ~~The peer field can be configured with multiple nodes, separated by commas, and indicated by () for one node.~~ Only one peer is supported in the current version.
- The endpoint of the peer can use a domain name. Please note that the resolution of the endpoint is done by the DNS resolver configured by the [General] section and is not related to the dns-server parameter in this paragraph.
- ~~The allowed-ips of 0.0.0.0/0 means that the policy can be used to access any address, or it can be configured for a specific intranet address.~~ allowed-ips has no effect in the current version.
- If you need to access a host using a domain name through this policy, you must configure the dns-server, and Surge will perform DNS resolution to that server through the WireGuard's VPN tunnel. Multiple DNS addresses can be configured, separated by commas.
- The [WireGuard NAME] segment can be split into a Detached Profile Section file.
- Multiple Wireguard instances can be configured and used simultaneously.
- Wireguard policies can be used as an underlying-proxy for other policies, but configuring an underlying-proxy for wireguard policies is not supported.

Usage Notes:

- WireGuard is an L3 VPN, so the overhead during processing is significantly higher than other general proxy protocols. It is suitable for scenarios with low bandwidth requirements.
- The tunnel only supports TCP and UDP protocol. In addition, a very simple ICMP response mechanism is provided, when WireGuard handshake is successful, you can ping the client tunnel IP from the server-side to test the connectivity.
- Since WireGuard protocol itself has no error reporting mechanism, in most cases, WireGuard policy errors are timeouts (e.g., wrong key, firewall blocking, not configuring server-side NAT, etc.), so please analyze the cause by grabbing packets yourself.

