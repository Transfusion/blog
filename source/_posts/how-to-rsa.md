title: How I understand RSA
url: 389.html
id: 389
categories:
- [Math]
- [Musings]
- [Programming]
- [Security]
date: 2014-06-12 03:58:58
tags:
---
[![wpid-wp-1402514522645-1024x735.jpeg](/wp-content/uploads/2014/06/wpid-wp-1402514522645-300x215.jpeg)](/wp-content/uploads/2014/06/wpid-wp-1402514522645-1024x735.jpeg) Euler's totient function is defined as the number of positive integers relatively prime to n (including 1). E.g. φ(12) = 4 ( **1**, 2, 3, 4, **5**, 6, **7**, 8, 9, 10, **11**, 12), and φ(15) = 8. [ http://www.thescienceforum.com/mathematics/14111-modular-multiplicative-inverse-context-rsa.html]( http://www.thescienceforum.com/mathematics/14111-modular-multiplicative-inverse-context-rsa.html) [https://en.wikibooks.org/wiki/Algorithm_Implementation/Mathematics/Extended_Euclidean_algorithm](https://en.wikibooks.org/wiki/Algorithm_Implementation/Mathematics/Extended_Euclidean_algorithm) [https://docs.google.com/viewer?url=www.math.utah.edu/~fguevara/ACCESS2013/Euclid.pdf](https://docs.google.com/viewer?url=www.math.utah.edu/~fguevara/ACCESS2013/Euclid.pdf) as to why the extended Euclid's algo can be used to find the modular multiplicative inverse [![wpid-wp-1402514649564-1024x767.jpeg](/wp-content/uploads/2014/06/wpid-wp-1402514649564-300x224.jpeg)](/wp-content/uploads/2014/06/wpid-wp-1402514649564-1024x767.jpeg) [![wpid-wp-1402514730357-1024x491.jpeg](/wp-content/uploads/2014/06/wpid-wp-1402514730357-300x143.jpeg)](/wp-content/uploads/2014/06/wpid-wp-1402514730357-1024x491.jpeg) [https://docs.google.com/viewer?url=ftp://ftp.rsasecurity.com/pub/pkcs/pkcs-1/pkcs-1v2-1.pdf](https://docs.google.com/viewer?url=ftp://ftp.rsasecurity.com/pub/pkcs/pkcs-1/pkcs-1v2-1.pdf) [https://docs.google.com/viewer?url=ftp://ftp.rsasecurity.com/pub/rsalabs/rsa_algorithm/rsa-oaep_spec.pdf](https://docs.google.com/viewer?url=ftp://ftp.rsasecurity.com/pub/rsalabs/rsa_algorithm/rsa-oaep_spec.pdf) In particular, ^ page 9. OAEP is the padding scheme ( [http://crypto.stackexchange.com/questions/10145/rsa-pcks1-v2-1-rsaes-oaep-algorithm](http://crypto.stackexchange.com/questions/10145/rsa-pcks1-v2-1-rsaes-oaep-algorithm) [http://crypto.stackexchange.com/questions/2074/rsa-oaep-input-parameters](http://crypto.stackexchange.com/questions/2074/rsa-oaep-input-parameters) ) , whereas I2OSP and OS2IP (on page 4); what really helped things come full circle for me is realizing how they represent arbitrary data as an integer (first converting it to an octet string). Without further do, let's test our generated keys by encrypting and decrypting the number 521 (any number smaller than 527, our modulus, will do. ( [http://stackoverflow.com/questions/10061626/message-length-restriction-in-rsa](http://stackoverflow.com/questions/10061626/message-length-restriction-in-rsa) ) )

```py
$ python
Python 2.7.5+ (default, Feb 27 2014, 19:37:08)
[GCC 4.8.1] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> print 521**41 % 527
346
>>> print 346**281 % 527
521
```
Note that if we try with a larger number...
```py
>>> print 1000**41 % 527
411
>>> print 411**281 % 527
473
```

Nope. What really helped things come full circle once again (or full sphere..) [http://en.wikipedia.org/wiki/Pretty_Good_Privacy#Confidentiality](http://en.wikipedia.org/wiki/Pretty_Good_Privacy#Confidentiality) [http://superuser.com/questions/383732/how-does-ssh-encryption-work](http://superuser.com/questions/383732/how-does-ssh-encryption-work) It makes more sense to use a symmetric encryption algorithm with high throughput to encrypt the data first, then use PKI to encrypt and transfer the key. And that is how the world works.
