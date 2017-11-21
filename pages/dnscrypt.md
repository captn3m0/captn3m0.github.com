---
layout: page
title: DNSCrypt
permalink: /dnscrypt/
---

I have a DNSCrypt server running out of a Digital Ocean droplet in BLR1 region. If you are within India, this might be a nice DNS server to use. Runs with DNSCrypt support, and uses [OpenDNS](https://use.opendns.com/) resolvers as the upstream.

This is currently considered to be in `alpha`, which means I don't take any guarantees for this and it can go down at any point. The server does not log anything for DNS queries. This is running on a small DO server, so I'd recommend using this only for personal machines.

Connection details are:

```
ProviderName    2.dnscrypt-cert.captnemo.in 
ProviderKey     053A:DFF2:C5A3:2916:D81A:D88A:6779:2C30:2BAA:D5D2:8032:95E8:5A9B:D22F:8687:1E10
ResolverAddress 139.59.48.222:4434
```

You can monitor the uptime of the same at [status.captnemo.in](https://status.captnemo.in/). The above IP is a floating IP (which means it won't change even after server restarts).

## CHANGELOG

2017-11-21
: Fixed Floating IP issues. Now UDP (default) works with Floating IPs

2017-10-04
: Launched to the public in `alpha`.

2017-08-13
: Initial setup. Running for personal use only.

For any other queries, please see my [contact page](/contact/).
