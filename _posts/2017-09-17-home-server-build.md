---
title: Home Server Build
layout: post
tags:
    - homeserver
    - archlinux
    - hardware
image: home-server.jpg
---

I'd been planning to run my own home server for a while, and this culminated in a mini-ITX build recently. The current build configuration is available at </setup/homeserver/>.

In no particular order, here were the constraints:

-   The case should be small (I preferred the Elite 110, but it was unavailable in India).
-   Dual LAN, if possible (decided against it at the end). The plan was to run the entire home network from this directly by plugging in the ISP into the server.
-   Recent i3/i5 for amd64 builds.
-   Enough SATA bays in the cabinet for storage

The plans for the server:

1.  Scheduled backups from other sources (Android/Laptop)
2.  Run Kodi (or perhaps switch to Emby)
3.  Run torrents. Transmission-daemon works. Preferably something pluggable and that works with RSS
4.  Do amd64 builds. See https://github.com/captn3m0/ideas#arch-linux-package-build-system
5.  Host a webserver. This is primarily for serving resources off the internet
    -   Host some other minor web-services
    -   A simple wiki
    -   Caldav server
    -   Other personal projects
6.  Sync Server setup. Mainly for the Kindle and the phone.
7.  Calibre-server, koreader sync server for the Kindle
    -   Now looking at libreread as well
8.  Tiny k8s cluster for running other webapps
9.  Run a graylog server for sending other system log data (using papertrail now, has a 200MB limit)

No plans to move mail hosting. That will stay at migadu.com for now.

I had a lot of spare HDDs that I was going to re-use for this build:

1.  WD MyBook 3TB (external, shelled).
2.  Seagate Expansion: 1TB
3.  Seagate Expansion 3TB (external, shelled)
4.  Samsung EVO 128GB SSD

The 2x3TB disks are setup with RAID1 over `btrsfs`. Important data is snapshotted to the other 1TB disk using btrfs snapshots and subvolumes. In total giving me \~4TB of storage.

## Software

Currently running `kodi-standalone-service` on boot. Have to decide on a easy-to-use container orchestration platform. Choices as of now are:

1.  Rancher
2.  Docker Swarm
3.  Shipyard
4.  Terraform
5.  Portainer

Most of these are tuned for multi-host setups, and bring in a lot of complexity as a result. Looking at Portainer, which seems well suited to a single-host setup.

Other services I'm currently running:

1.  `elibsrv`. Running a patched build with support for ebook-convert
2.  `ubooquity` for online reading of comics

![](/img/home-server.jpg)

{% include selfhosted.md %}
