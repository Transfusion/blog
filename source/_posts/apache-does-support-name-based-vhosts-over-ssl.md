title: Apache does support name-based vhosts over SSL.
url: 70.html
id: 70
categories:
  - Uncategorized
date: 2013-11-05 21:30:58
tags:
---
http://httpd.apache.org/docs/2.2/ssl/ssl_faq.html#vhosts

> Name-Based Virtual Hosting is a very popular method of identifying different virtual hosts. It allows you to use the same IP address and the same port number for many different sites. When people move on to SSL, it seems natural to assume that the same method can be used to have lots of different SSL virtual hosts on the same server. **It is possible, but only if using a 2.2.12 or later web server, built with 0.9.8j or later OpenSSL.** This is because it requires a feature that only the most recent revisions of the SSL specification added, called Server Name Indication (SNI).

http://www.codealpha.net/631/name-based-virtual-hosts-with-ssl-using-apache2-on-ubuntu-lucid/