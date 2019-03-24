---
title: Kindle Hacks Guide for Self
layout: post
---

I run a non-standard Kindle configuration:

1.  Jailbroken
2.  Runs KOReader
3.  And I strip DRM from every book that I purchase from Kindle.

Since I don't do any of these often enough to automate it, this is a self guide.

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
