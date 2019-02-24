---
title: "Dealing with dead disks in a btrfs RAID1 array"
layout: post
tags:
    - btrfs
    - raid
    - S.M.A.R.T
---

**tl;dr**: Check your disk usage v/s RAID capacity to ensure that you can remove a disk before trying. If you can connect a new disk without removing the old one, run a `btrfs replace` - it is much faster.

---

My homeserver setup has a 4 disk setup:

1.  128GB Samsung EVO 850 SSD as the primary disk (root volume)
2.  A 3 Disk btrfs RAID1 Array that I use for almost everything else.

The 3 disks were:

1.  A WD-3.5inch-3TB that I shelled from a WD-MyBook. This was the oldest disk in the array
2.  2xSeagate 2.5-inch-3TB external disks that I shelled from Seagate Expansion disks.

The WD disk had been giving rising errors recently, and I was noticing hangs on the system as well:

1.  My Steam saves would take time, and hang the game.
2.  Kodi would ocassionaly hang just switching between screens as it would load images from disk.
3.  gitea, which writes a lot to disk would get similar issues.

I asked a question on [r/archlinux](https://www.reddit.com/r/archlinux/comments/asrlam/btrfscleaner_at_100_cpu_usage_on_raid1_setup/egwc047/) and confirmed that it indeed a dead disk.

Ordered a new Seagate Barracuda 3TB the next day, but my peculiar setup caused me a lot of pain before I could remove the dead disk. The primary issue was with the limited number of SATA connectors I had (just 4). The original setup had `/dev/sdb,/dev/sdc,/dev/sdd` as the three RAID disks with `/dev/sdb` being the dying WD.

This is what all I tried:

1.  Removing `/dev/sdb` and adding a new disk the array (`/dev/sde`). Unfortunately, to add a disk to the array, you have to mount it first, and the setup just refused to mount in degraded mode. (It didn't give a visibly error, so I didn't know why)
2.  I tried to keep the old disk attached over USB on a friend's suggestion, but that didn't work either. This was likely a cable issue, and I didn't investigate this further.
3.  Booting with the original three disks but replacing the dying disk with the new one post boot. Didn't work as I kept getting read/write errors to sdb even after it was disconnected.

In short:

-   the system refused to mount the raid array with a missing disk (and I didn't want to risk a boot with the array unavailable)
-   I couldn't do a live replace because I had a limited number of SATA connectors.

## What worked:

Running a `btrfs device delete` and leting it run overnight. It gave an error after quite a long time that finally helped me figure out the problem:

```
btrfs device delete /dev/sdb1 /mnt/xwing
ERROR: error removing device '/dev/sdb1': No space left on device

btrfs fi df /mnt/xwing
Data, RAID1: total=2.98TiB, used=2.98TiB
System, RAID1: total=32.00MiB, used=544.00KiB
Metadata, RAID1: total=5.49GiB, used=4.81GiB
GlobalReserve, single: total=512.00MiB, used=0.00B
```

The RAID array was 2.7TBx3 disks and I was storing roughly `2.98TB` of data. To switch to a RAID1 setup with just 2 disks, I needed to delete some data. I ended up clearing out a few steam games (bye bye Witcher 3) and ran another `btrfs device delete` to resolve the issue.

If you are faced with a situation where you have to remove a device, but can't do a live replace, here's what you need:

1.  Check that your disk removal does not impact any data storage. Your n-1 disk array should have enough capacity to store everything.
2.  Run a `btrfs device delete`
3.  Reboot
4.  Re-attach new disk, and then run a `btrfs device add`

{% include selfhosted.md %}
