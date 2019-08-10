---
layout: post
title: Downgrading my iPad 2 to iOS 8
tags:
    - ios
    - downgrade
    - ipad
---

I own a iPad 2 (GSM), which is rarely used these days because it is too slow with the latest iOS 9 upgrades. It is a 8 year old device, but I can't just install Linux on it and make it usable, which is what I do with most other devices.

The next best thing was to downgrade the iOS version. The device is anyway un-supported at this point, so I might as well go there. Apple has restrictions on which iOS releases are installable at any point on any device, but thankfully they are still signing iOS6 for my device for some legal reasons.

## Steps:

1. Download the iOS firmware for your device from <https://ipsw.me/#platform>
2. Launch iTunes
3. Option+Click on the Restore button in iTunes
4. Select the file you just downloaded.
5. Disable iCloud on the device
6. Upgrade to iOS8

This is possible as long as Apple is signing the IPSW for your device. The case of iOS6 being signed seems to be true for:

- iPhone 4S
- iPad 2

## Security Notes

Running an unsupported OS is not something I take lightly. Here's a list of defensive measures I took to ensure that I'm not at risk while doing so:

1. Try to keep the device always in Airplane mode.
2. Keep sensitive data off the device. No photos/keychain sync for eg. Don't enable Calendar/Contact/Media sync.
3. Enable Restrictions on the device:
 - Restrict Safari to limited websites.
 - Disable application installs.
 - Disable iTunes store/iBooks store etc.
 - Disable GPS/Bluetooth.
 - Limit Background Refresh to very few trusted applications.
4. Limit number of applications (I only have Kybooks installed).
5. Disable Javascript on Safari.

If possible, I'd recommend using a separate Apple Account on the device.