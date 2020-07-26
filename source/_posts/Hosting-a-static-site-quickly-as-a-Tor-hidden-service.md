title: Hosting a static site quickly as a Tor hidden service with docker-compose
author: Transfusion
categories:
  - - Programming
  - - Unix
date: 2020-07-26 18:08:03
tags:
---

This sample bakes a private key into the resulting docker image that contains the Tor daemon. The only thing you need to edit are `args` and `volumes` in `docker-compose.yml`.

`docker-compose.yml`:
```
version: "3"
services:
  hidden_service:
    # we want to pass in the details of our hs AT BUILD TIME..
    build: 
      context: .
      dockerfile: Dockerfile.hidden_service
      args:
        TARGET_PORT: 8123
        ONION_HOSTNAME: abcdefghijklmnop.onion
        ONION_PRIVATE_KEY: -----BEGIN RSA PRIVATE KEY-----\nMIIC[REDACTED]\n...\n...\n-----END RSA PRIVATE KEY-----
    restart: always


  web_host:
    image: nginx:alpine

    volumes:
      - "~/my/static_site:/usr/share/nginx/html"
    ports:
      - "8123:80"

    restart: always
```

`ONION_PRIVATE_KEY` is what belongs in `/var/lib/tor/hidden_service/private_key`, `ONION_HOSTNAME` is what belongs in `/var/lib/tor/hidden_service/hostname`.
 
`Dockerfile.hidden_service`
```
FROM alpine:latest

ARG TARGET_PORT
ARG ONION_HOSTNAME
ARG ONION_PRIVATE_KEY

RUN apk update && apk add bind-tools && apk add curl && apk add \
    tor \
    --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ \
    && rm -rf /var/cache/apk/*

EXPOSE 9050

RUN mkdir -p /etc/tor
RUN chown -R tor /etc/tor

RUN echo $'HiddenServiceDir /var/lib/tor/hidden_service \n\
HiddenServicePort 80 web_host:80' > /etc/tor/torrc

run mkdir -p /var/lib/tor/hidden_service
run chmod 700 /var/lib/tor/hidden_service

RUN echo -e $ONION_PRIVATE_KEY > /var/lib/tor/hidden_service/private_key
# RUN cat /var/lib/tor/hidden_service/private_key
RUN chmod 600 /var/lib/tor/hidden_service/private_key

RUN echo ${ONION_HOSTNAME} > /var/lib/tor/hidden_service/hostname

run chown -R tor /var/lib/tor/hidden_service

USER tor
ENTRYPOINT [ "tor" ]
CMD [ "-f", "/etc/tor/torrc" ]
```

`Dockerfile.web_host`
```
FROM nginx:alpine
```

Copy these three into a folder, then do `docker-compose up` from within said folder.