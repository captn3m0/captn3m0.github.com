---
title: Google owned TLDs don't have A records any more
layout: post
---

A little while ago (Jan 2018), I ran a scan to see which all TLDs have an A record set (on the TLD). This is what lets you visit <http://ai/> as a valid website on your browser, for eg.

I ran the same scan as http://blog.towo.eu/a-records-on-top-level-domains/ (link is down, [archived](https://web.archive.org/web/*/http://blog.towo.eu/a-records-on-top-level-domains/)) and the results are at <https://captnemo.in/blog/2018/02/09/tld-a-records/>.

Decided to re-run the scan today, and noticed a stark difference: A lot of Google-owned TLD's which were earlier pointing to `127.0.53.53` don't have a A record anymore.

Scan run from `AS45609`.

Results:

|TLD|IP|Web|
|---|---|---|
|ai|209.59.119.34|[[http]](http://ai), [[https]](https://ai)|
|arab|127.0.53.53|Private IP|
|cm|195.24.205.60|[[http]](http://cm), [[https]](https://cm)|
|dk|193.163.102.58|[[http]](http://dk), [[https]](https://dk)|
|etisalat|127.0.53.53|Private IP|
|gg|87.117.196.80|[[http]](http://gg), [[https]](https://gg)|
|je|87.117.196.80|[[http]](http://je), [[https]](https://je)|
|pa|168.77.8.43|[[http]](http://pa), [[https]](https://pa)|
|pn|80.68.93.100|[[http]](http://pn), [[https]](https://pn)|
|politie|127.0.53.53|Private IP|
|tk|217.119.57.22|[[http]](http://tk), [[https]](https://tk)|
|uz|91.212.89.8|[[http]](http://uz), [[https]](https://uz)|
|ws|64.70.19.33|[[http]](http://ws), [[https]](https://ws)|
|мон|218.100.84.27|[[http]](http://мон), [[https]](https://мон)|
|мон|202.170.80.40|[[http]](http://мон), [[https]](https://мон)|
|мон|180.149.98.78|[[http]](http://мон), [[https]](https://мон)|
|اتصالات|127.0.53.53|Private IP|
|政府|127.0.53.53|Private IP|
|عرب|127.0.53.53|Private IP|
|招聘|127.0.53.53|Private IP|

Comparing with the previous scan, these TLDs no longer have an A record with them:

```diff
-android
-cal
-chrome
-dclk
-drive
-gle
-guge
-hangout
-nexus
-play
-sport
-谷歌
-グーグル
```

The majority of these are owned by Google. Not claiming it means anything, just a nice observation.

*Update*: An automatically updated version of this is available at https://captnemo.in/tld-a-record/
