---
layout: page
title: DNSCrypt
permalink: /dnscrypt/
---

I have a DNSCrypt server running out of a Digital Ocean droplet in BLR1 region. If you are within India, this might be a nice DNS server to use. Runs with DNSCrypt support, and uses [OpenDNS](https://use.opendns.com/) resolvers as the upstream.

This is currently considered to be in `beta`, which means I'll try my very best to keep it running at all times. The server does not log anything for DNS queries. This is running on a small DO server, so I'd recommend using this only for personal machines (and not enterprise setups).

Connection details are:

```
ProviderName    2.dnscrypt-cert.captnemo.in
ProviderKey     053A:DFF2:C5A3:2916:D81A:D88A:6779:2C30:2BAA:D5D2:8032:95E8:5A9B:D22F:8687:1E10
ResolverAddress 139.59.48.222:4434
```

You can monitor the uptime of the same at [status.captnemo.in](https://status.captnemo.in/). The above IP is a floating IP (which means it won't change even after server restarts).

The server is running dnscrypt-wrapper `v0.3`.

## Warning

By using this service you take full responsibility. If this puts your computer on fire, I'm not responsible!

## CHANGELOG

2017-12-10
: Now added to the official DNSCrypt resolver list. (Only one running in India). [[csv](https://github.com/DNSCrypt/dnscrypt-resolvers/blob/master/v1/dnscrypt-resolvers.csv)], [[announcement](https://twitter.com/captn3m0/status/939568861828997120)]

2017-12-06
: Server stability changed to `beta`.

2017-11-21
: Fixed Floating IP issues. Now UDP (default) works with Floating IPs

2017-10-04
: Launched to the public in `alpha`.

2017-08-13
: Initial setup. Running for personal use only.

For any other queries, please see my [contact page](/contact/).
