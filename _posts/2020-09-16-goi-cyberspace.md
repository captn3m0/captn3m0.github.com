---
layout: post
title: Analysing the Indian government cyberspace
tags: goi,dataviz
---

I recently did some work on analysing the Indian government cyberspace, thought I should document them somewhere outside of my Twitter[^9].

## List of GoI websites

I'd made a list of Indian government websites in Jan 2019:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I ran <a href="https://twitter.com/18F?ref_src=twsrc%5Etfw">@18F</a> /pulse on Indian Government websites to see how many of them support HTTPS. A quick summary:<br><br>Total Websites: 14183<br>Total Live Websites: 11710 (82%)<br>Websites with Valid HTTPS: 4753 (40% of all live websites)<br><br>Raw Dataset for now: <a href="https://docs.google.com/spreadsheets/d/16LWWplbSAu-EkWk4R7OVsk8JM6guyZ3yiKdXIzBDT_Q/edit?usp=sharing">docs.google.com/spreadsheets</a></p>&mdash; Nemo (@captn3m0) <a href="https://twitter.com/captn3m0/status/1085050749011161089?ref_src=twsrc%5Etfw">January 15, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The dataset was from 2 sources:

1. [GoI Directory](http://goidirectory.nic.in/)
2. [crt.sh](https://crt.sh) (All certificates ending in `.gov.in` were used)

I re-ran the scripts to get an updated list (12842 domains), then tabulated them against the public-suffix[^1] for each. There is a long-tail, and I've published results [here](https://gist.github.com/captn3m0/4f3da8f07fe884e62bfab3ac85616936). Here are the top public suffixes for Indian government sites:

Public Suffix|Domains|
-------------|-------
nic.in|2454
gov.in|7259
in|528
ac.in|490
com|568
co.in|171
org.in|168
edu.in|117
org|844
res.in|134
net.in|12
net|38

## Sanskari Proxy

This was a long standing idea on my [ideas repo][ideas]:

>A lot of Indian Government websites are inaccessible on the public internet, because
>they geo-fence it to within Indian Boundaries. The idea
>is to make a Indian Proxy service that specifically works only for the Geo-fenced Indian government
>websites.
>
>For eg, if `uidai.gov.in` is inaccessible, hitting `uidai.gov.sanskariproxy.in` will get you
>the same result, proxied via our servers.

Since I'd made an updated list of GoI websites, this seemed easy enough. I realized that setting up `uidai.gov.sanskariproxy.in` would likely count as impersonation under the Indian law,
so I did the next best thing: run an actual proxy. Here's the announcement tweet:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Are you a security researcher outside India? Do you hate getting geoblocked to Indian government websites?<br><br>Well, I made a proxy for security researchers outside India to access Indian government websites without resorting to shady VPNs.<br><a href="https://github.com/captn3m0/sanskari-proxy">captn3m0/sanskari-proxy</a></p>&mdash; Nemo (@captn3m0) <a href="https://twitter.com/captn3m0/status/1302191390508552192?ref_src=twsrc%5Etfw">September 5, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Project page is <https://github.com/captn3m0/sanskari-proxy>, and if you'd like to get access - please reach out.

## Cyberspace Ownership

I'd planned to get a complete list of geoblocked websites next. While I'm progressing on this front, the results have been inconsistent/inaccurate so far. As an intermediate step, I'd made a list of IPs against every domain[^2], which looked like this:

Domain|IP Address
---|---
aavin.tn.gov.in|164.100.134.148
abnhpm.gov.in|14.143.233.34
agnii.gov.in|13.232.216.65
ap.gov.in|117.254.92.53
aponline.gov.in|125.16.9.130
appolice.gov.in|118.185.110.147
attendance.gov.in|164.100.166.114
cgg.gov.in|112.133.222.115

While running numerous nmap scans (and failing), I start checking the <abbr title="Autonomous System Number"><a href="https://en.wikipedia.org/wiki/Autonomous_system_(Internet)">ASN</a></abbr>[^asn] for some of these IPs to see who was hosting each website - especially the ones I was finding were blocked.

I stumbled upon a bulk [IP to ASN service](https://team-cymru.com/community-services/ip-asn-mapping/) by Cymru, ran all the IPs against it and published the results. Here's the important graph:

![% of Indian Government domains hosted by each ASN. The image is a pie-chart representation showing share of each ASN. 45% of the chart is taken up by ](/img/domain-by-asn.png)

As you can expect, <abbr title="National Informatics Centre">NIC</abbr>[^nic] has the highest share, with <abbr title="National Knowledge Network">NKN</abbr>[^nkn], BSNL, and [CtrlS](https://www.ctrls.in/) following at roughly 5% each. There are a few other chart on [the twitter thread](https://twitter.com/captn3m0/status/1303683006276620288), and the raw data is available [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vRFcjIsqE13A7FaRID_z_ETFtGNdpznx4VcFfmEzJGjHBx-oT-urp60C9BZZK7Umc9f5QX0Z4Yd3Vja/pubhtml#) with interactive versions of each visualization.

## What next?

I'm working on running and comparing connectivity scans to these IPs to get a better understanding of the geoblocking situation. There's also some issues with the domain list, as it seems to be missing lots of domains - so more corrections are needed.

[^1]: A "public suffix" is one under which Internet users can (or historically could) directly register names. For eg - `nic.in` or `github.io`. Mozilla manages the list at <https://publicsuffix.org/>.
[ideas]: https://github.com/captn3m0/ideas
[^2]: There are issues with this approach, since domains do resolve to multiple IPs. But this is okay for the rudimentary analysis I've been doing so far.
[^9]: Twitter decided to suspend 12 different accounts I had access to recently - I'm starting to get wary of using Twitter for archival now.
[^asn]: Autonomous Systems (AS) is how the internet is sliced up and managed by different entities. Each AS (usually an ISP) is responsible for routing within its network, while announcing network routes on how it can be reached.
[^nkn]: National Knowledge Network is a multi-gigabit research and education network that provides a high speed network backbone for educational institutions in India.
[^nic]: The primary government office (under <abbr title="Ministry of Electronics and Information Technology">MeitY</abbr>) that provides infrastructure and support for government IT services.