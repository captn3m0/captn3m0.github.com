---
title: Kindle Hacks Guide for Self
layout: post
---

I run a non-standard Kindle configuration:

1.  Jailbroken
2.  Runs KOReader
3.  DRM Stripping

Since I don't do any of these often enough to automate it, this is a self guide.

# Jailbreak

The lifehacker guide is a good starting point: https://lifehacker.com/how-to-jailbreak-your-kindle-1783864074

The mobileread forums have the definitive guides: https://www.mobileread.com/forums/showthread.php?t=275881

Also see https://wiki.mobileread.com/wiki/5_x_Jailbreak#Will_this_jail_break_work_on_my_current_firmware.3F

(Most of these only cover modern paperwhite kindles)

## Maintaining the Jailbreak

Sometimes, Kindle firmware updates will stop the Jailbreak. Search for your firmware on mobileread forums. For 5.8 series, see https://www.mobileread.com/forums/showthread.php?p=3562050

Copy the `.bin` file to your kindle root directory and trigger a manual firmware update. That should reboot and re-affirm the jailbreak.

# Applications

Once you have a jailbreak, the rest is mostly installing packages via MRPI. I keep a ready directory of packages I can copy as-is to my Kindle. The current listing is at https://paste.ubuntu.com/p/CXS5hYZdqc/ with most of it just being koreader.

The primary 2 packages are:

-   `Update_KUALBooklet_v2.7_install.bin`
-   `update_kpvbooklet_0.6.6_install.bin`

Run `;log mrpi` via search after copying them to re-install them if needed.

## Koreader

Download the latest release from https://github.com/koreader/koreader/releases/latest.

You should download the `kindle5-linux-gnueabi` package for modern paperwhites. Unzip it to the copy directory mentioned above.

Aside: koreader has a linux appimage version for desktops, which [I package for AUR](https://aur.archlinux.org/packages/koreader-appimage/).

# DRM Related Stuff

DRM is inherently bad for users. If I switch my Ebook reader from Kindle (which are great) to
a Kobo tomorrow, I want my content to stay with me.

See https://www.eff.org/issues/drm for more details.

## Getting the Key

My current key is saved in pass:

`pass show Keys/Kindle.k4i |jq`

Save it in a file, which you can import to Calibre.

If you don't have the key or if the above isn't valid, see this comment: https://www.reddit.com/r/ebooks/comments/2muccd/remove_drm_restrictions_from_almost_any_type_of/cm8f5gt/

## Importing the Key

> At the bottom-left of the plugin’s customization dialog, you will see a button labeled "Import Existing Keyfiles". Use this button to import existing ‘.k4i’ key files. Key files might come from being exported from this plugin, or may have been generated using the kindlekey.pyw script running under Wine on Linux systems.

## Stripping DRM

1.  Install Kindle for PC. It does work on Wine. Make sure you download `1.17.0 (44170)`. I trust [filehippo](https://filehippo.com/download_kindle_for_pc/download/a6284b51053b0e38f4b9f90d4470bd91/) for this. The sha256sum for the installer is `14e0f0053f1276c0c7c446892dc170344f707fbfe99b6951762c120144163200`
2.  Launch it, and download the book.
3.  Go to `~/Documents/My Kindle Content`
4.  Find book by Last Modified Date.
5.  Run `calibredb add book.azw`
