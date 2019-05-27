---
layout: page
title: DNSCrypt
permalink: /dnscrypt/
---

I have a [DNSCrypt][dnscrypt] server running out of a Digital Ocean droplet in BLR1 region. If you are within India, this might be a nice DNS server to use. This is running on a small DigitalOcean server, so I'd recommend using this only for personal machines (and not enterprise setups).

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

The DNS Stamp is:

```
sdns://AQcAAAAAAAAAEjEzOS41OS40OC4yMjI6NDQzNCAFOt_yxaMpFtga2IpneSwwK6rV0oAyleham9IvhoceEBsyLmRuc2NyeXB0LWNlcnQuY2FwdG5lbW8uaW4
```

The server is running dnscrypt-wrapper `dnscrypt-server-docker` with [QNAME Minimization Enabled](https://github.com/captn3m0/dnscrypt-server-docker/commit/437cacc0b67784280c619c6f5922f872fc4ebe89).

## Uptime

This is currently considered `stable` for production use. It is expected to be up at all times aside for scheduled and emergency maintainence.

The total cumulative downtime for the service throughout 2019 (As of May 2019) is 10 minutes.

The [planned uptime is 99.99%](https://uptime.is/four-nines). There is no SLA provided, since this is a personal service.

You can monitor the uptime of the same at [status.captnemo.in](https://status.captnemo.in/).

## Privacy & Transparency

Please see [/dns/privacy](/dns/privacy) for the Privacy Policy, Transparency Guidelines, and Operating Principles of the resolver.

## Disclaimer

The service is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. in no event shall I be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.

## CHANGELOG

2019-05-28
: [Enabled QNAME Minimization](https://github.com/captn3m0/dnscrypt-server-docker/commit/437cacc0b67784280c619c6f5922f872fc4ebe89).

2019-05-18
: Switched to Docker with [automatic key rotation](https://captnemo.in/blog/2019/05/18/dnscrypt-migrating-to-docker/). No longer uses a Upstream resolver, and instead acts as a Recursive Resolver.

2019-05-12
: Resolver stability changed to `stable`. Published Draft policies.

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

[dnscrypt]: https://dnscrypt.info/ "DNSCrypt is a protocol that authenticates communications between a DNS client and a DNS resolver."
