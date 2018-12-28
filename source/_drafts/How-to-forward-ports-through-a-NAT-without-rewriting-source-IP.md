title: How to forward ports through a NAT without rewriting source IP
author: Transfusion
date: 2018-02-11 13:27:47
tags:
---
Use case: You're exposing a service, say SSH, and in your logs (or `w`) all connection attempts show up as the IP of your router instead of the external machine. This comes up surprisingly often and I hope I nailed all the keywords :)

In OpenWRT/LEDE, 