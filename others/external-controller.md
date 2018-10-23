# External Controller Access

Surge can be managed from remote machine by tools like Surge Dashbaord or Surge CLI. You need to manually enable this function.


```
[General]
external-controller-access = apassword@127.0.0.1:8888
```

This parameter consists three parts: password, listen address and port number. No part can be omitted.

When you use this function in Surge iOS, listening on 127.0.0.1 means only connections from USB cable will be allowed. Listening on 0.0.0.0 means connections from local Wi-Fi network will also be allowed. Connection from cellular network will always be restricted due to a security consideration.
