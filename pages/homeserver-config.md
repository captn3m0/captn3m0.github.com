---
layout: page
title: Homeserver Configuration
permalink: /setup/homeserver/
---

This is the latest hardware configuration of my homeserver.

Category|Details|Notes
----|-------|-----
CPU|[Intel Core i5-7600 3.5 GHz Quad-Core](https://ark.intel.com/content/www/us/en/ark/products/97150/intel-core-i5-7600-processor-6m-cache-up-to-4-10-ghz.html)
Motherboard|[MSI B250I GAMING PRO AC Mini ITX LGA1151](https://www.msi.com/Motherboard/B250I-GAMING-PRO-AC.html)
Memory|Kingston HyperX Fury Black 8 GB (1 x 8 GB) DDR4-2133 CL14 Memory
~~Memory~~|~~Kingston HyperX Fury Black 8 GB (1 x 8 GB) DDR4-2133 CL14 Memory~~|Dead. Awaiting replacement
Primary Storage|[Samsung 850 EVO-Series 120 GB](https://amzn.to/2I0QyfA) 2.5" Solid State Drive|Re-used from a previous laptop upgrade. Used for the OS
Internal Storage|Seagate 3TB ([ST3000DM008](https://amzn.to/36DfQKL))|Internal, SATA
Internal Storage|Seagate 3TB ([ST3000DM008](https://amzn.to/36DfQKL))|Internal, SATA
Internal Storage|Seagate Barracuda 3 TB ([ST3000DM008](https://amzn.to/2GE0F9l))|Internal, SATA
External Storage|[Seagate Desktop 8 TB](https://www.amazon.de/gp/product/B07DQBFQ2D) 3.5" 5400RPM Internal Hard Drive|Connected over USB to HDD enclosure
External Storage|[Seagate Desktop 8 TB](https://www.amazon.de/gp/product/B07DQBFQ2D) 3.5" 5400RPM Internal Hard Drive|Connected over USB to HDD enclosure
Graphic Card|[MSI GeForce GTX 1050 Ti 4 GB Video Card](https://www.msi.com/Graphics-card/GeForce-GTX-1050-Ti-GAMING-X-4G.html)
Case|[Cooler Master Elite 130 Mini ITX Tower Case](https://www.coolermaster.com/catalog/cases/mini-itx/elite130/)
HDD Enclosure|ORICO Multi Bay HDD Enclosure [3529RUS3-V1-SV](https://www.orico.me/product/orico-aluminum-3-5-inch-sata-usb3-0-esata-external-multi-bay-hdd-enclosure-on-the-desktop-3529rus3/)|Pre-used from a friend
Power Supply|[Cooler Master GM 450 W 80+ Bronze Semi-modular ATX Power Supply](https://www.coolermaster.com/catalog/power-supplies/masterwatt/masterwatt-450/)
UPS|[APC BX600CI-IN UPS](https://amzn.to/34t22Qv)
Audio|[F&D E200 Sound Bar](https://amzn.to/33B5oBy)|Connected to TV Aux out.<br>Pre-used from a friend

## Hardware Changelog

### Mar 2018

-   Switched from the 1TB Expansion to a 3TB Seagate Expansion that I got cheap on Amazon. The disk setup is now btrfs RAID1 over 3x3TB disks.
-   I added a UPS. [Twitter Thread](https://twitter.com/captn3m0/status/973264624752603136) with some details.

### Sep 2018

I added a new 8GB RAM (Kingston HyperX Fury DDR4), and a NVidia Graphics Card (1050 Ti 4GB OC)

### Jan 2019

A friend was leaving Bangalore and offered me her UPS, so now I have a 2xUPS(600VA) setup now.

### Feb 2019

The WD 3TB MyBook HDD was dying, so I replaced it with a 3TB Seagate Barracuda Internal HDD. Switching the disks was a challenge due to some btrfs issues. I wrote about it [here](https://captnemo.in/blog/2019/02/24/btrfs-raid-device-replacement-story/).

## Mar 2020

Added a 8TBx2 RAID setup. The disks are identical [8TB Amazon SE Seagate Expansions](https://www.amazon.co.uk/d/B07DQBFQ2D/), which I got for cheap, and the RAID enclosure is a pre-used ORICO. First time I'm running a hardware RAID setup, lets see how it goes. Moved the second UPS to my PC setup and got a sound bar for audio.

## Apr 2020

One of the RAM sticks died, so I'm down to 8GB again. The hardware RAID setup isn't working well, so I turned it off.

## Sep 2020

Attempted to revive the 2xTB setup. Moved to btrfs RAID and added both the disks individually to my normal RAID configuration. Works much better than the hardware RAID. Both the disks are still connected over the HDD enclosure, but the enclosure presents them as 2 individual disks now. Here's how it shows up:

```
Total devices 5 FS bytes used 3.26TiB
  devid    2 size 2.73TiB used 0.00B path /dev/sdd1
  devid    3 size 2.73TiB used 0.00B path /dev/sdb1
  devid    4 size 2.73TiB used 0.00B path /dev/sdc1
  devid    5 size 7.28TiB used 3.28TiB path /dev/sde
  devid    6 size 7.28TiB used 3.28TiB path /dev/sdf
```

Last Updated: 16th October 2020.

{% include selfhosted.md %}