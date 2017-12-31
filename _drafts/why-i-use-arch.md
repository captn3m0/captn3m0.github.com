---
layout: post
title: Why I use Arch?
---

I switched to Arch around June 2015. I was then using Elementary OS as my primary, and Ubuntu as a secondary OS. I took the plunge and switched straight to Arch Linux+i3. Just writing my thoughts on why Arch works for me, and whether it would work for you. In the time since, I've had:

- One major kernel upgrade (3->4)
- 2 hard disk switches (320GB HDD -> 128GB SSD -> 256GB SSD)
- To setup a parallel work environment on another laptop using same config
- Thousands of package installations and upgrades (I started tracking them this year)

All while keeping my _system and personal configuration_. This is why I :heart: Arch Linux:

## Rolling Distro aka No Yearly Upgrades

Arch Linux being a rolling distribution means I'm always on the latest version of everything. Most packages get upgraded within a few days of an upstream release. If you've ever been frustrated by a large OS upgrade breaking your workflow (I remember not upgrading to Unity for quite some time when Ubuntu switched), this is the perfect fix.

Instead of one-big-break, you get individual upgrades that you can apply cleanly and manage in isolation.

### Caviats

- Rolling distro also means your kernel gets upgraded every fortnight
- Package upgrades might introduce new features, or config syntax changes. You have to take care of them _as you run upgrades_. Upgrading your packages and config becomes a housekeeping chore.

### Notes

- You can use the LTS kernel for kernel-level stability

## Customizability

I used to have a very-customized Windows setup around a decade back. I even wrote about my Vista setup. At the end, it boils down to: whatever workflow works for you. For me, this means:

- Locking my laptop as soon as I unplug my Yubikey
- Being able to create my own packages for software that I use
- 