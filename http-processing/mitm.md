# HTTPS Decryption (Man-in-the-Middle Attack, MitM)

Surge may decrypt HTTPS traffic by MitM. Please see [Wikipedia article](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) for more information.

The certificate generator can help you generate a new CA certificate for debugging and make the certificate trusted by the system. It's available in Surge Dashboard (Mac version) and Surge iOS Config Editor. This certificate is generated locally and only saved in your profile file and the system Keychain. The key of the new certificate is generated randomly using OpenSSL.

You can also use an existing CA certificate. Export the certificate to PKCS#12 format (.p12) with a passphrase. Please note that the passphrase cannot be empty due to system limitations. Use the "base64" command to encode in the base64 string and append these settings below to your config file.


```
[MITM]
enable = true
ca-p12 = MIIJtQ.........
ca-passphrase = password
hostname = *google.com
h2 = true
```

Surge only decrypts traffic to hosts declared here.

- Wildcard characters * and ? are supported.
- Use prefix - to exclude a hostname.
- By default, only the requests to port 443 be decrypted.
  - Use suffix :port to allow other ports.
  - Use suffix :0 to allow all ports.

Example:
- `-*.apple.com`: Excludes all requests sent to *.apple.com on port 443.
- `www.google.com`: Allows MitM for www.google.com on port 443.
- `www.google.com:8080`: Allows MitM for www.google.com on port 8080.
- `www.google.com:0`: Allows MitM for www.google.com on all ports.
- `*:0`: Allows MitM for all hostnames on all ports. 

A general configuration may be like this:

`hostname = -*.apple.com, -*.icloud.com, *`

> Some applications have a strict security policy to use pinned certificates or CA. Enabling decryption to these hosts may cause problems.


## Options

### tcp-connection

By default, only connections that go through Surge HTTP proxy are decrypted with MITM. Enable the option to tell Surge to perform MITM on raw TCP connections that go through Surge VIF (Enhanced Mode). Please notice that you still need to fill in the hostnames on the list.

### skip-server-cert-verify

Do not verify the certificate of the remote host while performing MITM.

### h2

MITM over HTTP/2: Decrypt HTTPS traffic with MITM over HTTP/2 protocol, which can improve the performance of concurrent requests.

### client-source-address {{book.BETA}}

Use this parameter to enable the MITM function on some devices only.

  - It's a list parameter using commas as the separator.
  - You may specify a single IP address or use a CIDR block. Both IPv4 and IPv6 are supported.
  - You may use the `-` prefix to exclude some clients, e.g., `client-source-address = -192.168.1.2, 0.0.0.0/0`
  - If the parameter is not set, MITM is enabled for all clients. A equivalent to `client-source-address = 0.0.0.0/0, ::/0`
  - `127.0.0.1` should be included if you want to enable MITM for the current device.      


