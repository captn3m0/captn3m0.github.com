---
title: Kindle Hacks, A Self-guide
layout: post
---

I run a non-standard Kindle configuration:

1.  Jailbroken <small>(because I want to own the device, not rent it)</small>
2.  Runs KOReader <small>(because I want to read EPUBs and PDFs with reflow.)</small>
3.  DRM Stripping <small>(because I want to own the book, not rent it)</small>

Since I don't do any of these often enough to automate it, this is a self guide to help me follow these steps the next time I have to do any of this. No guarantees of this being helpful to anyone else but me.

# Jailbreak

The [lifehacker guide on how to jailbreak your kindle](https://lifehacker.com/how-to-jailbreak-your-kindle-1783864074) is a good starting point [[archived](https://outline.com/cEZNAt)]. The mobileread forums have the [definitive guides](https://www.mobileread.com/forums/showthread.php?t=275881). Also see [this FAQ](https://wiki.mobileread.com/wiki/5_x_Jailbreak#Will_this_jail_break_work_on_my_current_firmware.3F) on the mobileread wiki.

(Most of these only cover modern paperwhite kindles)

## Maintaining the Jailbreak

Sometimes, Kindle firmware updates will stop the Jailbreak. Search for your firmware on mobileread forums. See [this link](https://www.mobileread.com/forums/showthread.php?p=3562050) for the 5.8 series.

Copy the `.bin` file to your kindle root directory and trigger a manual firmware update. That should reboot and re-affirm the jailbreak. To trigger a manual firmware update, go to the Kindle Menu and click "Update". If it is greyed out, check if the file was copied correctly, and try rebooting.

# Applications

Once you have a jailbreak, the rest is mostly installing packages via MRPI. I keep a ready directory of packages I can copy as-is to my Kindle. The current listing is at <https://paste.ubuntu.com/p/CXS5hYZdqc/> with most of it just being koreader.

[koreader](https://koreader.rocks/) is a FOSS document viewer for E Ink devices that supports Kindle, Kobo, PocketBook, Ubuntu Touch and Android devices.

The primary 2 packages are:

-   `Update_KUALBooklet_v2.7_install.bin`
-   `update_kpvbooklet_0.6.6_install.bin`

Run `;log mrpi` via search after copying them to re-install them if needed.

## koreader

Download the latest release from [GitHub](https://github.com/koreader/koreader/releases/latest).

You should download the `kindle5-linux-gnueabi` package for modern Paperwhites. Unzip it to the copy directory mentioned above.

Aside: koreader has a linux appimage version for desktops, which [I package for AUR](https://aur.archlinux.org/packages/koreader-appimage/).

# DRM Related Stuff

DRM is inherently bad for users. If I switch my Ebook reader from Kindle (which are great _as of today_) to
a Kobo tomorrow, I want my content to stay with me.

There are much better websites that explain the issues with DRM, so go visit: [fckdrm.com](https://fckdrm.com/), [DefectiveByDesign.org](https://www.defectivebydesign.org/), or [EFF/drm](https://www.eff.org/issues/drm).

The primary tool for stripping DRM from Kindle books is [apprenticeharper's DeDRM Repo](https://github.com/apprenticeharper/DeDRM_tools).

## Getting the Key

My current key is saved in pass:

`pass show Keys/Kindle.k4i |jq`

Save it in a file, which you can import to Calibre.

If you don't have the key or if the above isn't valid, see [this comment on r/ebooks](https://www.reddit.com/r/ebooks/comments/2muccd/remove_drm_restrictions_from_almost_any_type_of/cm8f5gt/) [[archived](https://web.archive.org/web/20190326171740/https://www.reddit.com/r/ebooks/comments/2muccd/remove_drm_restrictions_from_almost_any_type_of/cm8f5gt/)].

## Importing the Key

> At the bottom-left of the plugin’s customization dialog, you will see a button labeled "Import Existing Keyfiles". Use this button to import existing ‘.k4i’ key files. Key files might come from being exported from this plugin, or may have been generated using the kindlekey.pyw script running under Wine on Linux systems.

I once did some trickery on the `kindlekey.pyw` application to get it working on my system, but I didn't take notes. If I ever do this again - AUTOMATE THIS.

## Stripping DRM

1.  Install Kindle for PC. It does work on Wine. Make sure you download `1.17.0 (44170)`. I trust [filehippo](https://filehippo.com/download_kindle_for_pc/download/a6284b51053b0e38f4b9f90d4470bd91/) for this. The sha256sum for the installer is `14e0f0053f1276c0c7c446892dc170344f707fbfe99b6951762c120144163200`. I have a backup copy referenced below as well.
2.  Launch it, and download the book.
3.  Go to `~/Documents/My Kindle Content`
4.  Find book by Last Modified Date.
5.  Run `calibredb add book.azw`. If all goes well, the book should show up in your library, and you should be able to convert it.

---

# Reference Files

I have a backup of my current Kindle files at http://ge.tt/75zk4Dv2 in case you need any of the files mentioned above. Checksums for the files are below, since `ge.tt` doesn't believe in HTTPS:

```
e3b05193ed9d0b482f01dfb550eba67f3b113b5165aae5632379cf35fec2f59d  copy.tar.gz
14e0f0053f1276c0c7c446892dc170344f707fbfe99b6951762c120144163200  KindleForPC-installer-1.17.44170.exe
50bb0e5d9c03bcb79b17c1b7063cefd2c947a9d1c4392814e6ec05225296472a  kual-helper-0.5.N.zip
39352b4b68993680f06d5ecc57ce7ec4c271b6b5f2386ea998027420c45f2acd  KUAL-KDK-1.0.azw2
ceb207ee4c8d3674f308ff91432aeabf213b203571e270f70b8ae218df6ded7d  KUAL-KDK-2.0.azw2
fce02f0e104e846f1e4cc0e029500c5a722614d63a47035d78ea4cf59f67a448  kual-mrinstaller-1.6.N.zip
4a6de1fafe47ec0e3bfb529edead401c92e66b00697d507abe945679b3b7bc65  KUAL-v2.7.zip
253d0b00b31d62ef9dadb7ca88b98e2718cb35246816b3c50dd63c0a7ef28a52  Update_jailbreak_hotfix_1.14_5.8.10_install.bin
cc63ba1b454d1f32492c835f108ee04aaa80e6e7a95f12b7216c2c015daa2fbc  Update_jailbreak_hotfix_1.14_nomax_install.bin
```
