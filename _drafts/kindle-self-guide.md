---
title: Kindle Hacks Guide for Self
layout: post
---

I run a non-standard Kindle configuration:

1.  Jailbroken
2.  Runs KOReader
3.  And I strip DRM from every book that I purchase from Kindle.

Since I don't do any of these often enough to automated it, this is a self guide.

# DRM Related Stuff

DRM is inherently bad for users. If I switch my Ebook reader from Kindle (which are great) to
a Kobo tomorrow, I want my content to stay with me.

See https://www.eff.org/issues/drm for more details.

## Stripping DRM

1.  Install Kindle for PC. It works on Wine. Make sure you download `1.17.0 (44170)`
2.  Launch it, and download the book
3.  Go to `~/Documents/My Kindle Content`
4.  Find book by Last Modified
5.  Run `calibredb add book.azw`

## Getting the Key

My current key is saved in pass:

`pass show Keys/Kindle.k4i |jq`

## Importing the Key

> Importing Existing Keyfiles:

> At the bottom-left of the plugin’s customization dialog, you will see a button labeled "Import Existing Keyfiles". Use this button to import existing ‘.k4i’ key files. Key files might come from being exported from this plugin, or may have been generated using the kindlekey.pyw script running under Wine on Linux systems.

## Getting the Key

If you don't have the key, see this comment: https://www.reddit.com/r/ebooks/comments/2muccd/remove_drm_restrictions_from_almost_any_type_of/cm8f5gt/
