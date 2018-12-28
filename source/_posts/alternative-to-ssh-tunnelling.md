title: Alternative to SSH tunnelling
url: 124.html
id: 124
categories:
  - Security
date: 2014-01-09 15:38:47
tags:
---
[https://wido.me/sunteya/setup-a-socks-proxy-server-pass-by-secure-firewall/](https://wido.me/sunteya/setup-a-socks-proxy-server-pass-by-secure-firewall/) [http://www.bock.nu/blog/secure-firewall-bypass-danted-stunnel](http://www.bock.nu/blog/secure-firewall-bypass-danted-stunnel) SSH Tunneling is TCP over TCP over a single connection. Rather unreliable. Socks can handle multiple connections in a non-blocking fashion. Also, to give you security on par with SSH, make sure to use AES256 somewhere in your cipher chain;

```bash
transfusion@shell:~$ openssl ciphers -v -tls1 | grep 'AES(256)'
ECDHE-RSA-AES256-SHA384 TLSv1.2 Kx=ECDH     Au=RSA  Enc=AES(256)  Mac=SHA384
ECDHE-ECDSA-AES256-SHA384 TLSv1.2 Kx=ECDH     Au=ECDSA Enc=AES(256)  Mac=SHA384
ECDHE-RSA-AES256-SHA    SSLv3 Kx=ECDH     Au=RSA  Enc=AES(256)  Mac=SHA1
ECDHE-ECDSA-AES256-SHA  SSLv3 Kx=ECDH     Au=ECDSA Enc=AES(256)  Mac=SHA1
SRP-DSS-AES-256-CBC-SHA SSLv3 Kx=SRP      Au=DSS  Enc=AES(256)  Mac=SHA1
SRP-RSA-AES-256-CBC-SHA SSLv3 Kx=SRP      Au=RSA  Enc=AES(256)  Mac=SHA1
DHE-RSA-AES256-SHA256   TLSv1.2 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA256
```

Alternatively, if you're not sure what to use ,

```bash
options = NO_SSLv2
ciphers = HIGH:MEDIUM
```

in your stunnel.conf should suffice.