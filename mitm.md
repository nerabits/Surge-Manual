# HTTPS Decryption (Man-in-the-Middle Attack, MitM)

Surge may decrypt HTTPS traffic by MitM. Please see [Wikipedia article](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for more information.

Certificate generator will help you generate a new CA certificate for debugging and make the certificate trusted by system. It's available in Surge Dashboard (Mac version) and Surge iOS Config Editor. This certificate is generated locally and will only be saved in your config file and system Keychain. The key of certificate is generated randomly using OpenSSL.

You can also use an existed CA certificate. Export the certificate to PKCS#12 format (.p12) with passphrase. Please note that the passphrase cannot be empty due to system limitation. Use "base64" command to encode in base64 string and append these settings below to your config file.


```
[MITM]
enable = true
ca-p12 = MIIJtQ.........
ca-passphrase = password
hostname = *google.com
```


Surge will only decrypt traffic to hosts which are declared in "hostname". Prefix wildcard \* is allowed. It uses the same wildcard rule as [Local DNS Mapping](dns/local-dns-mapping.md). Although you can use single \* to enable MitM to all requests, it's not recommended.


> Some applications has strict security policy to use pinned certificates or CA. Enabling decryption to these hosts may casue problems.
