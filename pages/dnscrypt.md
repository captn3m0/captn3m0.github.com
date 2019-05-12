---
layout: page
title: DNSCrypt
permalink: /dnscrypt/
---

I have a DNSCrypt server running out of a Digital Ocean droplet in BLR1 region. If you are within India, this might be a nice DNS server to use. Runs with DNSCrypt support (queries to upstream are encrypted), and uses [Quad9](https://www.quad9.net/) resolvers. This is running on a small DigitalOcean server, so I'd recommend using this only for personal machines (and not enterprise setups).

Connection details are:

```
ResolverName captnemo-in
```

Alternatively, if you don't have the resolver in your DNSCrypt version (it was added around Jan-2018), then you can use:

```
ProviderName    2.dnscrypt-cert.captnemo.in
ProviderKey     053A:DFF2:C5A3:2916:D81A:D88A:6779:2C30:2BAA:D5D2:8032:95E8:5A9B:D22F:8687:1E10
ResolverAddress 139.59.48.222:4434
```

The above IP is a Floating IP (which means it won't change even after server restarts or dies).

The server is running dnscrypt-wrapper `0.3-8.g625f311`.

## Uptime

This is currently considered to be in `stable`, this is expected to be up at all times aside for scheduled and emergency maintainence. The total cumulative downtime for the service throughout 2019 (As of May 2019) is 10 minutes.

The planned uptime is 99.99%. There is no SLA provided, since this is a personal service.

You can monitor the uptime of the same at [status.captnemo.in](https://status.captnemo.in/).

## Privacy & Transparency

Please see [/dns/privacy](/dns/privacy) for the Privacy Policy, Transparency Guidelines, and Operating Principles.

## Disclaimer

The service is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. in no event shall I be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.

## CHANGELOG

2019-05-12
: Resolver stability changed to `Stable`. Published Draft policies.

2018-09-19
: Upstream resolver changed to Quad9.

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
