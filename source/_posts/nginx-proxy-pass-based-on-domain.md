---
title: nginx proxy_pass based on domain
date: 2017-12-22 15:23:51
tags:
	- Linux
---

Nginx supports multiple server blocks listening on the same port; this is how Virtual Hosts work; thus we simply `proxy_pass` virtual hosts to our desired target.

```nginx
server {
        listen  80;
        server_name soundcloud.com;

        location / {
                        proxy_pass http://soundcloud.com;
        }
}       
        
server {
        listen  80;
        server_name api.soundcloud.com;
        
        location / {
                        proxy_pass http://api.soundcloud.com;
        }
}
```

[https://stackoverflow.com/questions/21064401/route-different-proxy-based-on-subdomain-request-in-nginx](https://stackoverflow.com/questions/21064401/route-different-proxy-based-on-subdomain-request-in-nginx)