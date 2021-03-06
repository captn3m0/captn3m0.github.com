---
layout: post
title: adventures with systemd, btrfs, and RAID
---

After facing lots of challenges with a hard disk enclosure I'd recently acquired, I decided to drop it and move the disks inside the case instead. As my homeserver has gotten upgrades over time, some of the older disks have become redundant. This was my RAID setup until a few days ago:

```
Total devices 5 FS bytes used 3.26TiB
  devid    2 size 2.73TiB used 0.00B path /dev/sdd1
  devid    3 size 2.73TiB used 0.00B path /dev/sdb1
  devid    4 size 2.73TiB used 0.00B path /dev/sdc1
  devid    5 size 7.28TiB used 3.28TiB path /dev/sde
  devid    6 size 7.28TiB used 3.28TiB path /dev/sdf
```

The first 3 disks here were (3x3TB) were all connected over internal SATA connectors. The 2x8TB disks were connected over a USB3 cable to a hard disc enclosure that did USB3<>SATA interop of some sort.

Since I was facing many issues with the enclosure, and none of my internal disks were getting used, I decided to move the disks from the external enclosure to inside my case. I did this alongside a RAM upgrade, and the disks started showing up correctly (as `/dev/sdb` and `/dev/sdc`). However, the RAID1 configuration broke, since 3/5 disks were missing - quite expected.

<aside><details><summary>How my RAID1 setup boots</summary>
`btrfs` RAID is nicely supported on ArchLinux. You need to make sure that your mkinitcpio hooks include btrfs. Then, I have a custom systemd service that runs a btrfs ready check before the mounts happen. The mount itself happens as a normal fstab mount, which gets delegated to systemd-mount.
</details>
</aside>

Note that the 3 disks I'd removed - all had zero usage at this point. The next step here would be to run `btrfs device delete` which removes a disk from a btrfs RAID filesystem. However, to run this command, your filesystem must be mounted in RW mode. The normal way to do that after disk changes is to use the recovery mode:

`mount -o recovery /dev/sdc /mnt/xwing`.

This command returned no errors, even if I got a few warnings in my dmesg:

```
BTRFS info (device sdc): allowing degraded mounts
BTRFS info (device sdc): disk space caching is enabled
BTRFS info (device sdc): has skinny extents
BTRFS warning (device sdc): devid 2 uuid c2e4fe2d-5a6e-4402-8a2f-5530617fb49a is missing
BTRFS warning (device sdc): devid 3 uuid 202482b3-1523-4e37-86bf-1fa3cf65217f is missing
BTRFS warning (device sdc): devid 4 uuid 37d84c6b-46e2-439e-94f1-3f3b5889f2b9 is missing
BTRFS info (device sdc): bdev (efault) errs: wr 0, rd 98834, flush 0, corrupt 0, gen 0
```

However, when I checked the actual mount path, it wasn't really mounted. Running `mount` didn't show sdc as mounted anywhere. I played around a bit with various mount options (`ro`) to no avail.

After getting nowhere with this problem, I asked for help on the btrfs IRC channel. What confused everyone was that:

- The mount looks like it succeeds (I even got a 0 return), yet
- there was nothing in the logs to say why it wasn't getting mounted.

Someone suggested me to try mounting on a different path, and _it worked!_. Turns out `systemd` was unmounting the disk as soon as it was mounted. I found the smoking gun on the journalctl logs:

```
systemd: mnt-xwing.mount: Unit is bound to inactive unit dev-disk-by\x2duuid-493787da\x2db488\x2d4661\x2db95c\x2d2a132109efa6>
systemd: Unmounting /mnt/xwing
```

Which made me ask - *Why?* One of the benefits of running Arch is that I'm responsible for the complete system - including the way disks are mounted. I went down the rabbit hole to figure out why this was happening.

## systemd

systemd, as you ought to know, tries to do everything - including mounting disks on its own. However, most linux systems usually use `/etc/fstab` to actually configure disk mounts. systemd supports disks mounts via a [mount unit configuration](https://www.freedesktop.org/software/systemd/man/systemd.mount.html), which are unit configuration files ending with `.mount`.

Since nobody is going to write these files, `systemd` comes with a nice [systemd-fstab-generator](https://www.linux.org/docs/man8/systemd-fstab-generator.html) that translates `/etc/fstab` into native systemd units _early at boot_.

## mkinitcpio

The _early at boot_ part where `systemd-fstab-generator` is meant to run is configured via `mkinitcpio` in ArchLinux. This prepares the `initramfs` by letting you add/remove hooks into the linux init process. For eg, I have the `btrfs` hook configured, which:

1. [adds the btrfs linux module](https://github.com/archlinux/svntogit-packages/blob/packages/btrfs-progs/trunk/initcpio-install-btrfs)
2. [runs a device scan](https://github.com/archlinux/svntogit-packages/blob/packages/btrfs-progs/trunk/initcpio-hook-btrfs)

In my case, I had some requirements for running the `systemd` hook, which lets me run a select few systemd services before init itself runs. In hindsight - this was a bad idea. Unfortunately, this hook does a lot more than what I wanted. It installs a few units that ensure that the mounts now happen via systemd instead:

### `local-fs.target`

This is set as the target for all mount units generated by `systemd-fstab-generator`.

However, we still haven't actually run the generator yet. `systemd` runs all generators when you run `systemctl daemon-reload`(!). In this case, reading through the [`bootup`](https://www.man7.org/linux/man-pages/man7/bootup.7.html) man page tells us more.

### `initrd-parse-etc.service`

This is the first service (not target) that actually runs in the systemd-init process. The Unit file isn't that confusing:

```ini
[Unit]
Description=Reload Configuration from the Real Root
DefaultDependencies=no
Requires=initrd-root-fs.target
After=initrd-root-fs.target
OnFailure=emergency.target
OnFailureJobMode=replace-irreversibly
ConditionPathExists=/etc/initrd-release

[Service]
Type=oneshot
ExecStartPre=-systemctl daemon-reload
# we have to retrigger initrd-fs.target after daemon-reload
ExecStart=-systemctl --no-block start initrd-fs.target
ExecStart=systemctl --no-block start initrd-cleanup.service
```

The `ExecStartPre` step here runs the `daemon-reload`, which in turn triggers the `systemd-fstab-generator`, which generates the mount files from the fstab. Then when we reach `local-fs.target`, these mount points are pulled in as a dependency and get mounted.

At this point, systemd claims complete authority over that mountpoint - any attempts to mount anything on a failed-mount will be immediately met with a umount. [A lot of folks](https://bugzilla.redhat.com/show_bug.cgi?id=1494014) have cursed this behaviour to no avail and looks like systemd [might get a fix for this](https://github.com/w-simon/systemd/commit/2cb551af8cee8d9e71a68340c3a088fb2602ebfa) - the PR isn't yet approved.

## Learning

1. Running `systemd` during initrd is a bad idea.
2. Don't run a manual mount to a mountpoint managed by `systemd`
3. There's some [interesting mount options](https://www.freedesktop.org/software/systemd/man/systemd.mount.html) that systemd supports, but none of them disable the auto-unmount behaviour.