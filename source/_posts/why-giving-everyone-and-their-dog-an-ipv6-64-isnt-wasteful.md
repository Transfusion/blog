---
title: Why giving everyone and their dog an IPv6 /64 isn't wasteful
url: 133.html
id: 133
categories:
  - Uncategorized
date: 2014-01-22 00:01:27
tags:
---

> [http://etherealmind.com/allocating-64-wasteful-ipv6-not/](http://etherealmind.com/allocating-64-wasteful-ipv6-not/) [http://tools.ietf.org/html/rfc6177](http://tools.ietf.org/html/rfc6177) RFC 3177 \[RFC3177\] called for a default end site IPv6 assignment size of /48. Subsequently, the Regional Internet Registries (RIRs) developed and adopted IPv6 address assignment and allocation policies consistent with the recommendations of RFC 3177 \[RIR-IPV6\]. In 2005, the RIRs began discussing IPv6 address assignment policy again. Since then, APNIC \[APNIC-ENDSITE\], ARIN \[ARIN-ENDSITE\], and RIPE \[RIPE-ENDSITE\] have revised the end site assignment policy to encourage the assignment of smaller (i.e., /56) blocks to end sites. This document obsoletes RFC 3177, updating its recommendations in the following ways: 1) It is no longer recommended that /128s be given out. While there may be some cases where assigning only a single address may be justified, a site, by definition, implies multiple subnets and multiple devices.

> While it seems likely that the size of a typical home network will grow over the next few decades, it is hard to argue that home sites will make use of 65K subnets within the foreseeable future.

[http://keepingitclassless.net/2013/02/assigning-ipv6-prefixes-for-customer/](http://keepingitclassless.net/2013/02/assigning-ipv6-prefixes-for-customer/) IPv6 was designed with networks in mind. We have to think in terms of prefixes, instead of individual IP addresses. A /64 is the "base unit", 1 network. [http://www.ripe.net/internet-coordination/press-centre/understanding-ip-addressing](http://www.ripe.net/internet-coordination/press-centre/understanding-ip-addressing)

> With a /56, we may have 4.7 sextillion addresses, but only a mere 256 networks, if this /64 mentality is to be held true. 256 is not a lot, folks, not for small to medium customers, and not nearly enough for large customers, and service providers, such as cloud providers.