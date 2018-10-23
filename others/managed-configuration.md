# Managed Configuration

Surge can update a config file from an URL automatically. If the config starts with

`#!MANAGED-CONFIG http://test.com/surge.conf interval=60 strict=true`

The config can only be updated when Surge main application is running.

> Note: The new config in remote should also contain #!MANAGED-CONFIG line. Otherwise this config will become a regular one.

### Parameters
   
#### interval: Optional, s (Default: 86400s).
Determine how long the config will be updated.

#### strict: true or false (Default: false).

If strict is true, Surge will require a force update after the interval arrives. Otherwise if the update fails the user may still use the outdated config.

> Note: Even when strict is true, the user still can start Surge by widget or VPN switch in Settings.
