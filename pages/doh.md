---
layout: page
title: DoH Server
permalink: /doh/
---

Alongside my [DNSCrypt Server](/dnscrypt/), I'm also running a [DoH (DNS Over HTTPS)][doh] Server at [doh.captnemo.in](https://doh.captnemo.in). The IP Address for the server is `139.59.48.222`, and is expected to never change.

## Usage

### Firefox

1.  Load `about:config` in the Firefox address bar.
2.  Confirm that you will be careful if the warning page is displayed.
3.  Search for network.trr.mode and double-click on the name.
    -   Set the value to 2 to make DNS Over HTTPS the browser's first choice but use regular DNS as a fallback. This is the optimal setting for compatibility.
    -   You can set it to 1 to let Firefox pick whichever is faster, 3 for TRR only mode, or 0 to disable it.
    -   Since my DoH service is in `beta` right now, I recommend using `2` for now.
4.  Search for `network.trr.uri` and set it to `https://doh.captnemo.in/dns-query`. You can find other options at [the cURL wiki](https://github.com/curl/curl/wiki/DNS-over-HTTPS).
5.  Set `network.trr.bootstrapAddress` to `139.59.48.222`. If you are using some other server, set accordingly (or let it remain blank)

(Based on [this article](https://www.ghacks.net/2018/04/02/configure-dns-over-https-in-firefox/) on ghacks)

## Uptime

This is currently considered `alpha`. It is expected to be up at all times aside for scheduled and emergency maintainence. I do not recommend this for Enterprise usage.

The [planned uptime is 99.99%](https://uptime.is/four-nines). There is no SLA provided, since this is a personal service.

You can monitor the uptime of the same at [status.captnemo.in](https://status.captnemo.in/).

## Privacy & Transparency

Please see [/dns/privacy](/dns/privacy) for the Privacy Policy, Transparency Guidelines, and Operating Principles of the resolver.

## Disclaimer

The service is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. in no event shall I be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.

## CHANGELOG

2019-05-15
: Resolver goes online at https://doh.captnemo.in

2019-05-12
: Published Draft policies for the Resolver.

[doh]: https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/ 'A cartoon intro to DNS over HTTPS'
