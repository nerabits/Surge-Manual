# External Controller Access

Surge can be managed from a remote machine using tools like Surge Dashboard or Surge CLI. However, the function needs to be manually enabled.

```
[General]
external-controller-access = apassword@127.0.0.1:8888
```

This parameter is made up of three parts: password, listen address, and port number, and it's important to note that no part can be omitted. 

When using this function on Surge iOS, listening on 127.0.0.1 means that only connections from a USB cable will be allowed. However, listening on 0.0.0.0 means that connections from the local Wi-Fi network will also be allowed.  Connection from a cellular network will always be restricted due to security considerations.